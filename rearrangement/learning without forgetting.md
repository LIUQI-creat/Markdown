# Learning without Forgetting
## 介绍
LWF可以看做是知识蒸馏和微调的结合，学习对新任务有区别的参数，同时又保留原始任务在训练数据上的输出。
**输入：** 训练新任务的数据
**输出：**  通过训练整个网络、old task 和new task，得到new task任务上最好的结果

### 算法流程
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221115215019.png)
 ①首先记录Y0：新任务的数据通过原有网络和old tasks 得到的输出，作为之后知识蒸馏的教师网络的输出。
 ②训练网络；
	 首先warm-固定网络参数θs和old task 参数θo，
## 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY0NzAzNjEzMSwtNTM0NzM4NTkwLDE2Mz
M2NDEzMDJdfQ==
-->