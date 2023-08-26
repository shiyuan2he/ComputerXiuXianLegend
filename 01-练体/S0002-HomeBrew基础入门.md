# 零、homebrew
Homebrew 是一个自由开源的软件包管理系统，主要设计给 Apple Mac 电脑的操作系统 macOS 使用，但也支持 Linux 系统。它可以快速简洁的安装、卸载以及管理计算机软件包。

Homebrew 的一个重要特点是其包含了一些 Mac 预装软件缺失的 GNU 工具，如：bash, git, wget, curl 等。

并且其自身的安装和使用都非常简单，并且软件包的安装是独立的，互不影响，这也避免了因为依赖的问题导致的软件包卸载困难的情况。

# 一、检测
## 1.1 查看当前版本
> brew -v

输出如下，表示已经安装
```shell
Homebrew 4.0.28
Homebrew/homebrew-core (git revision efc626a3fe3; last commit 2023-07-18)
```

# 二、卸载

## 2.1 方式一：官方卸载

> /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall.sh)"

这是 Homebrew 官方提供的卸载脚本，非常方便且安全。

## 2.2 方式二：手动卸载
```shell
cd brew –prefix
brew prunerm git ls-files
rm -r /usr/local/Homebrew
rm -rf .gitrm -rf ~/Library/Caches/Homebrew
rm -rf /usr/local/opt
rm -rf /usr/local/Caskroom
rm -rf /usr/local/var/homebrew
```
本人未曾尝试过，不推荐使用。

# 三、安装
进入官网，直接找到如下命令行。

> /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

# 四、更换
## 4.1 更换brew源
### 4.1.1 什么是brew源？都有哪些源？

1. 官方源 Homebrew/core（已更名为 homebrew-core）

    这是默认的 Homebrew 源。 它是由 Homebrew 维护团队维护的，应用程序包的更新速度非常快，几乎可以满足日常生产使用。但如果在国内，可能会遇到网络问题，速度慢。

2. 官方 bottles 源

    这是 Homebrew 二进制预编译包的源。一些常用的包 Homebrew 会进行预编译，在需要的时候进行下载。
3. 清华大学开源软件镜像站

    清华大学开源软件镜像站提供了 Homebrew/core 的镜像，更新速度很快，国内用户可以使用此镜像提高 brew 更新的速度。
4. 中科大源

    中科大也提供了 Homebrew/core 的源，其特点也是更新速度快，网络稳定，是另一国内用户的良好选择。

### 4.1.2为什么要更换？

主观：使用brew install 安装软件的时候，巨慢无比，程序员无法忍受如此之慢！

客观：默认官方的更新源都是存放在GitHub上的，这也是中国大陆用户访问缓慢的原因，一般来说我们会更倾向选择国内提供的更新源，在此推荐中国科大以及清华大学提供的更新源

### 4.1.3 如何更换？

查看自己的源：
> cd "$(brew --repo)"
> git remote -v

官方源更新：
> brew update

清华大学开源软件镜像站:

```shell
cd "$(brew --repo)"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git
```

中科大源:

```shell
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git

cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```


# 五、复原

```shell
# 重置 brew.git:
cd "$(brew --repo)"
git remote set-url origin https://github.com/Homebrew/brew.git

# 重置 homebrew-core.git:
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://github.com/Homebrew/homebrew-core.git

# 重置 homebrew-cask.git （如果你使用的是 cask 插件的话）
cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
git remote set-url origin https://github.com/Homebrew/homebrew-cask.git

# 更新 Homebrew
brew update
```

# 六、基本命令
 | 命令 | 备注 |
 | -- | -- | 
 brew install软件名 |安装软件
 brew search 软件名 | 搜索软件
 brew uninstall 软件名 | 卸载软件
 brew update | 更新所有软件
 brew upgrade 软件名 | 更新具体软件
 brew list | 显示已安装软件 
 brew info/home 软件名 | 查看软件信息
 brew outdated | 查看软件信息查看哪些已安装的程序需要更新
 brew reps | 显示包依赖
 brew help | 显示帮助
 brew services list | 查询服务列表
 brew cleanup -n | 列出需要清理的内容
 brew cleanup | 清理所有的过时软件
 brew cleanup xx | 清理指定软件的过时包
 brew config | 用于查看brew所在环境及相关的配置情况
 brew doctor | 诊断当前brew存在哪些问题，并给出解决方案
