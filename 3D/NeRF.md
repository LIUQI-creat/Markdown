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
通过沿着**相机光线（camera rays）**获取 5D 坐标，使用经典的**立体渲染（volume rendering）**技术，我们将输出的颜色和密度投影到图像上，从而实现**新视图合成**

实现**神经场（Neural Field）**与图形学组件**体渲染（Volume rendering）**有效结合

![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114194140.png)

#### 用MLP 获取体素信息
输入：空间中点的位置 x = （x,y,z）和相机观察该点的方向 d = （θ, φ）
输出：该点的体素密度（σ）和 自发光颜色c = (r, g, b)

保证多视角一致，使得体素密度σ只与位置x有关；自发光颜色c与位置x和观察方向d有关。

具体MLP如下：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114194408.png)

#### 用体素渲染方程获得生成视角图片：光线采样+积分
将MLP获得的体素密度（σ）和 自发光颜色c = (r, g, b) 通过classical volume rendering 进行渲染，得到虚拟相机穿过每个像素的相机光线得到的颜色，方程如下：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114194927.png)
体素密度（σ）可以解释为射线终止于位置x处的无穷小粒子的微分概率
T(t)表示沿着射线从tn到t所累积的透明度，即光线从tn出发到t穿过该路径、不碰到其他粒子的概率

##### 离散近似计算
MLP仅在固定的离散位置被查询，所以将上面的连续的体素渲染方程变成离散形式进行近似计算：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114202534.png)
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114202609.png)
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114202627.png)
将视线路径均分成N段，在每一段上均匀地随机采样体素用于渲染计算。

##### Hierarchical volume sampling
上述在N个查询点处密集采样的策略是低效的。因为遮挡和自由空间会被重复采样。
采用 **分级表征渲染** ，优化coarse和fine两个网络
 分层采样Nc个点，根据上述公式评估coarse网络，得到coarse网络的输出后，沿着每条射线采样更偏向于对颜色计算有贡献的点
 coarse网络：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114204950.png)
对w进行归一化：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114205029.png)
得到分段常数概率密度函数，然后通过逆变换采样Nf个点，添加至原 Nc 个点中用于 fine 渲染
最后的Loss：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114205225.png)

#### positional encoding
深度网络更倾向于学习低频信息，使用高频函数，将输入映射到更高维度的空间，能让网络更好地拟合包含高频变化的数据
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221114205455.png)
这种表示方法，即使两个点在原空间中距离很近，很难分辨，但是经过positional encoding 后，能够轻松分辨

## 相关材料
https://zhuanlan.zhihu.com/p/380015071
https://github.com/yenchenlin/nerf-pytorch

## 训练
5000 iterations：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115195312.png)
10000 iterations:
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115195443.png)
15000 iterations:
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115195524.png)
20000 iterations:
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115195615.png)
groundtruth:
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115202843.png)
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTU1MTY2Njc4MiwxNTg4NjIwMDAzLDE0Nz
E1OTE1NTUsLTYzMjE5MjE1Myw1NzgyNzg3MiwtMTE0Nzk5ODE2
LC0xNjE0MDY2OTY2LC0xMTAwODgyMDkyLC0xMzUyMDUxODc4LC
0yMDQyMjI4MjAyLC0yMDM0NjQyOTM2LC0yNTU4OTE4MjQsMTAy
OTczNDAxMywxNzA2MTYwMTk2LDE3MTQwMDEzNDgsNzMwMDA2Mz
gsLTE0MjIzMDk3MjQsLTE4OTQ4MDU2NjYsLTkzMzkxNTgzMCwt
MTM1MzEyNjU5Nl19
-->