# IDEA初始化操作

## Maven

![image-20210625213821904](images/image-20210625213821904.png)

**`setting.xml` 配置阿里云镜像**

```xml
<mirror>
	<id>nexus-aliyun</id>
  <mirrorOf>central</mirrorOf>
	<name>Nexus aliyun</name>
	<url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```

![image-20210625212316016](images/image-20210625212316016.png)



## Encodings - 编码

![image-20201209150419802](images/image-20201209150419802.png)

## Indent - 缩进

![image-20201209150658909](images/image-20201209150658909.png)

## Font - 字体

![image-20201209152010881](images/image-20201209152010881.png)

## Theme - 暗黑模式

![image-20201209152043399](images/image-20201209152043399.png)

## Editor Tabs - 靠右展示编辑窗口标签

![image-20210624094633054](images/image-20210624094633054.png)

## Code Completion - 智能提示忽略大小写

![image-20210625145003196](images/image-20210625145003196.png)



## Live Template - 注释模板

- 创建 `Template Group`，自定义 Group 名称

![image-20210625215302007](images/image-20210625215302007.png)

- 在创建的 Group 里面创建 `Live Template`

  - Method

    ```
    /**
     * 
     *
     * @author $author$
     * @since $date$ $time$
     */
    ```

    > $author$  Expression `groovyScript(" _1.contains('Test') ? 'YuHai' : 'Kanshan'", filePath())`

## File and code Templates

- File Header

  ![image-20250422145143486](./images/IDEA%E5%88%9D%E5%A7%8B%E5%8C%96%E6%93%8D%E4%BD%9C/image-20250422145143486.png)

  ```
  /**
   * 
   *  
   * #if ($PACKAGE_NAME.contains("Test"))
  @author Test
  #else
  @author Kanshan
  #end
   * @since ${DATE} ${TIME}
   */
  ```

  

## System Setting - 默认不打开项目

![image-20210628082708516](images/image-20210628082708516.png)


## Auto Import - 导包优化

![image-20210628135742704](images/image-20210628135742704.png)

> - Add unambiguous imports on the fly：快速添加明确的导入
> - Optimize imports on the fly：自动帮助删除无用的导入
## Inspections - 序列化提示

![image-20210701194801837](images/image-20210701194801837.png)



## 自动导包去除星号（import xxx.*）

![image-20210909150957736](images/image-20210909150957736.png)

## Plugins - 插件

- Translation - 翻译
- .ignore - git
- CamelCase - 命名风格转换
- Easy Code - 代码生成
- Free MyBatis plugin - MyBatis Mapper 和 XML 映射和提示
- Maven Helper - Maven 冲突解决
- Mybatis Log - 打印MyBatis日志并自动拼接参数
- RestfulTookit - Controller 请求映射，快捷键：Ctrl + Alt + N
- Lombok - Lombok 编译插件
- Codota - 代码智能提示
- String Manipulation- 字符串处理
- SequenceDiagram - 方法调用时序图
- Rainbow Brackets - 彩虹括号

## VM Options - 参数

```
-Xms1024m
-Xmx2048m
-XX:+UseConcMarkSweepGC
-XX:SoftRefLRUPolicyMSPerMB=50
-ea
-XX:CICompilerCount=2
-Djdk.http.auth.tunneling.disabledSchemes=""
-XX:+HeapDumpOnOutOfMemoryError
-XX:-OmitStackTraceInFastThrow
-Djdk.attach.allowAttachSelf=true
-Dkotlinx.coroutines.debug=off
-Djdk.module.illegalAccess.silent=true
-Dide.no.platform.update=true
-Dsun.io.useCanonCaches=false
-XX:ReservedCodeCacheSize=512m
```

