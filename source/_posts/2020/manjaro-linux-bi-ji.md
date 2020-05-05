---
title: manjaro linux 笔记
categories:
  - 学习笔记
tags:
  - linux
keywords: manjro linux pacman nvidia
top: 'true'
toc: false
date: 2020-05-05 20:45:07
cover:
summary:
password:
mathjax:
---

# 一、什么是Manjaro?
Manjaro是一个基于Arch Linux的对用户友好的操作系统。
它的特点如下：
-	滚动发行：这意味着用户能得到最新的软件，同时Manjaro比Arch Linux要旧一些，更稳定。
-	用户友好：虽然Manjaro基于Arch Linux，但是通过很多努力，使Manjaro比Arch Linux简单很多，比如图形界面的安装向导。如果你之前使用过Ubuntu，那么使用Manjaro完全没有问题。
-	稳定：它不像Arch Linux那么前卫，也不像Ubuntu LTS那么守旧。
-	对硬件的良好的支持：Manjaro会自行根据硬件安装驱动。
-	丰富的软件：丰富的Manjaro源，同时支持AUR。
-	丰富的帮助资料：包括Wiki和forum。
-	多桌面环境： bspwm, Budgie, Cinnamon, Deepin, GNOME, i3, KDE Plasma, LXDE, LXQt, MATE, Xfce
-	最后一点：使用量持续下载排名第一，我们要相信群众的眼光。
作为桌面环境，manjaro有自己的优势，但是桌面系统，linux都不太好用，即便是做开发用
# 二、manjaro下载与安装
安装方式有图形安装和命令行安装，命令行安装更强大。
## 2.1、图形安装(虚拟机下演示XFCE桌面环境)：
2.1.1、下载：
https://manjaro.org/get-manjaro/
国外下载地址可以下载到最新版
国外官方bt下载：https://osdn.net/dl/manjaro/manjaro-xfce-18.0.2-stable-x86_64.iso.torrent
国内清华镜像下载：https://mirrors.tuna.tsinghua.edu.cn/manjaro-cd/
## 2.1.2、安装：
图形化安装方式按照提示安装即可，下面介绍命令行方式
## 2.2、命令行安装
### 2.2.1、下载：
下载Manjaro-architect 版 
https://manjaro.org/get-manjaro/
### 2.2.2、镜像写入U盘
使用usb写入工具https://etcher.io/，把下载的iso镜像文件写入u盘，
- Linux / Mac OS
在命令行中输入`dd bs=4M if=/path/to/manjaro.iso of=/dev/sd[drive letter] status=progress`即可将其烧录至U盘中。
- Windows
使用 Rufus 或者是 ImageWriter For Windows 进行烧录操作，切记要选择 DD 模式，否则会导致引导失败。

### 2.2.3、安装：
实体机设置BIOS使用，使用f12 u盘启动电脑就可以了。
- 检查网络是否通畅：`ping 114.114.114.114`
- 连接Wifi
- 查看wifi设备
- nmcli 连接Wifi `nmcli dev wifi connect <SSID name> password <your password>`
- 安装
	- 使用账号manjaro和密码manjaro登录`sudo pacman-mirrors -c China -i -m rank`选择最近的仓库源安装
- 关闭系统 `shutdown -h now`
然后拔掉U盘
启动系统后通过下面安装中文字体
``` bash
sudo pacman -Syy
sudo pacman -S wqy-bitmapfont wqy-microhei  wqy-zenhei wqy-microhei-lite
```
>参考引用：https://forum.manjaro.org/t/installation-with-manjaro-architect-iso/20429

# 三、初始化配置
## 3.1、配置源
更新就近源，使用网络安装的话，自动就帮你配置好源了。
- 命令行：`sudo pacman-mirrors -c China -i  -m rank`
- 图形操作： 
添加\删除软件--》首选项--》官方软件仓库
## 3.2、增加archlinuxcn源
archlinuxcn源包含一些常用的中文软件，例如：chrome,office

``` bash
echo -e "\n[archlinuxcn]\nSigLevel = TrustAll\nServer = https://mirrors.tuna.tsinghua.edu.cn/archlinuxcn/\$arch\n\n[antergos]\nSigLevel = TrustAll\nServer = https://mirrors.tuna.tsinghua.edu.cn/antergos/\$repo/\$arch\n"|sudo tee -a /etc/pacman.conf
```

添加archlinuxcn源（参考官方建议）

``` bash
echo -e "\n[archlinuxcn]\nSigLevel = Optional TrustedOnly\nInclude = /etc/pacman.d/archlinuxcn\n"|sudo tee -a /etc/pacman.conf
echo -e "\nServer = https://cdn.repo.archlinuxcn.org/\$arch\n"|sudo tee -a /etc/pacman.d/archlinuxcn
sudo pacman -Syy && sudo pacman -S archlinuxcn-keyring

https://github.com/archlinuxcn/repo
```

