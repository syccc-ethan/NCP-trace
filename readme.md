## 本文主要内容

- [目前困境](#困难)
- [使用说明](#使用说明)
- [使用pyecharts搭建中国疫情地图](#pyecharts)
- [肺炎实时追踪页面制作](#肺炎实时追踪页面制作)
- [后续开发](#后续开发)
- [参考资料](#参考资料)

## 困难

### 未解决

- Web端利用Js或其他接口如何确定当前使用人的地理位置？从而有针对性地显示当地省份的疫情地图。
- Python将得到的数据保存为json文件，JavaScript调用json文件。自动生成疫情数据。

### 已解决
- 数据来源问题已经解决，原本是根据支付宝的肺炎实时追踪手敲的，并保存在data_2020_02_12.py中。现在使用腾讯数据接口获取疫情数据。
- 省份确诊人数在市级上不产生颜色和数字变化，已解决。程序中城市的命名需要加<font color=red>**"市"**</font>才能匹配地图上的位置。
- 世界确诊人数在国家上不产生颜色和数字变化，已解决。程序中国家的命名需要为<font color=red>**"英文"**</font>才能匹配地图上的位置。

## 使用说明

### 文件作用说明

- readme.md即本说明文档
- images文件夹存放的是相关图片
- data_2020_02_12.py是根据支付宝手敲的数据，可以不看
- getData.py是利用腾讯数据接口获取疫情数据
- 中国疫情地图.py用于生成中国疫情地图.html文件
- 中国疫情地图.html用于在浏览器上展示，双击或拖拽到浏览器即可
- 肺炎实时追踪.html/.css将汇总各个页面，预计展示以下信息：
  - 全国疫情确诊人数分布图
  - 省份疫情确诊人数分布图
  - 全球疫情确诊人数分布图
  - 累计趋势分析
  - 增长趋势分析
  - 国内疫情数据汇总
  - 国外疫情数据汇总
  - 疫情实时讯息

## pyecharts

### pyecharts的介绍

pyecharts是一个用于生成Echarts图表的类库，Echarts是百度开源的一个数据可视化JS库

### pyecharts的安装

- 安装库：pip install pyecharts
- 安装地图文件：
  - 全球国家地图: pip install echarts-countries-pypkg
  - 中国省级地图: pip install echarts-china-provinces-pypkg
  - 中国市级地图: pip install echarts-china-cities-pypkg
  - 中国区县级地图: pip3 install echarts-china-counties-pypkg 
  - 中国区域地图: pip3 install echarts-china-misc-pypkg

### pyecharts的使用

- [pyecharts官网](http://pyecharts.org/#/)
- [pyecharts效果图展示](http://pyecharts.herokuapp.com/)

### pyecharts的代码示例

``` python
from pyecharts.charts import Map
from pyecharts import options as opts
#将数据处理成列表
locate = ['北京','天津','河北','山西','内蒙古','辽宁','吉林','黑龙江','上海','江苏','浙江','安徽','福建','江西','山东','河南','湖北','湖南','广东','广西','海南','重庆','四川','贵州','云南','陕西','甘肃','青海','宁夏','新疆','西藏']
popu = [10,8,18,8,5,29,8,17,27,24,12,11,6,7,22,16,11,14,18,5,1,7,14,4,6,8,6,15,13,39,25,21]
list1 = [[locate[i],popu[i]] for i in range(len(locate))]
map_1 = Map()
map_1.set_global_opts(
    title_opts=opts.TitleOpts(title="全国疫情确诊人数分布图"),
    visualmap_opts=opts.VisualMapOpts(max_=50)  #最大数据范围
    )
map_1.add("确诊人数", list1, maptype="china")
map_1.render('map1.html')
```

**示例效果图：**![](./images/示例效果图.png)

### 注意事项

<font color=red>**pyechart旧版本和新版本不兼容，且代码编写风格迥异，旧版本不再维护，鼓励大家使用新版本。**</font>

## pygal

### pygal安装

- pip install pygal

## 肺炎实时追踪页面制作

### 页面布局

### iframe

### 锚

- 锚点目标：  

```html 
<div id="test" name="test"></div>
```

- 锚点：**注意在href的属性值前加“<font color=red>#</font>”**

```html 
<div id="test" href="#test"></div>
```

### 效果示意图

- **全国疫情确诊人数分布图**![](./images/全国疫情确诊人数分布图.png)
- **省份疫情确诊人数分布图**![](./images/湖北疫情确诊人数分布图.png)
  - <font>在有网情况下省份定位显示省份疫情地图，无网显示默认<font>
  - <font>利用Javascript制作下拉表单，用户可以通过点击，选择显示的省份<font> ![](./images/省份选择.png)
- **全球疫情确诊人数分布图**![](./images/世界疫情确诊人数分布图.png)
- **累计趋势分析**![](./images/累计趋势.svg)
- **增长趋势分析**![](./images/新增趋势.svg)
- **国内疫情数据汇总**![](./images/chinaData.png)
- **国外疫情数据汇总**![](./images/worldData.png)
- **疫情实时讯息**![]()

## 后续开发

- 疫情发展预测

## 参考资料

### pyecharts作图

- [python绘制中国地图](https://zhuanlan.zhihu.com/p/45202403)
- [pyecharts官网](http://pyecharts.org/#/)
- [pyecharts效果图展示](http://pyecharts.herokuapp.com/)
- [python制作疫情实时分布图](https://zhuanlan.zhihu.com/p/105840267)
- [数据可视化：使用pyecharts制作疫情地图——进击的小梓](https://zhuanlan.zhihu.com/p/105001857?utm_source=wechatMessage_article_bottom)
- [（源代码）用Python制作疫情的实时数据地图（PS：全国以及每个省）——刘凤飞](https://zhuanlan.zhihu.com/p/105072241)
- 疫情数据来自腾讯数据接口

### pygal做趋势图svg

- [pygal官方文档](http://www.pygal.org/en/stable/documentation/index.html)

### html页面制作

- iframe标签
  - [Web前端之iframe详解——	
滥好人 ](https://www.cnblogs.com/hq233/p/9849939.html)

- 地理位置获取
  - [使用JS获取当前地理位置方法汇总——一纸奇文(暂时不可行)](https://blog.csdn.net/fyfy0613/article/details/81698897)

- 下拉菜单制作
  - [web前端实战系列[3]——下拉菜单——叶莜落](https://www.cnblogs.com/helloIT/articles/5155698.html)
  - [快速制作下拉式菜单栏](https://www.bilibili.com/video/av82476546?from=search&seid=429844793107330536)

### Web同源策略，跨源请求

- [Firefox 68: CORS请求不是http](https://www.jianshu.com/p/78904381ba32)