# **01-数据中心-数据分析：最新版本中，媒体分析下方的时间展示与上方时间选择无法对应，且折线图还是有被遮挡；**

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200326155231029.png" alt="image-20200326155231029" style="zoom:50%;" />

+ analysisTableClick（component） // 媒体分析中的tab栏
  + initRequestData（） // 初始化请求数据
    + 对象传入 走势图、占比图、排行榜
    + 测试：
      + 设置显示图表时间为32天
      + this.tableData 获取到的数据为32天
      + 请求发送的时间吻合
      + dataName 和dataDate数据都没有问题
      + 最大只能显示9天
+ selectorEchartsType（opt）
  + opt数据正常
+ LineBar.vue 
  + optionData 数据正常

+ 查看MediaChartTable插件

##  已解决：

+ 设置lengend的（遮挡问题）
  + `stop=start`
  + left
  + `orient=horizontal`
+ 设置`dataZoom.endValue=100`（时间显示不全问题）
  + 发现X轴被强制设置为最大8个



# 02- 数据- 数据视窗- 热点新闻详情页：媒体报道样式调整

![image-20200330150417115](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200330150417115.png)

+ ul>li 为脱标元素，导致父盒子无法被子元素撑开

## 已解决

+ 设置父盒子
  + position:`relative`



# 03- 数据中心-数据视窗：监管动态模块，证监局，深交所，深圳证监局下方均无数据显示；

![image-20200330150655758](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200330150655758.png)

+ 数据获取正常
+ 数据传输正常

## 已解决

+ 条件判断有误
  + 没有做兜底



# 04-**数据中心-法律法规：使用右侧条件进行筛选，切换到筛选结果最后一页时，会弹出所有的法律法规，不止限与当前筛选的条件；**

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200331152544953.png" alt="image-20200331152544953" style="zoom: 50%;" />![image-20200331152556887](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200331152556887.png)

![image-20200331152647656](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200331152647656.png)

+ 发文单位发送请求的数据结构

  + ![image-20200331153010914](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200331153010914.png)

  + 三级数据，分别用三个数组存储

+ 适用范围发送请求的数据结构

  + ![image-20200331153116818](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200331153116818.png)
  + 二级数据，用二级的id拼接成的数组

### **bug**

+ 第一次点击发文单位的选项时请求参数：
  + ![image-20200331153528271](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200331153528271.png)
  + 正常

+ 随机点击页码切换时参数：
  + ![image-20200331153617856](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200331153617856.png)
  + 参数切换成了使用范围的参数

+ 查看代码可知
  + ![image-20200331153705264](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20200331153705264.png)
  + 切换页码始终获取的是适用范围的数据

+ 解决办法：
  + ~~切换页面时判断当前是从哪里切来的？~~
    + 无法进行判断
      + 在切换发文单位和适用范围的时候进行清空
  + 清除适用范围中的选项
  + 传入发文单位的选项

+ 最终解决方案
  + 发文单位触发时将参数储存起来
  + 在点击页面时进行提取
  + 在切换tab栏时清楚相反的数据内容