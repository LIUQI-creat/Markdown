全连接+ dropout
conv1d
全连接 from liukun
全连接 dropout = 0
learning rate = 0.001

## 使用全连接or一维卷积
training :liukun 0.0001    
training : liukun  0.001  ---> conv1d 0.0001
stop: liuqi 0.001
training : transformer
training: 100 train, 20 test  用来测试全连接层效果


**loss下降，但是对应的performance没有提高**
![mlp](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221028154001.png)

**Loss提高，但是对应的performance也提高**
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221028155221.png)
最终结果，最好的是30 左右。
分析：在训练集上的拟合的效果不应该这么差。

## 修改loss
改为smooth_l1_loss 

##  没有0的二维卷积
从一维又变成二维。

## 把最后的特征图修改为二维
### transformer
### 全连接
### 二维卷积
### transformer  8layers + layernorm


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1Mzg3MTIyOTgsMTU2ODIyODkxNCwxNT
UxMTM0MTE0LC0xODk1Mzg3NDk4LDMwOTQ5MzQxLC0xOTA5NjM2
MDI4LC0xNTA5NjE1ODk1LDg5ODY5MzQ1MSwtODQwNDkzNzM2XX
0=
-->