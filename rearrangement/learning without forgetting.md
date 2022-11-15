# Learning without Forgetting
## 介绍
LWF解决了  不使用原始任务的数据的情况下，保持原始任务的同时又能解决新的任务的问题
LWF可以看做是知识蒸馏和微调的结合，学习对新任务有区别的参数，同时又保留原始任务在训练数据上的输出。
**输入：** 训练新任务的数据
**输出：**  通过训练整个网络、old task 和new task，得到new task任务上最好的结果

### 算法流程
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115215019.png)
 ①首先记录Y0：新任务的数据通过原有网络和old tasks 得到的输出，作为之后知识蒸馏的教师网络的输出。
 ②训练网络；
	 首先warm-up: 固定网络参数θs和old task 参数θo，训练新任务参数θn收敛
	 之后joint-optimize-step：共同训练θs、θo、θn
	 warm-up对于LWF是不必须的，加上是为了与微调比较
③损失函数：
对于新任务，通过交叉熵损失函数，使得预测的标签接近真实值
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115215928.png)
对于旧任务：
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115220044.png)
通过知识蒸馏Loss，将温度T设置为2，使得使用新任务的数据训练的旧任务的网络参数更贴近于旧任务

## 
<!--stackedit_data:
eyJoaXN0b3J5IjpbODk4ODYxNzU3LDE3NDUxMzY1NDgsLTUzND
czODU5MCwxNjMzNjQxMzAyXX0=
-->