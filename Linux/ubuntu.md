# Ubuntu

## 双系统安装
准备一块未分配的分区, 安装的时候，选择这块分区，挂在到 /

## 显卡驱动导致死机问题 
安装ubuntu之后，容易死机，显卡驱动问题，在“软件与更新”.“附加驱动”中安装显卡驱动即可。

## 双系统启动顺序问题
修改启动的顺序，默认win10：`vim /etc/default/grub`，修改GRUB_DEFAULT=0为4，执行：`update-grub`.  
更简单的方式：安装图形化管理界面Grub Customizer：`apt install grub-customizer`

## 删除双系统Ubuntu，恢复Win10
删除ubuntu分区，这个时候把启动文件也删了，win10启动不了。  
用win10的安装盘启动，进入修复命令行，执行：`bootrec /scanos`找到win10的路径，然后执行：`bcdboot g:\windows /s g:`，重启即可。  
可能需要进入bios调整下启动位置。

## 安装常用软件
### 安装中文输入法
`apt-get install fcitx-googlepinyin`  
https://blog.csdn.net/a805607966/article/details/105874756

### 安装微信
`wget -O- https://deepin-wine.i-m.dev/setup.sh | sh`  
- 微信：`sudo apt-get install com.qq.weixin.deepin`  
- QQ：`sudo apt-get install com.qq.im.deepin`  
- 钉钉：`sudo apt-get install com.dingtalk.deepin`  

由于新版变化，安装完成后需要注销重登录才能正常显示应用图标。
  
- https://github.com/zq1997/deepin-wine 
- https://www.zhihu.com/question/344766817  
- https://blog.csdn.net/qq_39182815/article/details/108888186  

### 优化看图软件
Image Viewer是系统自带默认看图软件，不支持Apple的.HEIC images。解决办法如下：
```
sudo apt update
sudo apt install heif-gdk-pixbuf
sudo apt install heif-thumbnailer
sudo apt install libheif1:amd64
```
https://askubuntu.com/questions/1298595/how-to-view-heic-photos-from-iphone-ios-11-on-ubuntu


### 安装图片处理软件
应用商店安装： GNU Image Manipulation Program

### 安装SSH客户端
应用商店安装： pac-vs

### 安装Git GUI
```
apt-get install git-gui
```
在git目录下，执行git gui，可以调出UI
