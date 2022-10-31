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
最终结果，最好的是 **30** 左右。
分析：在训练集上的拟合的效果不应该这么差。

## 修改loss
改为smooth_l1_loss 
效果很差
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221031132851.png)
##  没有0的二维卷积
从一维又变成二维。去除了为0 的部分，用长方形的卷积核进行卷积
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221031133005.png)

## 把最后的特征图修改为二维
### transformer
### 全连接
### 二维卷积
### transformer  8layers + layernorm


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkwNjM5ODc3MCwtMTUzODcxMjI5OCwxNT
Y4MjI4OTE0LDE1NTExMzQxMTQsLTE4OTUzODc0OTgsMzA5NDkz
NDEsLTE5MDk2MzYwMjgsLTE1MDk2MTU4OTUsODk4NjkzNDUxLC
04NDA0OTM3MzZdfQ==
-->