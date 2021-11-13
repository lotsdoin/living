# Linux 知识点

- [网络](#网络)
- [搭建 VPS 梯](#搭建 VPS 梯)
- [修复 Linux 字体很挫的方法](#修复 Linux 字体很挫的方法)
- [配置 ubuntu 系统](#配置 ubuntu 系统)
- [Linux 添加环境变量](#Linux 添加环境变量)
- [ubuntu 更新 gcc g++](#ubuntu 更新 gcc g++)
- [java](#java)
- [compile vim](#compile vim)
- [vim in CentOS](#vim in CentOS)
- [show the configdir of python3](#show the configdir of python3)
- [Ubuntu 18.04.1 虚拟机开机卡在“starting Gnome Display Manager” 的解决方法](#Ubuntu 18.04.1 虚拟机开机卡在“starting Gnome Display Manager” 的解决方法)
- [Ubuntu 18.04.1 虚拟机开机卡在 “Started Hold until boot procss finishes up”](#Ubuntu 18.04.1 虚拟机开机卡在 “Started Hold until boot procss finishes up”)
- [Virtualbox linux 挂载共享文件夹](#Virtualbox linux 挂载共享文件夹)

## 网络

```shell
# 查看开启了哪些端口
netstat -tlpn
# 查看某个端口是否开启
lsof -i :10666
```
## 搭建 VPS 梯

* 通过 ssh 登录到 VPS 中，`ssh root@199.xxx.231.19`,如果之前有免密登陆过次VPS，则先到 .ssh 目录下
将此 IP 信息删除再登录
* 安装 zsh, Oh-my-zsh
```sh
# 查看已有 shell
cat /etc/shells
# install zsh
apt-get install zsh -y
# install oh-my-zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
# install git and curl
apt-get install git && apt-get install curl -y
```
* 安装 vim
```sh
git clone https://github.com/vim/vim.git
apt-get install libncurses5-dev
cd vim
./configure
make
make install 

```
* scp -p ~/.ssh/id_rsa.pub root@<ip>:/root/.ssh/authorized_keys
* scp  -P 29503 ~/.vim.zip  root@199.115.231.19:/root/
* scp -P  29503 root@199.115.231.19:/root/ubuntu_install_ssr.sh  /Users/lotsd/lotsd

```text
 ssr运行状态：正在运行
 ssr配置文件：/etc/shadowsocksR.json

 ssr配置信息：
   IP(address):  199.115.231.19
   端口(port)：10666
   密码(password)：luoshuiwu7
   加密方式(method)： aes-256-cfb
   协议(protocol)： origin
   混淆(obfuscation)： plain

 ssr链接: ssr://MTk5LjExNS4yMzEuMTk6MTA2NjY6b3JpZ2luOmFlcy0yNTYtY2ZiOnBsYWluOmJIVnZjMmgxYVhkMU53Lz9yZW1hcmtzPSZwcm90b3BhcmFtPSZvYmZzcGFyYW09
/proc/self/fd/11: line 412: qrencode: command not found

 为使BBR模块生效，系统将在30秒后重启
scp -P  29503 root@199.115.231.19:/root/ubuntu_install_ssr.sh  /Users/lotsd/lotsd
```
## 修复 Linux 字体很挫的方法

```bash
sudo vim /etc/profile.d/java_options.sh

#!/bin/bash
opts=" -Dswing.aatext=true  -Dawt.useSystemAAFontSettings=lcd -Djava.net.useSystemProxies=true "
export _JAVA_OPTIONS="`echo ${_JAVA_OPTIONS} |sed -Ee 's/-Dawt.useSystemAAFontSettings=\w+//ig'` $opts"
```

## 配置 ubuntu 系统

* 换源
```txt
# vi /etc/apt/sources.list
#添加阿里源
deb http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ focal-backports main restricted universe multiverse
#添加清华源
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-updates main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-backports main restricted universe multiverse
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse
# deb-src https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ focal-security main restricted universe multiverse multiverse
```
* sudo apt-get update && apt-get upgrade
* 安装 zsh && oh-my-zsh
`chsh -s /bin/zsh`
```bash
# install ag 
sudo apt-get install silversearcher-ag

# safe-rm
git clone git@github.com:kaelzhang/shell-safe-rm.git
sudo bash shell-safe-rm/install.sh


sudo apt-get install zsh -y
# install curl
sudo apt-get install curl -y
# install git
sudo apt-get install git -y
# oh-my-zsh
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
或
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"

# antigen 管理 zsh 插件的插件
curl -L git.io/antigen > .antigen.zsh

# git config
 sudo apt-get install git
 git config --global user.name "lotsdoin"
 git config --global user.email "lotsdoin@gmail.com"
 ssh-keygen -t rsa 
 ssh -T git@github.com # check it

# gcc 
 sudo apt-get install gcc

# make
 sudo apt-get install make

# uname -a 查看使用内核
# dpkg --get-selections | grep linux-image

# 禁止内核更新
sudo apt-mark hold linux-image-5.3.0-42-generic
sudo apt-mark hold linux-image-extra-5.3.0-42-generic

# 重启内核更新
sudo apt-mark unhold linux-image-5.3.0-42-generic
sudo apt-mark unhold linux-image-extra-5.3.0-42-generic

# 美化
sudo apt install gnome-tweak-tool 
4.1 安装搜狗输入法
卸载 ibus（可选）
 $ sudo apt remove 'ibus*'

安装Fcitx输入框架
 $ sudo apt install fcitx

到官网下载搜狗输入安装包
 地址：https://pinyin.sogou.com/linux/

安装搜狗输入法：
 $ sudo dpkg -i sogoupinyin_2.2.0.0108_amd64.deb

如果遇到问题，执行如下命令
 $ sudo apt --fix-broken install
```

* 命令高亮和补全
```bash

git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
git clone git@github.com:zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
# edit ~/.zshrc


```
ubuntu如何查看版本信息？
方法1：使用命令： cat /proc/version 查看
方法2：使用命令： uname -a 查看
方法3：使用命令： lsb_release -a 查看

## Linux 添加环境变量
1. echo $PATH
edit the `/etc/profile` make all users use it..

2.添加临时环境变量
export PATH=/usr/local/bin:$PATH
// PATH是变量名，这里是指添加到PATH这个环境变量中
// =后面是要添加的环境变量
// :$PATH是指把新添加的环境变量与原先的环境变量重新赋值给PATH这个变量，这里可以看出如果有多个环境变量时，应该使用:进行分隔，如
// export PATH=/usr/local/php/bin:/usr/local/mysql/bin:$PATH
// 当然$PATH是放在开头还是最后是没有影响的

这种方法添加的环境变量会立即生效，但是在窗口关闭后便会失效

3.添加全局环境变量
vim /etc/profile
// 如果只修改当前用户的环境变量，则是`vim ~/.bashrc`
// 在文件的最后一行添加以下代码：
export PATH=$PATH:/usr/local/php/bin
// 规则和用法如第二条所说

## ubuntu 更新 gcc g++
1.添加源

sudo add-apt-repository ppa:ubuntu-toolchain-r/test  
2.更新升级信息

sudo apt-get update  

3.升级到你所需要的版本，例如

sudo apt-get install gcc-9 g++-9  
cd /usr/bin  
ls -l gcc*  

sudo rm gcc  
sudo ln -s /usr/bin/gcc-9 gcc  
sudo ln -s /usr/bin/g++-9 g++  

## java
 sudo apt install default-jdk

* install oracle java
$ sudo add-apt-repository ppa:webupd8team/java
sudo apt install oracle-java8-installer

package golang.org/x/tools/gopls@v0.6.4: cannot find package "golang.org/x/tools/gopls@v0.6.4" in any of:
	/usr/lib/go-1.10/src/golang.org/x/tools/gopls@v0.6.4 (from $GOROOT)
	/root/.vim/plugged/youcompleteme/third_party/ycmd/third_party/go/src/golang.org/x/tools/gopls@v0.6.4 (from $GOPATH)

## compile vim

```sh
./configure --with-features=huge --enable-multibyte --enable-luainterp --enable-rubyinterp --enable-pythoninterp --enable-python3interp --enable-perlinterp --enable-cscope --enable-tclinterp --enable-gui=gtk3 --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu --with-python3-config-dir=/usr/lib/python3.6/config-3.6m-x86_64-linux-gnu --with-x --with-tlib=ncurses --with-gnome
```
`configure` 出现
```text

configure: error: `LDFLAGS' was set to `-L/usr/local/lib -Wl,--as-needed' in the previous run
configure: error: `CPPFLAGS' was set to `' in the previous run
configure: error: in `/home/lotsd/github/vim/src':
configure: error: changes in the environment can compromise the build
configure: error: run `make distclean' and/or `rm auto/config.cache' and start over
```
报错, `make distclean` 解决

make && make install 

## vim in CentOS
作者：刘遄
链接：https://zhuanlan.zhihu.com/p/142358765
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。

[root@localhost vim-master]# ./configure --with-features=huge \
            --enable-rubyinterp=yes \
            --enable-luainterp=yes \
            --enable-perlinterp=yes \
            --enable-python3interp=yes \
            --enable-pythoninterp=yes \
            --with-python-config-dir=/usr/lib64/python2.7/config \
            --with-python3-config-dir=/usr/lib64/python3.6/config-3.6m-x86_64-linux-gnu \
            --enable-fontset=yes \
            --enable-cscope=yes \
            --enable-multibyte \
            --disable-gui \
            --enable-fail-if-missing \
            --prefix=/usr/local \
            --with-compiledby='Professional operations'
[root@localhost vim-master]# make VIMRUNTIMEDIR=/usr/local/share/vim/vim82 && make install--enable-fail-if-missing 表示问题会提示报错，并停止--enable-***interp=yes 表示加入***支持--with-***-config-dir=*** 表示指定配置文件路径make VIMRUNTIMEDIR=*** 表示指定VIM可执行文件的位置执行vim查看一下版本

## show the configdir of python3

```bash
 echo $(python3-config --configdir)
```

## Ubuntu 18.04.1 虚拟机开机卡在“starting Gnome Display Manager” 的解决方法
按alt+ctrl+F1~F6，输入用户名和密码（具体是几取决于版本）
输入：
df -h // 检查磁盘空间
会发现：文件系统 /dev/loopx 已用% 挂载点已100%
文件系统        容量  已用  可用 已用% 挂载点
udev             32G     0   32G    0% /dev
tmpfs           6.3G  2.0M  6.3G    1% /run
/dev/sda1       469G   12G  434G    3% /
tmpfs            32G     0   32G    0% /dev/shm
tmpfs           5.0M  4.0K  5.0M    1% /run/lock
tmpfs            32G     0   32G    0% /sys/fs/cgroup
/dev/loop0       13M   13M     0  100% /snap/gnome-characters/139
/dev/loop1       15M   15M     0  100% /snap/gnome-logs/45
/dev/loop2      141M  141M     0  100% /snap/gnome-3-26-1604/74
/dev/loop3       35M   35M     0  100% /snap/gtk-common-themes/818
/dev/loop4      2.3M  2.3M     0  100% /snap/gnome-calculator/260
/dev/loop5       91M   91M     0  100% /snap/core/6350
/dev/loop6      3.8M  3.8M     0  100% /snap/gnome-system-monitor/57
/dev/sdb        1.8T   77M  1.7T    1% /home/data
tmpfs           6.3G     0  6.3G    0% /run/user/1000
tmpfs           6.3G  4.0K  6.3G    1% /run/user/121

sudo apt autoremove --purge snapd //清理磁盘空间

不行的话, sudo apt-get install gnome

## Ubuntu 18.04.1 虚拟机开机卡在 “Started Hold until boot procss finishes up”
启动 ubuntu 时，磁盘空间不足。
如果有些人的设定了不会有进入到菜单menu的过程，那怎么进入到Advanced options for Ubuntu（中文版：Ubuntu 高级选项）呢？在启动的刚开始就要一直按shift键直到进入GNU GRUB菜单即可，如下图：（不行多试几遍哈，可能是按的时机不对，记住哦，是一直按着不放哦，直到进入菜单）

## Ubuntu 18.04.1 遇到的问题原因
因为使用的虚拟机系统是安装在 U 盘上使用的，使用过程中总是接触不良，导致问题很多，所以移动到电脑上。
`VBoxManage clonevdi /Volumes/M1/VMs/ubuntu/ubuntu.vdi ~/VirtualBox\ VMs/ubuntu.vdi`
或者 shift 进入 recovery mode,dpkg 选项修复 packages, reboot

## Virtualbox linux 挂载共享文件夹

```bash
sudo mount -t xboxsf share_folder mount_point
 sudo mount -t vboxsf lotsd ./share
```

## shell 

* 查找项目所用到的头文件
`find . -name ".[ch]" | xargs grep "#include" | sort | uniq`
