# CSS Layout

## 传统技术

基于盒状模型，依赖 display 属性 + position 属性 + float 属性。

## 现代工具

### Flex

![flex_terms.png](https://developer.mozilla.org/files/3739/flex_terms.png)

上图解释了当元素布局为 flex 时，它默认有两条轴：

- 子项（flex item） 排列方向上的轴称为主轴，与之垂直方向上的轴是交叉轴。主轴的开始和结束被称为 `main start` 和 `main end`，交叉轴的开始和结束被称为 `cross start` 和 `cross end`，子项在主轴方向的大小称 `main size`，在交叉轴上的大小称为`cross size`
- 设置了 `display: flex` 的父元素被称为 flex 容器（flex container）
- 在 flex 容器中的元素被称为 flex 子项（flex item）

#### Flex Container 的 6 个属性

1. flex-direction

   设置主轴方向

   ```js
   // 可选值
   row | row-reverse | column | column-reverse
    
   // 默认值
   row
   ```

2. flex-wrap

   设置子项是否自动换行

   ```js
   // 可选值
   nowrap | wrap | wrap-reverse 
    
   // 默认值
   nowrap
   ```

3. flex-flow

   flex-direction 和 flex-wrap 的组合

   ```js
   // 可选值
   <'flex-direction'> || <'flex-wrap'>
    
   // 默认值
   row nowrap
   ```

4. justify-content

   设置所有子项在主轴上的对齐方式

   ```js
   // 可选值
   stretch | center | flex-start | flex-end | space-between | space-around
    
   // 默认值
   stretch
   ```

5. align-items

   设置单个子项在交叉轴上的对齐方式

   ```js
   // 可选值
   stretch | center | flex-start | flex-end | baseline
   
   // 默认值
   stretch
   ```

6. align-contents

   设置多根轴（交叉轴）线的对齐方式

   ```js
   // 可选值
   stretch | center | flex-start | flex-end | space-between | space-around
   
   // 默认值
   stretch
   ```

#### Flex Item 的 6 个属性

1. flex-grow

   设置子项的扩展因子

   ```js
   // 可选值
   number | initial | inherit
    
   // 默认值
   0
   ```

2. flex-shrink

   设置子项的收缩因子

   ```js
   //可选值
   number | initial | inherit
    
   // 默认值
   1
   ```

3. flex-basis

   设置子项的初始 main size 值，**优先于 width/height 值**

   ```js
   // 可选值
   number | auto | initial | inherit
    
   // 默认值
   auto
   ```

4. flex

   flex-grow、flex-shrink 以及 flex-basis 的组合

   ```js
   // 可选值
   none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
    
   // 默认
   0 1 auto
   ```

5. align-self

   设置单个子项在交叉轴上的对齐方式，可覆盖 Flex Container 的 align-items 属性

   ```js
   // 可选值
   stretch | center | flex-start | flex-end | space-between | space-around
   
   // 默认值
   auto
   ```

6. order

   设置子项出现的顺序

   ```js
   // 可选值
   number | initial | inherit
   
   // 默认值
   0
   ```

### Grid

[MDN CSS layout]: https://developer.mozilla.org/en-US/docs/Learn/CSS/CSS_layout
[阮一峰老师的 CSS Flex 布局教程]: http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html
[阮一峰老师的 CSS Grid 网格布局教程]: http://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html
[RUNOOB CSS flex 属性]: https://www.runoob.com/cssref/css3-pr-flex.html







