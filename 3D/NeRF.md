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




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyNDA5NDk2NTQsLTEzNTMxMjY1OTYsMT
YxMDY0NTU2MywyMDQwMjk3NjIyXX0=
-->