
## 盒模型

- content
- padding
- border
- margin

## BFC

块级格式化上下文，独立的渲染区域，处于 BFC 内部的元素与外部元素相互隔离，内外元素定位不回相互影响

触发条件
- 根元素
- `position:absolute/fixed`
- `display:inline-block/table`
- `float`
- `ovevflow !== visible`
规则：
- 同一个 BFC 内的元素 `margin`会重叠
- 不会和 `float` 元素区域重叠
- BFC 高度会计算浮动子元素的高度
- 文字层不会被浮动元素覆盖，环绕周围
应用
- 阻止`margin`重叠
- 清除浮动
- 自适应两栏布局
- 阻止元素被浮动元素覆盖

## 层叠上下文

相当于三位世界中的`z`轴

## 左右居中

- `text-align:center`
- `margin: 0 auto`
- `table` 布局
- `position` 定位 + `transfrom`

## 垂直居中

- `position` 定位 + `transfrom`
- `vertical-align: middle;`

## 清除浮动

- `clear:both` - 浮动元素末尾的元素添加
- `overflow:hidden`/`auto` - 利用BFC

## 经典布局

- 圣杯


## 其他

**transition和animation的区别** - 前者之后两帧


