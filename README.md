# F2 微信小程序

F2 的微信小程序版本，支持原生 [F2](https://f2.antv.vision/) 的所有功能，欢迎使用反馈。

## 快速体验

- 微信扫码体验

![](https://gw.alipayobjects.com/zos/rmsportal/wmRJtPHkkoimGbPCeScc.jpg#align=left&display=inline&height=344&originHeight=344&originWidth=344&status=done&style=none&width=344)

- 使用微信开发者工具打开此项

## 说明
为了方便使用，我们封装了微信小程序的自定义组件，故需要微信小程序支持使用 npm 安装第三包。<br />**重要：版本要求**

1. 小程序基础库版本 2.7.0 或以上
1. 开发者工具 1.02.1808300 或以上开始，小程序支持使用 npm 安装第三方包。


## 如何使用
### 1. 安装依赖
项目默认初始化出来的是没有`package.json`的，需要新增`package.json`后再安装

```bash
## 没有package.json时执行下面这段
## echo "{}" > package.json

npm install @antv/wx-f2 --save
```

安装好依赖包之后，点击工具顶部菜单栏的详情：

![](https://gw.alipayobjects.com/zos/rmsportal/sAYeeUhRjrchjvJONsvp.png#align=left&display=inline&height=314&originHeight=314&originWidth=582&status=done&style=none&width=582)

勾选“使用 npm 模块”选项：

![](https://gw.alipayobjects.com/zos/rmsportal/NLCSaOYDPNQVaIAZBoiC.png#align=left&display=inline&height=1596&originHeight=1596&originWidth=1054&status=done&style=none&width=1054)

最后点击开发者工具中的菜单栏：工具 --> 构建 npm 即可运行。

![](https://gw.alipayobjects.com/zos/rmsportal/kORAowbzpNioXseBQoxC.png#align=left&display=inline&height=746&originHeight=746&originWidth=392&status=done&style=none&width=392)

如果碰到 **@babel/runtime 未找到npm包入口文件**，直接忽略就行了，不影响使用（强迫症碍眼的话，手动删除`node_modules/@babel/runtime`目录）
```bash
rm -rf node_modules/@babel/runtime
```
![](https://gw.alipayobjects.com/zos/finxbff/compress-tinypng/8997fffd-f9e4-45e4-b773-45f85e33f2f2.jpg)

### 2. 使用自定义组件
#### 1. 打开json文件，引入组件
```json
{
  "usingComponents": {
    "f2": "@antv/wx-f2"
  }
}
```

#### 2. wxml 使用组件
```xml
 <f2 class="f2" data="{{data}}" bind:draw="draw" />
```

#### 3. wxss 设置宽高
```css
.f2 {
  width: 100%;
  height: 500rpx;
}
```

#### 4. 实例化图表
```js
Page({
  data: {
    data:[
      { value: 123, type: '运行指数', date: '10/01' },
      { value: 62, type: '历史均值', date: '10/01' },
      { value: 212, type: '运行指数', date: '10/02' },
      { value: 59, type: '历史均值', date: '10/02' },
      { value: 53, type: '运行指数', date: '10/03' },
      { value: 210, type: '历史均值', date: '10/03' },
      { value: 162, type: '运行指数', date: '10/04' },
      { value: 1, type: '历史均值', date: '10/04' }
    ]
  },
  draw ({ detail: { chart, data } }) {
    chart.source(data, {
      date: {
        range: [0.05, 0.95]
      }
    })
    chart.legend('type', {
      align: 'right',
      itemWidth: 80
    })
    chart.line().shape('smooth').position('date*value').color('type', ['#de5341', '#4a81ed'])
    chart.area().shape('smooth').position('date*value')
      .color('type', ['l(90) 0:#de5341 1:#ffffff', 'l(90) 0:#4a81ed 1:#ffffff'])

    // 无需render
  }
});
```
## 组件 API
### Props

|参数|说明|类型|默认值|
|:-|:-|:-|:-|
|data|数据源(修改data会自动更新图表)|Array|[]|
|padding|图表绘图区域和画布边框的间距|String/Number/Array|"auto"|
|append-padding|图表画布区域四边的预留边距|Number/Array|0|

### Events

|事件名|说明|
|:-|:-|
|init|F2初始化|
|draw|chart绘制|
|reload|chart绘制完成|
|update|数据更新|

## f2 API

- F2 API 参见：[https://f2.antv.vision/zh/docs/api/f2](https://f2.antv.vision/zh/docs/api/f2)

## 如何贡献

如果您在使用的过程中碰到问题，可以先通过 [issues](https://github.com/antvis/wx-f2/issues) 看看有没有类似的 bug 或者建议。

## License

[MIT license](https://github.com/antvis/wx-f2/blob/master/LICENSE)
