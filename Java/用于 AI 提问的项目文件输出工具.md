```java
import com.google.common.collect.Lists;
import org.apache.commons.lang3.StringUtils;

import java.io.IOException;
import java.nio.charset.StandardCharsets;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

public class ProjectFilePrinter {
    private final List<String> ignorePatterns;
    private final List<String> extraIgnoreDirs;
    private final Path baseDir;

    public ProjectFilePrinter(Path gitignorePath, Path baseDir, List<String> extraIgnoreDirs) throws IOException {
        this.baseDir = baseDir;
        this.extraIgnoreDirs = extraIgnoreDirs != null ? extraIgnoreDirs : new ArrayList<>();
        ignorePatterns = new ArrayList<>();
        if (Files.exists(gitignorePath)) {
            ignorePatterns.addAll(Files.readAllLines(gitignorePath)
                    .stream()
                    .map(String::trim)
                    .filter(line -> !line.isEmpty() && !line.startsWith("#"))
                    .collect(Collectors.toList()));
        }
    }

    public void printFileTreeAndContents() throws IOException {
        System.out.println("## Project Structure");

        // 收集所有非忽略的文件
        List<Path> files = new ArrayList<>();
        System.out.println(baseDir.getFileName() != null ? baseDir.getFileName() : ".");
        printFileTreeRecursive(baseDir, "", files);

        // 输出每个文件的内容
        System.out.println("\n## File Contents:");
        for (Path file : files) {
            printFileContent(file);
        }
    }

    private void printFileTreeRecursive(Path directory, String indent, List<Path> files) throws IOException {
        List<Path> entries = Files.list(directory)
                .filter(this::isNotIgnored)
                .sorted((p1, p2) -> {
                    // 目录优先于文件，文件名按字母排序
                    boolean isDir1 = Files.isDirectory(p1);
                    boolean isDir2 = Files.isDirectory(p2);
                    if (isDir1 != isDir2) {
                        return isDir1 ? -1 : 1;
                    }
                    return p1.getFileName().toString().compareTo(p2.getFileName().toString());
                })
                .collect(Collectors.toList());

        for (int i = 0; i < entries.size(); i++) {
            Path entry = entries.get(i);
            boolean isLast = i == entries.size() - 1;
            String prefix = indent + (isLast ? "└── " : "├── ");
            System.out.println(prefix + entry.getFileName());

            if (Files.isDirectory(entry)) {
                String newIndent = indent + (isLast ? "    " : "│   ");
                printFileTreeRecursive(entry, newIndent, files);
            } else if (Files.isRegularFile(entry)) {
                files.add(entry);
            }
        }
    }

    private void printFileContent(Path file) throws IOException {
        String relativePath = baseDir.relativize(file).toString().replace("\\", "/");
        String fileName = file.getFileName().toString();
        String extension = getFileExtension(fileName).toLowerCase();
        // 使用 Files.readAllBytes 读取文件内容，兼容 Java 8
        String content = new String(Files.readAllBytes(file), StandardCharsets.UTF_8);

        System.out.println("\n### " + fileName);
        System.out.println("\n- ./" + relativePath);
        System.out.println("```" + extension);
        System.out.println(content.trim());
        System.out.println("```");
    }

    private String getFileExtension(String fileName) {
        int lastDot = fileName.lastIndexOf('.');
        return lastDot > 0 ? fileName.substring(lastDot + 1) : "";
    }

    private boolean isNotIgnored(Path path) {
        String relativePath = path.toString().replace("\\", "/");
        // 检查 .gitignore 模式
        for (String pattern : ignorePatterns) {
            String regex = patternToRegex(pattern);
            if (relativePath.matches(regex) || relativePath.contains("/" + pattern)) {
                return false;
            }
        }
        // 检查额外忽略的目录
        for (String pattern : extraIgnoreDirs) {
            String regex = patternToRegex(pattern);
            if (relativePath.matches(regex) || relativePath.contains("/" + pattern)) {
                return false;
            }
        }
        return true;
    }

    private String patternToRegex(String pattern) {
        String regex = pattern.replace(".", "\\.")
                .replace("*", ".*")
                .replace("?", ".?")
                .replace("/", "\\/");
        return ".*" + regex + ".*";
    }

    public static void main(String[] args) {
        // 读取的根目录
        String rootDir = "";
        // .gitignore 文件的路径
        String gitignoreFile = "";
        // 额外的忽略目录
        List<String> extraIgnoreDirs = Lists.newArrayList(".git", "test/");

        boolean ignoreReadme = true;
        try {
            Path directory = Paths.get(StringUtils.firstNonBlank(rootDir, "."));

            // 确保目录存在
            if (!Files.exists(directory) || !Files.isDirectory(directory)) {
                System.err.println("Error: Specified directory does not exist or is not a directory: " + directory);
                return;
            }
            if (ignoreReadme) {
                extraIgnoreDirs.add("README*.md");
            }

            Path gitignorePath = directory.resolve(StringUtils.firstNonBlank(gitignoreFile, ".gitignore"));
            ProjectFilePrinter printer = new ProjectFilePrinter(gitignorePath, directory, extraIgnoreDirs);
            printer.printFileTreeAndContents();
        } catch (IOException e) {
            System.err.println("Error reading files: " + e.getMessage());
        }
    }
}
```

