# macOS 系统的一些设置

Homebrew 设置镜像，这里用了中科大的镜像

```bash
# 替换各个源
git -C "$(brew --repo)" remote set-url origin https://mirrors.ustc.edu.cn/brew.git
git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
git -C "$(brew --repo homebrew/cask)" remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git

# zsh 替换 brew bintray 镜像
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc
source ~/.zshrc

# bash 替换 brew bintray 镜像
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
source ~/.bash_profile

# 刷新源
brew update
```

重置官方源

```bash
# 重置 brew.git 为官方源
git -C "$(brew --repo)" remote set-url origin https://github.com/Homebrew/brew.git
git -C "$(brew --repo homebrew/core)" remote set-url origin https://github.com/Homebrew/homebrew-core.git
git -C "$(brew --repo homebrew/cask)" remote set-url origin https://github.com/Homebrew/homebrew-cask

# zsh 注释掉 HOMEBREW_BOTTLE_DOMAIN 配置
vim ~/.zshrc
# export HOMEBREW_BOTTLE_DOMAIN=xxx

# bash 注释掉 HOMEBREW_BOTTLE_DOMAIN 配置
vim ~/.bash_profile
# export HOMEBREW_BOTTLE_DOMAIN=xxxxxxxxx

# 刷新源
brew update
```

快捷的代理设置
> 这里主要是配合 brew 使用，虽然使用了镜像，但是很多时候还是会从 github 拉取数据；新版的 macOS brew 里没有 proxychains 之类的东西了

```bash
vim ~/.zshrc

alias proxy='export all_proxy=socks5://127.0.0.1:1080'
alias unproxy='unset all_proxy'
```

如何使用：在使用 `brew` 命令前先执行 `proxy` 命令，使用完在执行 `unproxy`
