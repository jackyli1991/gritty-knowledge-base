## oh-my-zsh

Zsh配置管理框架。

```Shell
brew install zsh # 安装

cd ~/.oh-my-zsh # 目录

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting # 下载插件

vim ~/.zshrc # 配置文件
ZSH_THEME="powerlevel10k/powerlevel10k" # 修改主题
plugins=(git zsh-syntax-highlighting) # 添加插件

source ~/.zshrc # 重启
```


## brew

mac包管理器。

``` Shell
brew install [--cask] [formula]
brew uninstall [formula]
brew list
brew search [formula]
brew info [formula]
brew outdated
brew upgrade

brew doctor
brew cleanup

brew services list
brew services start <服务名>
brew services stop <服务名>
brew services restart <服务名>
brew services cleanup
```

#### language

```Shell
# vim ～/.zshrc
alias git='LANG=en_US.UTF-8 git' # english
alias git='LANG=zh_CN.UTF-8 git' # chinese
```
