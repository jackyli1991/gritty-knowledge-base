## oh-my-zsh

Zsh配置管理框架。

```Zsh
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

```Zsh
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


## git

#### SSH-Key

```Zsh
ssh-keygen -t rsa -C '2008042226@163.com' # 生成公钥和私钥

cd ~/.ssh # 存放目录
cat id_rsa.pub # 复制公钥，添加到https://github.com/settings/keys

ssh -T git@github.com # 验证
```

#### language

```Zsh
# vim ～/.zshrc
alias git='LANG=en_US.UTF-8 git' # english
alias git='LANG=zh_CN.UTF-8 git' # chinese
```
