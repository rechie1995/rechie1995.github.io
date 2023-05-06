# 如何安装谷歌Chrome浏览器

## 适用版本

- Kylin-Desktop-V10-SP1-General-Release-2203-X86_64

## 资源包获取（图形化）

1. 访问谷歌中文网站：[Google Chrome 网络浏览器](https://www.google.cn/intl/zh-CN/chrome/)
![谷歌中文网站](docs/res/Pasted%20image%2020230505221643.png)
2. 点击`下载Chrome`按键，在弹出的页面选择`64位.deb`，点击接受并安装
![选择Linux版本](docs/res/Pasted%20image%2020230505221915.png)
3. 在弹出的页面选择`保存`
![下载文件](docs/res/Pasted%20image%2020230505222159.png)
## 资源包获取（命令行）

```bash
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
```
## 安装

### 命令行安装

```bash
# 安装依赖
sudo apt install libu2f-udev
# 安装Chrome
sudo dpkg -i google-chrome-stable_current_amd64.deb
```