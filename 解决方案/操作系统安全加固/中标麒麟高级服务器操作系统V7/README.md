# 中标麒麟高级服务器操作系统 V7 安全加固参考

## 一、密码复杂度设置

在中标V7中，使用了pam_pwquality模块取代过去的pam_cracklib模块，用于设置密码复杂度。

我们可以通过命令`authconfig`来对密码复杂度进行修改。或者直接修改`/etc/security/pwquality.conf`配置文件内容。

## 二、登录尝试限制

通过pam_tally2.so模块可以实现用户多次输入错误密码后锁定当前登录用户，从而避免暴力破解用户密码。通常安全厂商的软件会要求在`/etc/pam.d/system-auth`配置文件中设置下面参数：

```bash
auth    reuqired    pam_tally2.so   deny=5  onerr=fail  even_deny_root unlook_time=180
```

- **deny** 参数设置允许重试次数，连续验证错误超过重试次数时，该登录用户被锁定。
- **onerr** 参数设置遇到意外时反馈PAM错误代码。
- **even_deny_root** 参数设置root用户认证时同样进行统计。
- **unlock_time** 参数设定被锁定用户解锁时间，单位为秒。

如果希望对SSH等服务生效，您还需要将上面配置内容写入`/etc/pam.d/password-auth`文件中。

## 三、开启系统审计

在中标麒麟V7中，默认已经设置开启auditd.service服务，只是并未创建相关的审计规则（默认审计内容与用户登录相关），这个需要根据用户的实际应用情况进行相关的设置操作。

##### 1. 创建审计规则

例如我们要创建一个用于审计用户是否修改`/etc/passwd`文件的规则，可以这样操作:

```bash
auditctl -w /etc/passwd -p wa -k passwd_change
```

其中参数意义如下：

- -w 后面是需要监控的文件或目录路径
- -p 设置了审计内容，我们目标是监控这个文件是否被修改内容或权限
- -k 代表该规则的关键字，可以方便我们在查询报告信息的时候，了解触发的是什么规则。

设置完成后，我们可以通过命令 `auditctl -l` 命令查询当前系统中识别到的审计规则。

##### 2. 设置永久性规则

这种设置的规则都是临时性的，如果需要永久性保存规则，需要把规则添加到`/etc/audit/rules.d/audit.rules`配置文件中。

##### 3. 查看审计结果

我们可以通过命令`aureport`命令来查询系统的审计结构，例如我们根据关键字查询审计情况可以直接输入`aureport -k`命令。

如果我们需要查看详细的审计日志记录，则可以使用`ausearch`命令进行查询，例如我们查询关键字passwd相关的信息可以执行`ausearch -k passwd`命令

##### 4. 删除审计规则

删除审计结果的操作只需要修改创建审计规则的参数，将-w修改为-W即可，例如删除之前创建的审计规则命令如下：

```bash
auditctl -W /etc/passwd -p wa -k passwd_change
```

## 四、设置自动超时

系统登录后超时自动退出可以通过在/etc/profile.d文件夹中创建一个配置文件用于设置TMOUT变量来实现，具体命令如下：

```bash
echo "export TMOUT=300" > /etc/profile.d/tmout.sh
```

需要注意，该设置完成后，需要注销重新登录或重启操作系统才能生效。

## 五、限制root用户直接登录

为了增强系统的安全稳定性，我们通常建议通过SSH连接到服务器上时，限制root用户直接登录，这样可以有效的防范针对系统用户的字典密码暴力破解。

限制root用户直接登录需要修改OpenSSH服务的配置文件，`/etc/ssh/sshd_config`，找到该配置中的关键字PermitRootLogin，将该参数设置为no。默认情况下配置文件中该参数处于注释状态，需要手动取消注释并把注释中的yes替换为no，然后重启sshd服务使配置文件生效，可以通过命令`systemctl restart sshd.service` 命令进行重启操作。
