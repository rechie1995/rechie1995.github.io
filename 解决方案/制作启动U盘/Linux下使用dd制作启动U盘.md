# Linux下使用dd制作启动U盘

1、  找到U盘

`sudo fdisk -l`

2、卸载U盘

`sudo umount /dev/sdb1`

3、 格式化U盘

`sudo mkfs.vfat /dev/sdb -I`

4、制作启动盘

`sudo dd if=Kylin-Desktop-V10-SP1-Release-hwe-2107-x86_64.iso of=/dev/sdb status=progress`