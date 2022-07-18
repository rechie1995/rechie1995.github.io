# Git

## Git 是什么？

Git是 Linus Torvalds 为了帮助管理 Linux 内核开发而开发的一个开放源码的分布式版本控制系统。

与常用的版本控制工具CVS，Subversion等不同，它采用了分布式版本库的方式，不必服务器端软件支持，使源代码的发布和交流极其方便。Git的速度很快，这对于诸如Linux Kernel 这样的大项目来说自然很重要。Git最为出色的是它的合并跟踪能力。

## Git 的安装

```bash
sudo apt install git
```

## 初次运行 Git 前的配置

在新的系统上，我们一般都需要先配置下自己的Git工作环境。配置工作只需一次，以后升级时还会沿用现在的配置。当然，如果需要，你随时可以使用相同的命令修改已有的配置。

Git 提供了一个叫做`git config`的工具，专门用来配置或读取相应的工作环境变量。而正是由这些环境变量，决定了Git在各个环节的具体工作方式和行为。这些变量可以存放在以下三个不同的地方：

> - `/etc/gitconfig`文件: 系统中对所有用户都普遍适用的配置。若使用`git config`时用`--system`选项，读写的就是这个文件。
> - `~/.gitconfig`文件: 用户目录下的配置文件只适用于该用户。若使用`git config`时用`--global`选项，读写的就是这个文件。
> - 当前仓库的git目录中的配置文件(也就是工作目录中的`.git/config`文件): 这里的配置仅仅针对当前仓库有效。每一个级别的配置都会覆盖上层的相同配置，所以`.git/config`里的配置会覆盖`/etc/gitconfig`中的同名变量。

### 用户信息配置

第一个要配置的是你个人的用户名称和电子邮件地址。

这两条配置很重要，每次Git提交时都会引用这两条信息，说明是谁提交了更新，所以会随更新内容一起被永久纳入历史记录:

```bash
git config --global user.name "rechie"
git config --global user.name "502117806@qq.com"
```

### 文本编辑器配置

```bash
git config --global core.editor vim
```

### 差异分析工具

```bash
git config --global merge.tool vimdiff
```

### 查看配置信息

```bash
git config --list
```
