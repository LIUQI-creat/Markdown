## 1、数据集的环境安装不好
openGL：Ubuntu下的GLX安装不成功。
安装需要sudo apt-get ，但是没有权限。
http://www.sztemple.cc/articles/linux%E4%B8%8B%E7%9A%84opengl-mesa%E5%92%8Cglx%E7%AE%80%E4%BB%8B
https://en.wikibooks.org/w/index.php?title=OpenGL_Programming/Installation/Linux&veaction=edit&section=2

## ai2-thor
The following builds were found, but had missing dependencies. Only one valid platform is required to run AI2-THOR.
Platform Linux64 failed validation with the following errors: No valid X display found
  Linux64 requires a X11 server to be running with GLX. If you have a NVIDIA GPU, please run: **sudo ai2thor-xorg start**

![所需环境](https://raw.githubusercontent.com/LIUQI-creat/pic/main/require.jpg)

## training
Exception: The following builds were found, but had missing dependencies. Only one valid platform is required to run AI2-THOR.
Platform CloudRendering failed validation with the following errors: Vulkan API driver missing.
  CloudRendering requires libvulkan1. Please install by running: sudo apt-get -y install libvulkan1




<!--stackedit_data:
eyJoaXN0b3J5IjpbMzU2NTkwNzIyXX0=
-->