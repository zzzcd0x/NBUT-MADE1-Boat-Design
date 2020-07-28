NBUT 2020 MADE I Boat Design

writer：zzzcd0x

# 思路

根据板材长度以及合理的长宽比等因素设定A和B的范围

第一步是粗筛，即枚举A的范围内每一个长度为0.6的区间的中点，计算中点位置的A、B、H对应的船体底面方程的重心、正浮吃水线、倾斜135°时的吃水线平面方程、浮心和复原力矩，最终判断该答案是否合理的条件是135°时复原力矩绝对值小于0.01

得到区间中点后手动选取几组理想的数据然后放入精筛，精筛中讲枚举选取的每一个中点对应的区间中的每一个值，筛选条件比粗筛多了长宽比、复原力矩绝对值大小要求小于0.001。

最终从精筛得到的数据中选取一组理想的作为最终数据

# 各个函数的作用

- low_accuracy 粗筛主函数
- high _accuracy 精筛主函数
- getCOM 返回值为船体重心的z轴坐标
- getCOB 返回值为储存135°时船体浮心的一维矩阵
- getTOI 返回值为复原力矩
- waterline 返回值为正浮吃水线高度
- waterline135 返回值为135°时吃水线方程的截距

# 注意事项和优化方案

粗筛过程代码运行时间较长，原因是没有用到matlab擅长的矩阵运算而是用了积分计算，因此每一组ABH要运行大概3s，虽然很多数据会在计算前没筛掉但因为需要枚举的数据量巨大，所以还是很慢。

精筛会筛出较大量的数据，因此最终将结果输出到了excel方便查看和筛选。

matlab无法求解带参积分，所以将求解带参积分的过程改为了二分求解参数值，二分可以在远小于枚举的时间复杂度内求得不差于枚举的答案。
# 下水咯

![](https://cdn.luogu.com.cn/upload/image_hosting/lsdbndwg.png)
