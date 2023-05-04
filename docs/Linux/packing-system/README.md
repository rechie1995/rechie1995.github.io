# 包管理系统: 工具和基本原则

曾几何时，软件都是通过 FTP 或邮件列表（即通过邮件列表发布源代码的补丁包）来分发的（最终这些发布方式在互联网的迅猛发展下都演化成为一个个现今常见的软件发布网站）。（一般在一个 tar 文件中）只有一个非常小的文件包含了创建二进制的说明。你需要做的是先解压这个包，然后仔细阅读当中的 README 文件， 然后通过./configure、make、make install进行软件安装。可以想象，为你系统上的每一个软件都执行上述的流程将是多么无聊费时，更不用说如果更新一个已经安装的软件将会多复杂，多么需要精力投入。

软件包(package)这个概念是用来解决在软件安装、升级过程中的复杂性的。包将软件安装升级中需要的多个数据文件合并成一个单独的文件，这将便于传输和（通过压缩文件来）减小存储空间，包中的二进制可执行文件已根据开发者所选择的编译标识预编译。包本身包括了所有需要的元数据，如软件的名字、软件的说明、版本号，以及要运行这个软件所需要的依赖包等等。

不同流派的 Linux 发行版都创造了它们自己的包格式，其中最常用的包格式有：

- .deb：这种包格式由 Debian、Ubuntu、Linux Mint 以及其它的变种使用。这是最早被发明的包类型。
- .rpm：这种包格式最初被称作 红帽包管理器(Red Hat Package Manager)（LCTT 译注： 取自英文的首字母）。使用这种包的 Linux 发行版有 Red Hat、Fedora、SUSE 以及其它一些较小的发行版。
- .tar.xz：这种包格式只是一个软件压缩包而已，这是 Arch Linux 所使用的格式。（LCTT 译注：这种格式无需特别的包管理器，解压即可）

尽管上述的包格式自身并不能直接管理软件的依赖问题，但是它们的出现将 Linux 软件包管理向前推进了一大步。

多年以前，非 Linux 世界的用户是很难理解软件仓库的概念的。甚至今时今日，大多数完全工作在 Windows 下的用户还是习惯于打开浏览器，搜索要安装的软件（或升级包），下载然后安装。但是，智能手机传播了软件商店（AppStore/应用）市场这样一个概念。智能手机用户获取软件的方式和包管理器的工作方式已经非常相近了。些许不同的是，尽管大多数软件商店还在费力美化它的图形界面来吸引用户，大多数 Linux 用户还是愿意使用命令行来安装软件。总而言之，软件仓库是一个中心化的可安装软件列表，上面列举了在当前系统中预先配置好的软件仓库里所有可以安装的软件。

![linux-package-management](res\Linux\packing-system\linux-package-management.png)

在Linux发行版中，几乎每一个发行版都有自己的包管理器。常见的有：

- Debian的dpkg以及它的
  - 前端apt（使用于Debian、Ubuntu）。
- Red Hat的RPM包管理器以及它的
  - 前端dnf（使用于Fedora、 CentOS 8）
  - 前端yum（使用于Red Hat Enterprise Linux、CentOS 7及以下）
  - 前端ZYpp（使用于openSUSE）
  - 前端urpmi（使用于Mandriva Linux、Mageia）
- 其他包管理器有
  - ArchLinux中使用的Pacman
  - Gentoo使用的基于源代码的Portage
  - Mac系统下的Homebrew等

使用包管理器将大大简化在Linux发行版中安装软件的过程。

> [Linux软件包管理系统](https://www.biaodianfu.com/linux-package-management.html)
> [Debian管理员手册-第五章 包管理系统: 工具和基本原则](https://www.debian.org/doc/manuals/debian-handbook/packaging-system.zh-cn.html)