## 3.3、pacman用法

``` bash
sudo pacman -S package_name                     //安装软件
sudo pacman -R package_name                     //删除软件
sudo pacman -Ss string1 string2 ...                //搜索
sudo pacman -Si vlc                                      //查看包信息
sudo pacman -Sc                                     //清空并且下载新数据
sudo pacman -Syy                                   //刷新缓存
sudo pacman -Syu                                   //更新系统（升级软件包）
也可以通过图形化进行操作。
```

参考：https://wiki.archlinux.org/index.php/Pacman_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)

## 3.4、中文字体
``` bash
sudo pacman -S wqy-bitmapfont wqy-microhei  wqy-zenhei wqy-microhei-lite
更多字体选用：
sudo pacman -S adobe-source-han-sans-cn-fonts adobe-source-han-serif-cn-fonts noto-fonts-cjk  noto-fonts noto-fonts-emoji
```

参考资料：https://wiki.archlinux.org/index.php/Fonts_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)

## 3.5、输入法设置

``` bash
sudo pacman -S fcitx-im fcitx-configtool fcitx-googlepinyin fcitx-sogoupinyin
sudo echo -e "export GTK_IM_MODULE=fcitx\nexport QT_IM_MODULE=fcitx\nexport XMODIFIERS=@im=fcitx">>~/.xprofile

```
重启生效
如果是mint桌面环境，还需要在任务栏添加键盘小程序才能启动中英文切换。

## 3.8、挂载硬盘 
假如我们需要将sdb1硬盘挂载到/data
df 命令查看需要挂载的磁盘名称，本例中是sdb1
`$ sudo df -l`
mkdir命令创建一个文件夹，即挂载点，本例中挂载到根目录的/data文件夹
`$ sudo mkdir /data`
将sdb1硬盘挂载到/data
`$ sudo mount -w /dev/sdb1 /data`
实现系统启动后自动挂载该分区
$ sudo vim /etc/fstab 在/etc/fstab最后一行添加以下内容： 
`/dev/sdb1 /data ext4 defaults 1 2`


# 四、manjaro应用
proxychains-ng：命令行代理
`sudo vim /etc/proxychains.conf`
文件末尾添加：
`socks5 127.0.0.1 1080`
然后，大多数的终端软件就可以上网了，例如：
`proxychains curl www.google.com`
`shadowsocks-qt5：s5代理`

配置virtualbox
安装VirtualBox
提示：安装VirtualBox时，您需要知道正在运行的内核版本。要获取此信息，请在终端中输入命令uname -r。

要安装VirtualBox，请在终端中输入以下命令：
``` bash
sudo pacman -S virtualbox virtualbox-guest-iso virtualbox-ext-vnc
```
然后需要选择要安装的相应VirtualBox主机模块，具体取决于当前运行的内核版本。与安装驱动程序相似，这样做可确保VirtualBox能够正常运行。例如，在运行内核3.7的情况下，将输入相应的数字以安装以下模块：

uname -r
你会得到类似的东西：3.7.4-1-MANJARO。这意味着内核是linux37。然后安装它
``` bash
sudo pacman -S linux 37 -virtualbox-host-modules
```
安装完成后，就需要将VirtualBox模块添加到内核中。简单的方法是简单地重启系统。否则，要立即开始使用VirtualBox，请输入以下命令：
``` bash
sudo vboxreload
```
向下滚动到页面底部以查找Oracle VM VirtualBox扩展包部分

2.单击安装的VirtualBox版本的相应链接以下载Extension Pack

3.下载Extension Pack后，启动VirtualBox应用程序，启动需要使用sudo virtualbox

4. VirtualBox启动后，从顶部菜单中选择File，然后选择Preferences

5.选择“ 扩展”选项卡以查看该部分，然后单击位于最右侧的 名为“ 添加包”的图标

7.找到下载的Extension Pack，确保它突出显示，然后单击“ 打开”按钮开始安装过程

8.确认您要安装扩展包，然后确认您同意许可条款（至少需要向下滚动到术语底部以激活我同意按钮）

9. Extension Pack应在几秒钟内安装，并会显示确认消息。
[安装Virtualbox Extension Pack]
$ yaourt virtualbox-ext-oracle

`sudo pacman -S virtualbox-ext-oracle`
最后一步是将您的个人用户帐户添加到vbox用户组。这是完全访问VirtualBox提供的功能所必需的，包括在Guest操作系统中使用USB设备的能力。

将您的帐户添加到vbox用户组
将用户名添加到vbox用户组的命令的语法是：
``` bash
sudo gpasswd -a [用户名] vboxusers
sudo gpasswd -a li vboxusers
sudo VBoxManage extpack install --replace Oracle_VM_VirtualBox_Extension_Pack-${LatestVirtualBoxVersion}.vbox-extpack
```
参考资料：https://wiki.manjaro.org/index.php?title=VirtualBox
