# 1、数据集的环境安装不好：2D 3D绘图应用API

## GLX 
openGL：Ubuntu下的GLX安装不成功。

![所需环境](https://raw.githubusercontent.com/LIUQI-creat/pic/main/require.jpg)

**【报错】**
1、The following builds were found, but had missing dependencies. Only one valid platform is required to run AI2-THOR.
Platform Linux64 failed validation with the following errors: No valid X display found
  Linux64 requires a X11 server to be running with GLX. If you have a NVIDIA GPU, please run: **sudo ai2thor-xorg start**

2、执行完安装命令，执行glxinfo | grep "OpenGL version"：
** Error: unable to open display**

https://askubuntu.com/questions/1206767/understanding-glxinfo-error
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221104100813.png)
服务器上不能运行？

3、运行训练指令
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221104102343.png)

**【问题】**
安装需要sudo apt-get ，但是没有权限。
http://www.sztemple.cc/articles/linux%E4%B8%8B%E7%9A%84opengl-mesa%E5%92%8Cglx%E7%AE%80%E4%BB%8B
https://en.wikibooks.org/w/index.php?title=OpenGL_Programming/Installation/Linux&veaction=edit&section=2

##  解决方法
### 解决方法1： 用脚本启动x-server
**不需要渲染**
Passing in `headless` in this context means you want a controller without actually rendering any frames (i.e., a metadata-only controller).

> sudo python /PATH/TO/startx.py &

https://github.com/allenai/ai2thor/issues/993
**【问题】**
执行不了脚本，没有权限。
**【解决】**
https://github.com/allenai/ai2thor/issues/325
联系管理员，管理员说不行。

### 解决方法2：使用CloudRendering platform
这样就不启动Xorg server
采用CloudRendering platform
https://github.com/allenai/ai2thor/issues/934
**【问题】**
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221104115444.png)
Vulkan还不匹配，还需要重新装下。

**【解决】**
https://linuxconfig.org/install-and-test-vulkan-on-linux
https://command-not-found.com/vulkaninfo
自定义镜像的时候有问题
https://blog.csdn.net/luolinll1212/article/details/113261022
https://github.com/allenai/ai2thor/issues/924

用编译的方式安装，编译完成了，但是无法

> vulkaninfo | less

**error: XDG_RUNTIME_DIR not set in the environment.**
https://github.com/allenai/ai2thor-docker
https://www.dianjilingqu.com/444537.html

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
## 数据加载运行效果
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/%E5%BE%AE%E4%BF%A1%E5%9B%BE%E7%89%87_20221103200240.jpg)
## 运行十分卡顿
不能进行其他操作，左上角的虚拟界面会变灰黑屏
## 出错1  multiprocess并行处理
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221103195751.png)
## 出错2  与ai2thor数据库连接
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/1bfa04b032597b2d95755d1d6fe1afe.jpg)








engine.py    1997      / 319
vector_sampled_tasks.py           163


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTExMzE0OTgzMCwtNDkzMTIyMTQ3LC0xMD
g0ODkzMTY4LC0xMzA5MzY3OTY1LC0xNzMwOTM3MzQxLDI1NTM5
NjY1MSwtODQ3MzI4MDEyLC0xMTUyOTg1NjYsLTY5NzkxMjAyMy
wtMTEyNTQwNjE2NiwtNTM1OTM5NDU1LC0xODQ5MjM2MDAzLDE5
MzA1MzUyMjMsNzUyNjU5MjYxLDE1ODU3NzczNDMsMTQ3MDUzNz
QxNywyMTIwMzg5OTcxLDUyOTg5MTcyOCwtMTg3MjA2MDYzNCwx
NjczOTgzMDEwXX0=
-->