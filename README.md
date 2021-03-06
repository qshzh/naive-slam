# naive-slam
Stereo SLAM in Matlab

- 目标：从双目相机采集到的数据根据稀疏法绘制特征点地图。[效果](https://www.youtube.com/watch?v=MUyNOEICrf8 "orb-slam")
- 非实时

## 一、框架
![](https://github.com/zqsh/naive-slam/blob/master/asset/frame.png)
### 1、视觉数据
无

### 2、前端里程
![](https://github.com/zqsh/naive-slam/blob/master/asset/od.png)

1. 采集的图像进行矫正，畸变图像处理
2. 特征检测匹配
3. 同一时刻的二张图片根据对极几何原理估计特征点的位置
4. t时刻的图片与t+1时刻的图片 估计相机的旋转矩阵和平移向量


### 3、后端优化
- 什么是后端优化。理想上如果前端里程估计的数据玩完全正确的话，就能有完美的定位和建图。但是这是不可能的233333. 每一帧都会有误差，累计误差的积累会让结果非常不好，大尺度下甚至不能用。 
- 常用的方法有：BA、EKF、Graph-based 我们课程设计使用自己手写的EKF进行实验。好处就是：可控！即使偏差大了也能知道哪步有问题。不会陷入盲目调参，对学习有帮助。有EFK模型基础，再用图优化时候理解会更深。
![](https://github.com/zqsh/naive-slam/blob/master/asset/ekf.png)

### 4、建图
- 挖坑待填

### 5、回环检测
![](https://github.com/zqsh/naive-slam/blob/master/asset/loop-closure.png)
- 大坑！怕matlab没有好用的轮子，自己重写要挂。
- 小尺度的可以尝试

## 二、分工
![](https://github.com/zqsh/naive-slam/blob/master/asset/matlab.png)

### 2017-4-4
1. LZY 负责图像的畸变处理和图像转移关系的求解
2. GMH 负责他图像的特征点的提取和匹，根据双目求解出特征点的深度
3. KZL 负责根据图像来反求解出相机的位姿变化
4. FJJ 负责SLAM的后端优化
5. ZQS 负责喊加油和胶水作用

### 2017-4-22
1. ZQS 增加了测试KITTI数据
## 二、一些有用的资源

- [半闲居士blog](http://www.cnblogs.com/gaoxiang12/)
- [slam 14讲](https://github.com/gaoxiang12/slambook)
- [入门资料](https://blog.csdn.net/lmg2015/article/details/52869208)

