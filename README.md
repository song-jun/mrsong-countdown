
# my-countdown

> A Vue.js project

## Build Setup

## 组件特色
# 年份倒计时
# 活动倒计时
# 列表循环倒计时

``` bash

# 使用方法
1.npm i mrsong-countdown -D
2.全局注册组件
import mrsongCountdown from 'mrsong-countdown'
Vue.component('mrsongCountdown',mrsongCountdown)
3.使用组件
<mrsong-countdown @sendData="getData" :isYear='true'>
    #自定义内容，自定义样式（数据是通过getData获取子组件的数据）
    <!-- <div>{{time.timeText}}</div> -->
</mrsong-countdown>
4.参数说明（参数可选）
activeTime:活动截止时间（String）;
isActivity：是否展示活动截止时间（true/false）;
isYear：是否展示年份倒计时（true/false）;
isList：是否展示列表倒计时（true/false）;
data:列表倒计时数据（Array）;
sendData: 向父组件传递数据;

# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build
```

For detailed explanation on how things work, consult the [docs for vue-loader](http://vuejs.github.io/vue-loader).
=======
# mrsong-countdown
倒计时
