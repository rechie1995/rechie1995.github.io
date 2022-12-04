# 如何禁止使用ping命令

通过下面的命令来屏蔽主机的ping命令，使别人无法ping你的机器

```bash
echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_all
```

要想重新允许，则将1变为0即可：

```bash
echo 0 > /proc/sys/net/ipv4/icmp_echo_ignore_all
```
