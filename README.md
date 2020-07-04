# Rating Component for Vue 2.x

一个简单，可高度定制化的基于 Vue 2.x 的评分组件

## 特性

- SVG icon 缩放不失真
- icon 颜色、大小自定义
- 自定义评分个数
- 支持纯展示的模式
- 支持显示小数评分
- 支持通过图片的自定义 icon
- 支持自定义图片 icon 的样式

## 安装和使用

### npm

`npm install rating` (暂时未发布)

在你的 APP 中引入 Rating (es6)

```javascript
import rate from 'rating'

Vue.use(rate)
```

在 template 中

```html
<rate v-modal="2" :count="5" />
```

## 关于 props 的选项

- `count {Number|String}`: 评分组件 item 展示的数量

```html
<rate :count="5" />
```

- `value {Number|String}`: 默认展示的分数，支持小数分数展示

```html
<rate v-modal="4.7" />
```

- `disabled {Boolean}`: 仅用于展示

```html
<rate :count="5" v-modal="4" disabled />
```

- `size {Boolean}`: svg icon 展示的大小 默认 40px

```html
<rate :count="5" v-modal="4" size="60" />
```

- `iconid {String}`: ID SVG icon 的 id,用于显示自定义 icon

插入 symbol icon 到你的代码中

```html
<symbol id="c-icon" class="icon" viewBox="0 0 32 32">
  <path
    d="M23.6 2c-3.363 0-6.258 2.736-7.599 5.594-1.342-2.858-4.237-5.594-7.601-5.594-4.637 0-8.4 3.764-8.4 8.401 0 9.433 9.516 11.906 16.001 21.232 6.13-9.268 15.999-12.1 15.999-21.232 0-4.637-3.763-8.401-8.4-8.401z"
  ></path>
</symbol>
```

绑定 icon id 到 rate 组件上

```html
<rate :count="5" iconid="c-icon" />
```

- `activeColor {String}`: icon 选中的颜色
- `inactiveColor {String}`: icon 未选时的颜色

```html
<rate v-model="4.2" :count="5" activeColor="#1500b0" inactiveColor="#7669d6" />
```

- `activeImage {String}`: 选中时的自定义图片
- `inactiveImage {String}`: 未选中时的自定义图片

```javascript
...
computed: {
  customImg() {
    return {
      default: require('./assets/img1.png'),
      active: require('./assets/img2.png')
    }
  }
}
...
```

```html
<rate
  v-model="4.2"
  :count="5"
  :activeImage="customImg.active"
  :inactiveImage="customImg.default"
/>
```

- `customImgStyle {Object}`: 自定义图片的样式

```html
<rate
  :count="5"
  v-modal="4"
  :activeImage="customImg.active"
  :inactiveImage="customImg.default"
  :customImgStyle="{
				width: '60px',
				height: '60px',
				margin: '0 10px'
			}"
/>
```

## Events

```javascript
new Vue({
  ...
  methods: {
    onAfterRate (rate) {
      alert(rate)
    }
  }
  ...
})
```

```html
<rate :count="5" v-model="4" @after-rate="onAftereRate" />
```
