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
+ 