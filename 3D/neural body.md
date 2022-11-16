# Neural Body: Implicit Neural Representations with Structured Latent Codes for Novel View Synthesis of Dynamic Humans
##  引言
### 解决的问题
解决从稀疏的相机视角，生成动态人体的自由视角的视频

### 当前方法的局限性
 - NeRF需要非常稠密的视角来训练网络。对于动态物体，设备成本高，并且不方便
 - NeRF只能处理静态场景。对于每个静态场景训练一个网络，对于动态场景，上百帧需要训练上百个网络，成本高

### 本文的idea
基于观看一个动态的物体更能想象他的3D形状，因此通过整合时序信息来获取足够多的3D shape observation，解决稀疏视角下，单帧信息不足以恢复正确的3D scene representation
定义一组隐变量，从同一组隐变量中生成不同帧的场景，能把不同帧观察的信息和一组隐变量关联到一起。经过训练能把一段视频的各个帧的信息整合到隐变量中，从而实现整合时序信息的目的。
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221116171936.png)

##  论文方法
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221116172054.png)
### structured latent code
为了用人体姿态控制隐变量的空间位置，论文将
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMjQ5OTUwNzMsOTkyMjI5NTgsNjMyND
U3NjYsNTEzODIxMzM3XX0=
-->