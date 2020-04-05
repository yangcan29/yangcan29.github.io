---
layout:     post
title:      highcharts入门
subtitle:   简单上手highcharts画图表
date:       2020-04-05
author:     YC
header-img: img/post-bg-20200405.jpg
catalog: true
tags:
    - 前端
---
# 四个步骤快速上手
和echarts很相似，同样都是画图表的库，使用上大体相似，不过配置option属性上面还是有很多细微的差异，因此遇到问题多参考[官方API文档](https://api.highcharts.com.cn/highcharts)。我个人更喜欢highcharts的API文档，因为每个属性后面都有简要的配置说明，而且对应的每个属性还有在线实例，可以说非常体贴了。
## 1.引入highcharts

```js
<!--步骤1 引入 highcharts.js -->
<!-- 网络引入 -->
<!-- <script src="http://cdn.highcharts.com.cn/highcharts/highcharts.js"></script> -->
<script src="./js/highcharts.js"></script>
```

注意引入的路径正确就好。

## 2.准备DOM容器

```js
<!--步骤2 图表容器 DOM -->
<div id="container" style="width: 600px;height:400px;"></div>
```

## 3.配置图表项目

```js
//步骤3 图表配置
var options = {
        chart: {
            type: 'column'                          //指定图表的类型，默认是折线图（line）
        },
        title: {
            text: '我的第一个图表'                 // 标题
        },
        xAxis: {
              categories: ['苹果', '香蕉', '橙子']   // x 轴分类
        },
        yAxis: {
            title: {
                text: '吃水果个数'                // y 轴标题
            }
        },
        series: [{                              // 数据列
            name: '小明',                        // 数据列名
            data: [1, 0, 4]                     // 数据
            }, {
                name: '小红',
                data: [5, 7, 3]
            }]
        };
```

options是highcharts的配置项，图表的数据及图表组件都在这里进行配置，通过键值对的形式存在，参考API文档完成配置。

## 4.图表绘制

```js
//步骤4 图表初始化函数并且绘图
var chart = Highcharts.chart('container', options);
```

在`id="container"`的DOM容器处，通过`chart()`函数进行图表绘制。

这个实例为[官方一分钟上手教程](https://www.highcharts.com.cn/docs/start-helloworld)。

# 常用的配置教程
- [数据列（series）](https://www.highcharts.com.cn/docs/basic-series)  
- [数据提示框及提示的格式](https://www.highcharts.com.cn/docs/basic-tooltip)：格式化函数formatter属性  
- [图例内容及样式配置](https://www.highcharts.com.cn/docs/basic-legend)  
- [去除版权信息](https://www.highcharts.com.cn/docs/basic-legend)  

# 实例巩固
## 简单甘特图代码

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>gantt</title>
</head>
<body>
    <!--步骤1 引入 highcharts.js -->
    <!-- 网络引入 -->
    <!-- <script src="http://cdn.highcharts.com.cn/highcharts/highcharts.js"></script> -->
    <script src="./js/highcharts.js"></script>
    <script src="./js/xrange.js"></script>

    <!--步骤2 图表容器 DOM -->
    <div id="container" style="width: 600px;height:200px;"></div>

    <script>
        //步骤3 图表配置
       options={
            chart: {
                type: 'xrange'    //类型为甘特图，注意除了highcharts.js引入以外还要引入xrange.js
            },
            title: {
                text: '简单甘特图'    //标题
            },
            xAxis: {
            },
            yAxis: {
                title: {
                    text: '',
                },
                categories: ['序列1', '序列2' ],   //y轴表示类别
                labels: {
				style: {
                   // color: 'red',
                    fontSize: 18      //设置y轴标签的样式，字体大小为18px
				}
			},
                reversed: true      //true：y轴从上到下为序列1，序列2；false：否则为序列2，序列1
            },
            tooltip: {
               outside: true,
            //    设置提示框的格式
               formatter:function(){
                 return this.yCategory+"："+this.x+"到"+this.x2;
              }
            },
            legend:{
                enabled:false,      //取消图例
            },
            series: [{
                name: '花费时间',
                borderColor: 'gray',
                colors: ['blue','red'],  //序列的颜色为蓝和红
                pointWidth: 30,    // 序列的高度
                // x表示每个块起始值，x2表示终止值；y=0表示系列1，y=1表示系列2；partialFill为块上面的标值
                data: [{x: 0, x2: 8, y: 0, partialFill: 1}, 
                { x: 9.746, x2: 17.746, y: 0, partialFill: 2}, 
                { x: 21.406, x2: 29.406, y: 0, partialFill: 4}, 
                { x: 32.64, x2: 38.64, y: 0, partialFill: 8}, 
                { x: 40.386,  x2: 46.386,  y: 0, partialFill: 7},
                { x: 50.252, x2: 56.252, y: 0, partialFill: 6},
                { x: 58.002, x2: 64.002, y: 0, partialFill: 5},
                { x: 67.138, x2: 71.138,  y: 0, partialFill: 21},
                { x: 73.388, x2: 77.388, y: 0, partialFill: 20}, 
                { x: 82.888, x2: 86.888, y: 0, partialFill: 18}, 
                { x: 0, x2: 6, y: 1, partialFill: 3}, 
                { x: 12.03,  x2: 18.03,  y: 1, partialFill: 10},
                { x: 20.939, x2: 26.939, y: 1, partialFill: 9},
                { x: 31.711, x2: 37.711, y: 1, partialFill: 11},
                { x: 40.628, x2: 46.628,  y: 1, partialFill: 12},
                { x: 50.739,  x2: 53.739,  y: 1, partialFill: 16},
                { x: 56.648, x2: 59.648, y: 1, partialFill: 15},
                { x: 64.759, x2: 67.759, y: 1, partialFill: 14},
                { x: 70.676, x2: 73.676,  y: 1, partialFill: 13},
                { x: 77.355, x2: 79.355, y: 1, partialFill: 17},
                { x: 86.888, x2: 89.888,  y: 1, partialFill: 19},    
            ],
                dataLabels: {
                    enabled: true          //partialFill是否会显示，true为显示
                }
            }]
        };

        //步骤4 图表初始化函数并且绘图
        var chart = Highcharts.chart('container', options);
    </script>
</body>
</html>
```
这是一个非常简单的甘特图，但是我当时为了实现功能还是配置了很久，因为阅读API文档找对应的功能配置还是很需要耐心，并且不断尝试。而且对于partialFill这个函数我还修改了源文件xrange.js里面对应的函数，因为源文件中的函数返回的是百分数。因此最后的效果如下图。

## 甘特图效果
![甘特图效果](https://s1.ax1x.com/2020/04/05/GrP6xS.png)