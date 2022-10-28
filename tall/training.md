全连接+ dropout
conv1d
全连接 from liukun
全连接 dropout = 0
learning rate = 0.001


training :liukun 0.0001    
training : liukun  0.001  ---> conv1d 0.0001
stop: liuqi 0.001
training : transformer
training: 100 train, 20 test  用来测试全连接层效果


**loss下降，但是对应的performance没有提高**
![mlp](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221028154001.png)

**Loss提高，但是对应的performance也提高**
![](https://raw.githubusercontent.com/LIUQI-creat/pic/main/20221028155221.png)


<!--stackedit_data:
eyJoaXN0b3J5IjpbMzA5NDkzNDEsLTE5MDk2MzYwMjgsLTE1MD
k2MTU4OTUsODk4NjkzNDUxLC04NDA0OTM3MzZdfQ==
-->