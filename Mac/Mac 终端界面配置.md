# Mac 终端界面配置

### 安装 ohmyzsh

```sh
## github安装
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
## gitee国内进行安装【推荐】
sh -c "$(curl -fsSL https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh)"
```



### 安装 zsh-autosuggestions

1. Install command:

   ```sh
   brew install zsh-autosuggestions
   ```

2. To activate the autosuggestions, add the following at the end of your .zshrc:

   ```sh
   source $(brew --prefix)/share/zsh-autosuggestions/zsh-autosuggestions.zsh
   ```

3. Start a new terminal session.



### 修改 .zshrc 文件

```sh
# 禁用自动更新提示
DISABLE_AUTO_UPDATE="true"
DISABLE_UPDATE_PROMPT="true"

# 导入 .bash_profile 配置
if [ -f ~/.bash_profile ]; then
    source ~/.bash_profile
fi

```

