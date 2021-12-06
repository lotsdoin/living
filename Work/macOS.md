# macOS 知识点


- [开启索引](#开启索引)
- [打开软件显示软件已破损](#打开软件显示软件已破损)
- [常用命令](#常用命令)
- [pyenv 安装本地版本](#pyenv 安装本地版本)
- [macOS 进入名称带空格的目录](#macOS 进入名称带空格的目录)
- [macOS 环境下写 C 程序经常找不到头文件](#macOS 环境下写 C 程序经常找不到头文件)
- [解决 cman 乱码问题](#解决 cman 乱码问题)
- [强制关闭软件](#强制关闭软件)

## 开启索引
```bash
sudo mdutil -a -i on
```
## 打开软件显示软件已破损
打开终端输入以下信息，记录去掉【】括号
【xattr -r -d com.apple.quarantine 直接把APP拖进来】注意quarantine后有空格
【codesign -f -s - --deep 直接把APP拖进来】注意deep后有空格

## 常用命令
```bash
brew services start redis

```

## pyenv 安装本地版本
最近在用pyenv安装python的时候发现官网特别慢，经常出现拒绝访问的情况。看了一些解决方法，发现可以使用本地的python源码进行安装，让pyenv从本地下载就可以了~步骤如下：

* 首先从官网下载要安装的python源码：https://www.python.org/ftp/python/3.5.2/Python-3.5.2.tar.xz，我下载后放到了~/Downloads/下,
* cp Python-3.5.2.tar.xz ~/Downloads/
* 然后在~/Downloads下启动一个简单的httpserver
* cd ~/Downloads/ 
* python -m SimpleHTTPServer 8000
* 在执行pyenv install 3.5.2之前要先添加一个环境变量export PYTHON_BUILD_MIRROR_URL="http://127.0.0.1:8000/"
* export PYTHON_BUILD_MIRROR_URL="http://127.0.0.1:8000/"
* pyenv install 3.5.2
* 但是从http的log中发现收到的请求是一个字符串"HEAD /0010f56100b9b74259ebcd5d4b295a32324b58b517403a10d1a2aa7cb22bca40 HTTP/1.1",我们要把Python-3.5.2.tar.xz复制一份到这个字符串为名的文件,然后重启httpserver，最后用pyenv即可安装
* cp Python-3.5.2.tar.xz 0010f56100b9b74259ebcd5d4b295a32324b58b517403a10d1a2aa7cb22bca40
* python -m SimpleHTTPServer 8000
* pyenv install 3.5.2
　　
## macOS 进入名称带空格的目录
```sh
# 进入目录
cd /Applications/Trial' 'Reset.app/Contents/MacOS/
cd /Applications/Trial" "Reset.app/Contents/MacOS/
cd /Applications/Trial\ Reset.app/Contents/MacOS/
# 执行程序
sudo /Applications/Trial' 'Reset.app/Contents/MacOS/ParagonNTFSReset
sudo /Applications/Trial" " Reset.app/Contents/MacOS/ParagonNTFSReset
sudo /Applications/Trial\ Reset.app/Contents/MacOS/ParagonNTFSReset
```

## macOS 环境下写 C 程序经常找不到头文件
因为一般 brew 都会安装程序到 `/usr/local/Cellar`目录下，需要建立软连接，即
在【/usr/local/include】目录建立openssl的目录软连接 ：openssl -> ../Cellar/openssl/1.0.2q/include/openssl
在【/usr/local/lib】目录建立libssl.dylib和libcrypto.dylib的两个文件软连接 ：
libcrypto.dylib -> ../Cellar/openssl/1.0.2q/lib/libcrypto.1.0.0.dylib
libssl.dylib -> ../Cellar/openssl/1.0.2q/lib/libssl.1.0.0.dylib

## 解决 cman 乱码问题
[URL](https://github.com/man-pages-zh/manpages-zh/issues/3)
1. install `groff`
    brew install groff
2. write `/etc/man.conf`, add follow commands:
    `NROFF preconv -e UTF8 | /usr/local/bin/nroff -Tutf8 -mandoc -c`

## 强制关闭软件
option+command+esc打开强制退出应用程序窗口

## ranger 命令行文件管理器
`ranger ` 查看即可。
