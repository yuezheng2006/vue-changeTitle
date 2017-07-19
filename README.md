### 作用
Vuejs 主要解决ios端微信标题不能通过 document.title = xxx 的方式修改 兼容android
功能比较简单  没有发布到npm  如需使用拉下来放到自己项目里面使用就OK了

### 原理
参照链接(https://www.zhihu.com/question/26228251）

#### ES6
> main.js

```js
import changeTitle form 'vue-changeTitle/index.js'
Vue.use(changeTitle)
```
> 路由定义示例

```js
// ...
const routes = [
  {
    name: 'homePage',
    path: '/home',
    meta: {
      title: '首页'
    },
    component: require('../views/Home.vue')
  },
  {
    name: 'page1',
    path: '/page1',
    meta: {
      title: '路由页面1'
    },
    component: require('../views/page1.vue')
  },
  {
    name: 'page2',
    path: '/page2',
    meta: {
      title: '路由页面2'
    },
    component: require('../views/page2.vue')
  }
]
// ...
```

> 使用可采用v-wechat-title形式亦可采用this.$changeTitle(xxx)的形式调用

App.vue **建议全局只使用一次该指令 标题可用vuex或者router中定义 不要多处使用!!**

```html
<!-- 任意元素中加 v-wechat-title 指令 建议将标题放在 route 对应meta对象的定义中 -->
<div v-wechat-title="$route.meta.title"></div>
<!--or-->
<router-view v-wechat-title="$route.meta.title"></router-view>
```

> 自定义加载的图片地址 默认是 ./favicon.ico 可以是相对或者绝对的 只要是一个可以访问到的图片地址(最好是小图地址）

```html
<div v-wechat-title="$route.meta.title" img-set="/static/logo.png"></div>
```
