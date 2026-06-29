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
```Zsh
brew install [--cask]  [formula]

```

