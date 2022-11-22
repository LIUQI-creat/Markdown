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
为了用人体姿态控制隐变量的空间位置，论文将隐变量放在SMPL的6890个端点上，得到structured latent code。每一帧，根据不同视角的图片，预测SMPL，通过SMPL驱动structured latent code的空间位置。
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221116175756.png)

### Code diffusion
因为structured latent code 在3D空间上是稀疏的，因此导致送入NeRF的向量有很多0，因此论文通过3D卷积，把structured latent code变成 latent code volume， 将在端点上的structured latent code扩散到附近的3D空间。

### Density and color regression
与NeRF类似，通过MLP获得体素密度和自发光颜色
**Density model：** 只与latent code有关
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221116173824.png)
**Color model：** 与latent code、观察视角d、空间位置x、以及latent embendding lt （观察到的颜色与实践也有一定关系）有关
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221116174041.png)

### Volume rendering
与NeRF类似，得到的密度和颜色，通过体素渲染进行渲染，得到像素上的颜色。
给定一个像素，我们首先使用相机参数计算它的相机光线，沿着相机光线在近边界和远边界（基于SMPL模型估计场景边界）采样Nk个点，经过上述步骤得到密度和颜色，之后进行近似积分。
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221116174737.png)

### Training
与NeRF类似，计算groundtruth图片与合成的图片像素点颜色的L2损失
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221116175652.png)


### 复现
#### Run the code on People-Snapshot
##### visualization
 - Visualize novel views of single frame
	 1张P40，使用预训练模型latest.pth，时间4：43
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221121161131.png)
 - Visualize views of dynamic humans with fixed camera
	预训练模型，时间8：10
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221121161308.png)
	
	为啥这么模糊？重新再来一遍：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221121171333.png)
	
 - Visualize mesh
	No module named 'OpenGL'
#####  Training on People-Snapshot
- Training
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221122095406.png)

tensorbood：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221122125346.png)

加个可视化结果


#### Run the code on ZJU-MoCap
##### Test on ZJU-MoCap

 - Test on training human poses
     lasted.pth：
	 gt：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221122224649.png)
	 实际：
	 ![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221122224826.png)
	 metric：![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221122224303.png)
 - Test on unseen human poses
	 meti

##### Visualization on ZJU-MoCap
-  Visualize novel views of single frame
-   Visualize novel views of single frame by rotating the SMPL model
-   Visualize views of dynamic humans with fixed camera
-   Visualize views of dynamic humans with rotated camera

##### Training on ZJU-MoCap
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTU2Mjk4OTIzMSwtNjQwOTM0MTIsNTA4Nj
A2MjE2LDI3MzYwODU5MywxNjU4ODU4Njk4LDE3NTM5NTgwNDIs
NDU3ODk0NzMwLC01NTA5NjA3NzcsMTMzODYwODUwMCwxMzYxNT
U1NzM4LDE5MjI3MDg3MzAsNTk0ODc3NTM4LC0xNDE2NDY0NDQ4
LDk5MjIyOTU4LDYzMjQ1NzY2LDUxMzgyMTMzN119
-->