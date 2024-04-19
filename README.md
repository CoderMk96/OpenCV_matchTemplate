### 项目简介

利用opencv提供的模板匹配方法，实现银行卡卡号的截取和识别。

### 效果图

![](C:\Users\24111\AppData\Roaming\marktext\images\2024-04-19-19-12-18-image.png)

### 环境依赖

基于python 3.6.4， opencv 3.4.1开发的

### 更新日志

#### V1.0.0 版本

对于模板图：

1. 转灰度图

2. 二值化图像，使用反二进制阈值化 THRESH_BINARY_INV

3. 计算轮廓，只检测外轮廓，指保留重点坐标，得出每个数字的轮廓链表

4. 对轮廓链表根据位置，进行排序，放入字典中{数字，对应图像}

对于检测图：

1. 初始化卷积核，一个是在礼帽操作时使用，另一个是在闭运算时使用

2. 读取输入图像，预处理（转灰度图）

3. 礼帽操作，突出更明亮的区域（原始输入-开运算）

4. Sobel梯度计算，用于进一步加强边缘

5. 归一化，加强梯度的对比值

6. 将归一化后的梯度图像转换为8位无符号整数类型，以便显示和处理

7. 进行闭操作，将数字连在一起去

8. 二值化，使用固定值进行二值化，并自动寻找合适的阈值

9. 再进行闭操作，使边缘更加连续

10. 计算轮廓

11. 遍历轮廓，并根据区域和大小进行筛选

12. 将合适的轮廓进行从左到右排序

13. 遍历每一个轮廓中的数字，在灰度图中根据轮廓位置进行截取，二值化（自动阈值）

14. 计算每一组轮廓，并根据从左到右排序

对于得出来的数字（4个数字一组）：

1. 找到当前数值的轮廓，resize成合适的大小

2. 遍历模板字典，进行模板匹配计算各分，并将其放到scores[]列表中

3. 取出scores列表中最大值所对应的索引位置，即为其代表的数字
