# NERF
## 背景
视角合成使用一个中间3D场景表征作为中介，生成高质量的虚拟视角。根据表示形式，分为显式和隐式
### 显式
Mesh，Point Cloud，Voxel，Volume等
优点：对场景显式建模，合成照片级别的虚拟视角。
缺点：离散表示，不够精细化，造成重叠等伪影；对内存的消耗，限制了高分辨率场景的应用
### 隐式
用函数表述场景几何。
优点：连续的表示，适用于大分辩率场景，不需要3D信号监督
缺点：无法生成照片级的虚拟视角

## NeRF
### 简介
实现神经场（Neural Field）与图形学组件体渲染（Volume rendering）有效结合

![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114194140.png)
#### 用MLP 获取体素信息
输入：空间中点的位置 x = （x,y,z）和观察方向 d = （θ, φ）
输出：该点的体素密度（σ）和 自发光颜色c = (r, g, b)

保证多视角一致，使得体素密度σ只与位置x有关；自发光颜色c与位置x和观察方向d有关。

具体MLP如下：


#### 用体素渲染方程获得生成视角图片：光线采样+积分


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIzOTc2MTQ5NiwtMTQyMjMwOTcyNCwtMT
g5NDgwNTY2NiwtOTMzOTE1ODMwLC0xMzUzMTI2NTk2LDE2MTA2
NDU1NjMsMjA0MDI5NzYyMl19
-->