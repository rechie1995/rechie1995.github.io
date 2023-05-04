# 如何制作系统启动盘

## 如何获取镜像文件

### 银河麒麟

- 通过官网申请试用
- 通过技术服务人员申请试用

## 如何获取系统启动盘制作工具

- [Ventoy](https://www.ventoy.net/cn/index.html)
- [Rufus](http://rufus.ie/zh/)
- [UltraISO](https://cn.ultraiso.net/)
- [dd](https://www.gnu.org/software/coreutils/manual/html_node/dd-invocation.html#dd-invocation)

## Ubuntu下如何制作系统启动盘

1、找到U盘

`sudo fdisk -l`

2、卸载U盘

`sudo umount /dev/sdb1`

3、 格式化U盘

`sudo mkfs.vfat /dev/sdb -I`

4、制作启动盘

`sudo dd if=Kylin-Desktop-V10-SP1-Release-hwe-2107-x86_64.iso of=/dev/sdb status=progress`
