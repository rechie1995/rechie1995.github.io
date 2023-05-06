# 如何创建LVM

## 创建分区并创建PV

在虚拟机上挂载一块新的磁盘，使用`fdisk`工具或者其他硬盘工具给磁盘分区

在分区上创建物理卷

```bash
pvcreate /dev/sdb1
```

## 创建VG

创建卷组，并将刚刚创建的pv加入到vg中来

```bash
vgcreate [卷组名称] /dev/sdb1
```

## 创建LV

创建逻辑卷（LV）

```bash
lvcreate -l +100%free -n (LV_name) [卷组名称（vg_name）]
```

## 给LV创建文件系统

给刚刚创建的逻辑卷（LV）创建文件系统

```bash
mkfs.xfs /dev/mapper/vg_name-LV_name
```

## 挂载并使用

给`LV`创建挂载点`/data`并将`LV`挂载到挂载点上，并且开机自动挂载
```bash
mkdir /data
mount /dev/mapper/vg_name-LV_name /data
echo "/dev/mapper/vg_name-LV_name /data xfs default 0 0" >> /etc/fstab
```

## 全过程脚本

```bash
#!/bin/bash

function set_lvm(){
	pvcreate /dev/sdb1
	vgcreate datavg /dev/sdb1
	lvcreaete -l +100%free -n datalv datavg
	mkfs.xfs /dev/mapper/datavg-datalv
	mkdir /data
	mount /dev/mapper/datavg-datalv /data
	echo "/dev/mapperdatavg-datalv /data xfs default 0 0" >> /etc/fstab
}
set_lvm
```