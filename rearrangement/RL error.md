# 1、数据集的环境安装不好：2D 3D绘图应用API

## GLX 
openGL：Ubuntu下的GLX安装不成功。

![所需环境](https://raw.githubusercontent.com/LIUQI-creat/pic/main/require.jpg)

**【报错】**
The following builds were found, but had missing dependencies. Only one valid platform is required to run AI2-THOR.
Platform Linux64 failed validation with the following errors: No valid X display found
  Linux64 requires a X11 server to be running with GLX. If you have a NVIDIA GPU, please run: **sudo ai2thor-xorg start**

执行Error: unable to open display

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

glxinfo | grep rendering


**make sure X server with OpenGL is running, and the OpenGL extensions have been installed for your graphics card.**


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0NTE5OTkzODAsMjEyMTA3ODExLDE4MT
M3NDQ0MTcsMTA5Njg4NTE5NCwtMTYyNTIyMjE2NywxNDY1MDcw
MTI3LDExMjkwNTM0MDUsLTY5MDI4NDcyOSwxODQ5NjQ1MzI0LD
M1NjU5MDcyMl19
-->