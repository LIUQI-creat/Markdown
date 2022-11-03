# 1、数据集的环境安装不好：2D 3D绘图应用API

## GLX 
openGL：Ubuntu下的GLX安装不成功。

![所需环境](https://raw.githubusercontent.com/LIUQI-creat/pic/main/require.jpg)

**【报错】**
The following builds were found, but had missing dependencies. Only one valid platform is required to run AI2-THOR.
Platform Linux64 failed validation with the following errors: No valid X display found
  Linux64 requires a X11 server to be running with GLX. If you have a NVIDIA GPU, please run: **sudo ai2thor-xorg start**

执行完安装命令，执行glxinfo | grep "OpenGL version"：
** Error: unable to open display**

**【问题】**
安装需要sudo apt-get ，但是没有权限。
http://www.sztemple.cc/articles/linux%E4%B8%8B%E7%9A%84opengl-mesa%E5%92%8Cglx%E7%AE%80%E4%BB%8B
https://en.wikibooks.org/w/index.php?title=OpenGL_Programming/Installation/Linux&veaction=edit&section=2

## Vulkan
Vulkan API安装不成功

**【报错】**
Exception: The following builds were found, but had missing dependencies. Only one valid platform is required to run AI2-THOR.
Platform CloudRendering failed validation with the following errors: Vulkan API driver missing.
  CloudRendering requires libvulkan1. Please install by running: **sudo apt-get -y install libvulkan1**

**【问题】**
无法sudo
通过cmake安装缺少环境
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221028111015.png)


![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221101143106.png)


## glx
sudo apt-get update
sudo apt-get install mesa-utils

sudo apt update
sudo apt upgrade
sudo add-apt-repository ppa:kisak/kisak-mesa
sudo apt update
sudo apt install mesa

apt-get update && apt-get install -qy build-essential libgl1-mesa-dev
sudo apt-get -y install libvulkan1

sudo apt-get install xbase-clients
systemctl set-default graphical.target
glxinfo | grep rendering


**make sure X server with OpenGL is running, and the OpenGL extensions have been installed for your graphics card.**


# 2、在1070Ti 运行错误
## 运行效果

## 运行十分卡顿
## 出错1
## 出错2







engine.py    1997      / 319
vector_sampled_tasks.py           163


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg3NDU5MTE0MywtMjA1Nzc5NDY5NCwtNj
Y4ODMzMjEzLC0xMTMxMDUwMzU2LC0xNDU2Mzk2NDI2LDIxMjEw
NzgxMSwxODEzNzQ0NDE3LDEwOTY4ODUxOTQsLTE2MjUyMjIxNj
csMTQ2NTA3MDEyNywxMTI5MDUzNDA1LC02OTAyODQ3MjksMTg0
OTY0NTMyNCwzNTY1OTA3MjJdfQ==
-->