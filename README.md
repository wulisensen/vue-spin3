# vue-spin3

> 基于ant design的vuejs loading组件

## Build Setup

``` bash
# 引入
import Spin3 from '**/spin3'

# 注册
Vue.component('Spin3', Spin3)

# 调用
<Spin3></Spin3>
```

## 参数

### String size
提供3个尺寸，默认不填为中，small，large

### String tip
loading时显示的文字，可以为空

### Boolean spinning
控制loading的开关

### Boolean noDot
不显示图标

## Demo

``` bash
# 正常调用
<Spin3 :spinning="loader" tip="加载图表中"></Spin3>

# 组件中加入内容，自动出蒙层
<Spin3 :spinning="loader">
  <div>
    ...
  </div>
</Spin3>
```

