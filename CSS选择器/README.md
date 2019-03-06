# CSS选择器

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

4. 伪类选择器(Pseudo-Classes Selectors)

    + 超链接的4种状态：E:link E:visited E:hover E:active

        - E:link 设置超链接 **未被访问前** 的样式

        - E:link 设置超链接在其链接地址 **已被访问过** 时的样式

        - E:link 设置超链接在其 **鼠标悬停** 时的样式

        - E:link 设置超链接在被用户激活（在 **鼠标点击与释放之间** 发生的事件）时的样式

        - 正确的书写顺序：l(link)ov(visited)e  h(hover)a(active)te 即 **love hate**
    
    + 打印：@page :first @page :left @page :right

    + E:not(s) (IE9+)：匹配 **不含有s选择器** 的E元素

        - 示例：

            ```
            /* 给列表中除最后一项外的所有列表添加一条底边 */
            .demo li:not(:last-child) {
                border-bottom: 1px solid #ddd;
            }
            ```

    + E:root (IE9+)：匹配 **E元素在文档的根元素**。在HTML中，**根元素永远是HTML**

    + E:empty (IE9+)：匹配 **没有任何子元素(包括text节点)** 的元素E

        - 主要用于 显示购物车 或者 数字
    
    + E:checked (IE9+)：匹配 **处于选中状态** 的元素E。(**radio** 与 **checkbox**)

    + E:enabled (IE9+) / E:disabled (IE9+)：匹配处于 **可用状态/不可用状态** 的元素E

    + E:target (IE9+)：匹配 **URL指向** 的E元素

    + E:first-child / E:last-child (IE9+)：匹配 **父元素** 的 **第一个/最后一个** 子元素E

       - E元素必须是某个元素的子元素 且 其父元素的 第一个/最后一个 子元素必须是E元素。

       - 如果 第一个/最后一个 子元素不是E元素，则无效

    + E:only-child (IE9+)：匹配 **父元素仅有的一个子元素E**
        
        - 必须是某个元素的子元素 且 该父元素 仅有 它一个子元素
    
    + E:nth-child(n) (IE9+)/ E:nth-last-child(n) (IE9+)：匹配 **父元素** 的 **第n个/倒数第n个** 子元素E

        - 使用 乘法因子(Xn+Y) 作为换算方式，X为计数器，Y为偏移量，可以是0、1、2..，所以(2n)偶数，而(2n+1)奇数

        - 可以使用关键字，如 **odd** (奇数)、**even** (偶数)

        - 如果 此位置下的子元素 不是E元素，则无效

    + E:first-of-type (IE9+)/ E:last-of-type (IE9+)：匹配 **父元素下** 的 **第一个/最后一个 类型为E** 的子元素

        - 排在父元素 第一/最后一个元素 不一定 是E元素，第一/最后一个E元素 可能存在于子元素列表中的 任何位置

    + E:only-of-type (IE9+)：匹配 **父元素** 的 所有子元素中 **唯一的** 那个子元素E

        - 父元素可以有多个子元素，但 其中类型为E 的元素只能有一个
    
    + E:nth-of-type(n) (IE9+)/ E:nth-last-of-type(n) (IE9+)：匹配 **父元素** 的 **第n个/倒数第n个 类型为E** 的子元素

        - 使用 乘法因子(Xn+Y) 作为换算方式，X为计数器，Y为偏移量，可以是0、1、2..，所以(2n)偶数，而(2n+1)奇数

        - 可以使用关键字，如 **odd** (奇数)、**even** (偶数)

        - 匹配的是 类型为E 的 第n个/倒数第n个，不是 位置上 的 第n个/倒数第n个

5. 伪对象选择器(Pseudo-Element Selectors) 

    + CSS3将 伪对象选择器前面的 **单个冒号(:)** 修改为 **双冒号(::)** 用以区别伪类选择器，但以前的写法仍然有效，所以为了兼容，最好还是使用 **单个冒号(:)** 的写法

    + 本质上并不支持伪元素的双冒号(::)写法，而是忽略掉了其中的一个冒号，仍以单冒号来解析，所以等同变相支持了E::first-letter

    + E:first-letter / E::first-letter：设置 **对象内** 的 **第一个字符** 的样式

        - 此伪对象仅作用于 **块对象**。内联对象要使用该伪对象，必须先将其设置为块级对象

        - 该伪类常被用来配合 **font-size属性** 和 **float属性** 制作 **首字下沉效果**

            示例：

            ```
            /* CSS */
            p {
                width: 200px;
                padding: 5px 10px;
                border: 1px solid #ddd;
                font:14px/1.5 simsun,serif,sans-serif;
            }

            p:first-letter {
                float: left;
                font-size: 40px;
                font-weight: bold;
                line-height: 1;
            }

            p::first-letter {
                float: left;
                font-size: 40px;
                font-weight: bold;
                line-height: 1;
            }
            /* HTML */
            <p>今天，阳光明媚，晴空万里，
            非常适合户外活动，如踏青、远足之类的。
            长期坐在办公室的同学们要多注意运动。</p>
            ```

        - IE6 在使用该选择符时有个显式的BUG：**选择符** 与 **包含规则的花括号** 之间不能紧挨着，需 **留有空格或换行**
    
    + E:first-line / E::first-line：设置 **对象内** 的 **第一行** 的样式

        - 此伪对象仅作用于 **块对象**。内联对象要使用该伪对象，必须先将其设置为块级对象

        - IE6 在使用该选择符时有个显式的BUG：**选择符** 与 **包含规则的花括号** 之间不能紧挨着，需 **留有空格或换行**

    + E:before / E::before：设置在 **对象前(依据对象树的逻辑结构)** 发生的内容。用来和 **content属性** 一起使用，并且 **必须定义content属性**

        - 不支持设置属性position、float、list-style-*和一些display值，Firefox3.5开始取消这些限制

        - IE10在使用伪元素动画有一个问题，需要使用一个空的:hover来激活

    + E:after / E::after：设置在 **对象后(依据对象树的逻辑结构)** 发生的内容。用来和 **content属性** 一起使用，并且 **必须定义content属性**

        - 不支持设置属性position、float、list-style-*和一些display值，Firefox3.5开始取消这些限制

        - IE10在使用伪元素动画有一个问题，需要使用一个空的:hover来激活

    + E::placeholder：设置 **对象文字占位符** 的样式

        - 默认的文字占位符为 **浅灰色**

        - 除了 Firefox 是 **::[prefix]placeholder**，其他浏览器都是使用 **::[prefix]input-placeholder**

        - ::-moz-placeholder 伪对象在Firefox 19+替代了之前的 :-moz-placeholder 伪类

        - Firefox支持该伪元素使用text-overflow属性来处理溢出问题

        - 示例：

            ```
            <input type="text" placeholder="占位符" />

            input::-webkit-input-placeholder {
                color: #999;
            }
            input:-ms-input-placeholder { // IE10+
                color: #999;
            }
            input:-moz-placeholder { // Firefox4-18
                color: #999;
            }
            input::-moz-placeholder { // Firefox19+
                color: #999;
            }
            ```