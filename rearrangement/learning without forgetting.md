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

## 方法比较
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115221854.png)
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115222309.png)
### Fine-tuning
训练θs、θn参数，θo不变。利用小的学习率，希望参数能够稳定在距离原始值不太远的局部最优处。
优点：新任务表现好
缺点：旧任务表现差

### Feature Extraction
训练θn参数，θs、θo不变。
不修改原始网络，但原始网络中的特性不一定适合新的任务，因此new task performance 一般。

### Joint Training
训练θn、θs、θo参数。
输入是所有任务的训练数据，通过整合所有任务的共同知识，改进所有任务。每个任务为其他任务提供正则化
训练效率慢，需要数据多。

### Learning without Forgetting
训练θn、θs、θo参数。
输入是新任务的训练数据，相比Joint Training 所需数据变少。
新的任务上，表现好于fine-tuning, LFL, fine-tuning FC, and feature extraction
在旧的任务上，比微调更好

## 训练结果
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221116120228.png)
每次增加5类，进行分类预测。Test Accuracy 是总的分类结果
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221116120402.png)
是每5类的分类(新任务)的预测结果



<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUxMjM3MzgwNiwxMzI2NTY0Nzk1LC0xNj
QxMTc0MDksMTI3NjAyMjkyLDIwNDMyODU2OTksLTE1MTk1NDEy
OTEsODk4ODYxNzU3LDE3NDUxMzY1NDgsLTUzNDczODU5MCwxNj
MzNjQxMzAyXX0=
-->