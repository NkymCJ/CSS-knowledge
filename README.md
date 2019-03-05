# CSS-knowledge

CSS知识

CSS Cascading Style Sheet 层叠样式表

### CSS 三大特性：继承 层叠 优先级

1. 继承

    设置 上级(父级) 的 CSS 样式，上级(父级) 及以下的 子级(下级、后代) 都具有此属性

    并不是所有的属性都可以继承，可以继承的属性主要以 **color / font- / text- / line-** 开头，还有 **visibility、cursor** 等

    特殊情况：

    a标签 的 文字颜色 和 下划线 是不能继承的

    h标签 的 文字大小 是不能继承的

    text-decoration 是不能继承的

    vertical-align 是不能继承的

    内联元素不能继承 text-align text-indent

2. 层叠

    层叠性只有在多个选择器选中同一个标签, 然后又设置了相同的属性, 才会发生层叠(后者覆盖前者)

3. 优先级

    当多个选择器选中同一个标签, 并且给同一个标签设置相同的属性时, 如何层叠就由优先级来确定

    **!important > 行内样式 > ID选择器 > 类选择器 > 标签 > 通配符 > 继承 > 浏览器默认属性**

    看样式：

    + 看是否命中对应的标签
    
    + 根据权重，即 **比较标签的数量**。通过比较 **ID、类、标签** 这三种选择器的数量来决定谁的优先级最高。当数量相同时，通过层叠来决定

### CSS 选择器

1. 元素选择器

    通配符(*) 类型选择器(E) ID选择器(E#id) 类选择器(E.class)

2. 关系选择器

    + 包含选择器(E F)
    
    + 子选择器(E>F)

    + 相邻选择器(E+F)：**选择与E元素同级** 且 **紧挨着E元素** 的第一个F元素

    + 兄弟选择器(E~F)：**选择与E元素同级** 的 **所有** F元素

3. 属性选择器

    + E[attr]：具有attr属性的E元素

    + E[attr="val"]：具有att属性 且 **属性值等于val** 的E元素

    + E[attr^="val"]：具有att属性 且 **属性值为以val开头的字符串** 的E元素

    + E[attr$="val"]：具有att属性 且 **属性值为以val结尾的字符串** 的E元素

    + E[attr*="val"]：具有att属性 且 **属性值为包含val的字符串** 的E元素

    + E[attr|="val"]：具有att属性，其值是 **以val开头并用连接符"-"分隔的字符串** 的E元素；如果 **值仅为val**，也将被选择

    + E[attr~="val"]：具有att属性 且 属性值为 **用空格分隔的字词列表**，**其中一个等于val** 的E元素(包含只有一个值且该值等于val的情况)

4. 伪类选择器

    + 超链接的4种状态：E:link E:visited E:hover E:active

        - E:link 设置超链接 **未被访问前** 的样式

        - E:link 设置超链接在其链接地址 **已被访问过** 时的样式

        - E:link 设置超链接在其 **鼠标悬停** 时的样式

        - E:link 设置超链接在被用户激活（在 **鼠标点击与释放之间** 发生的事件）时的样式

        - 正确的书写顺序：l(link)ov(visited)e  h(hover)a(active)te 即 **love hate**
    
    + 打印：@page :first @page :left @page :right

    + E:not(s)：匹配 **不含有s选择器** 的E元素

        示例：

        ```
        /* 给列表中除最后一项外的所有列表添加一条底边 */
        .demo li:not(:last-child) {
            border-bottom: 1px solid #ddd;
        }
        ```

    + E:root：匹配E元素在文档的根元素。在HTML中，**根元素永远是HTML** 

    + E:empty：
