# apt (Linux软件包管理工具)

apt 是一个在Debian、Ubuntu和银河麒麟桌面操作系统中的Shell前端软件包管理器
apt 命令提供了查找、安装、升级、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。
apt 命令执行需要root权限。

## apt 常用命令

- apt update 列出所有可更新的软件清单
- apt upgrade 升级软件包
- apt full-upgrade 升级软件包，升级前先删除需要更新软件包
- apt install <package_name> 安装指定的软件包
- apt install <package_name1> <package_name2> <package_name3> 安装多个指定的软件包
- apt show <package_name> 显示软件包具体信息，例如：版本号，安装大小，依赖关系等
- apt remove <package_name> 删除软件包
- apt autoremove 清除不再使用的依赖和库文件
- apt purge <package_name> 移除软件包及配置文件
- apt search <keyword> 查询软件包
- apt list --installed 列出所有已经安装的软件包
- apt list --upgradeable 列出所有可更新的软件包及版本信息
- apt list --all-versions 列出所有已安装的包的版本信息