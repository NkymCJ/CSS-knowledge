# CSS技巧和经验

### 1. 行内块元素(img、a等)之间(水平、垂直)产生的几像素间距问题

+ 方法1：设置为 ```img{display:block;}```

+ 方法2：垂直排放的话，设置为 ```img{vertical-align:top;}```

+ 方法3：(**建议**) 设置为 ```.parent{font-size:0;line-height:0;}```

+ 方法4：(**不建议**) 去掉html的行内块元素之间的空格，使它们紧挨着

### 2. 清除列表每行最右侧项的右边距

+ 方法1：使用 ```overflow:hidden``` 配合 **增加宽度** 或 **负边距(负边距也能够增加宽度)**，缺点是需要 **3层结构**

    示例：

    ```
    /* CSS */
    .test {
        width: 320px;
        overflow: hidden; /* 超出隐藏 */
    }

    .test ul {
        width: 330px; /* 增加宽度 */
        overflow: hidden; /* 闭合浮动 */
    }

    /* 或者采用以下方式 */
    .test ul {
        margin-right: -10px; /* 负边距 */
        overflow: hidden; /* 闭合浮动 */
    }

    .test ul li {
        float: left;
        height: 100px;
        width: 100px;
        background-color: #aaa;
        margin-right: 10px;
    }

    /* HTML */
    <div class="test">
        <ul>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
            <li></li>
        </ul>
    </div>
    ```

+ 方法2：(**建议 CSS3 IE9+**) 使用 ```ul:nth-child(Xn)``` 或 ```ul:nth-of-type(Xn)```，X为列表列数，优点是只需要 **2层结构**

    示例：
    
    ```
    /* CSS */
    ul {
        width: 320px;
        overflow: hidden; /* 闭合浮动 */
    }

    ul li {
        float: left;
        height: 100px;
        width: 100px;
        background-color: #aaa;
        margin-right: 10px;
    }

    ul li:nth-child(3n) {
        margin-right: 0;
    }

    /* HTML */
    <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
    </ul>
    ```

### 3. 浮动问题

1. **什么是浮动** 容器高度不能自动伸长以适应内容的高度，使得内容溢出到容器外面而影响(破坏)布局的现象。

    ![float](./images/float.png)

2. **产生浮动的原因** 容器高度为 auto 且 容器内有浮动元素(float:left/right)

3. **清除浮动**

    需了解概念：**clear** **BFC** **hasLayout**

    方法大致分为两种：1. 使用clear 2. 使父容器形成BFC(最好再触发hasLayout)

    + 方法1：使用 clear 的元素
        
        在容器内尾部插入带 ```clear:both``` 样式的空元素。方法简单，兼容性好，但是需要添加重复HTML元素，更改结构，不利于维护
        
        ```
        /* CSS */
        .left {float:left;}
        .box {height:200px;width:200px;background-color:#ccc;}

        .clear {
            clear:both; /* 关键 */
        }

        /* HTML */
        <div>
            <div class="left box">123</div>
            <div class="left box">456</div>
            <div class="clear"></div> <!-- 添加HTML元素 -->
        </div>
        ```

    + 方法2(**推荐**)：使用CSS的 overflow 属性

        使用 ```overflow:hidden``` 或 ```overflow:auto``` 生成BFC(Block Formatting Context)。为了兼容低版本IE(IE < 8)，还需要加入 ```zoom:1``` 用以触发hasLayout

        ```
        /* CSS */
        .left {float:left;}
        .box {height:200px;width:200px;background-color:#ccc;}

        .parent {
            overflow:hidden; /* 生成 BFC */
            zoom:1; /* IE < 8 触发 hasLayout */
        }

        /* HTML */
        <div class="parent">
            <div class="left box">box1</div>
            <div class="left box">box2</div>
        </div>
        ```

    + 方法3：父容器也设置浮动

        给浮动元素的父容器也添加上浮动属性即可清除内部浮动，但是这样会使其整体浮动，影响布局

        ```
        /* CSS */
        .left {float:left;}
        .box {height:200px;width:200px;background-color:#ccc;}

        /* HTML */
        <div class="parent2">
            <div class="parent1 left">
                <div class="left box">box1</div>
                <div class="left box">box2</div>
            </div>
        </div>
        // 分析：parent1有包裹，但parent2没有包裹
        ```

    + 方法4：使用邻接元素处理(与方法1原理相同)

        浮动元素后面的元素添加 ```clear:both``` 样式

        ```
        /* CSS */
        .left {float:left;}
        .box {height:200px;width:200px;background-color:#ccc;}

        /* HTML */
        <div>
            <div class="left box">float:left</div>
            <div class="left box">float:left</div>
            <div style="clear: both;">123</div>
        </div>

        ```

    + 方法5(**推荐**)：使用CSS的伪对象选择器

        使用 ```:after``` 在容器内部最后插入元素，为元素添加 ```clear:both``` 样式以清除浮动，同时为了兼容低版本IE(IE < 8)，设置容器 ```zoom:1``` 触发hasLayout

        使用 ```:before``` 是为了解决父子元素外边距合并问题

        写法1：

        ```
        /* CSS */
        .left {float:left;}
        .box {height:200px;width:200px;background-color:#ccc;}

        .clearfix:before , /* 解决父子元素外边距合并问题 */
        .clearfix:after {
            display: block;
            content: " ";
            height: 0;
            width: 0;
            font: 0/0 a; /* 字体大小/行高 字体 */
            visibility: hidden;
        }

        .clearfix:after {
            clear: both;
        }

        .clearfix {
            zoom: 1; /* IE < 8 触发 hasLayout */
        }

        /* HTML */
        <div class="clearfix">
            <div class="left box">float:left</div>
            <div class="left box">float:left</div>
        </div>
        ```

        写法2：(**更加简洁，Bootstrap使用的就是这种方式**)

        ```
        /* CSS */
        .left {float:left;}
        .box {height:200px;width:200px;background-color:#ccc;}

        .clearfix:before , /* 解决父子元素外边距合并问题 */
        .clearfix:after {
            content: " ";
            display: "table";
        }

        .clearfix:after {
            clear: both;
        }

        .clearfix {
            zoom: 1; /* IE < 8 触发 hasLayout */
        }

        /* HTML */
        <div class="clearfix">
            <div class="left box">float:left</div>
            <div class="left box">float:left</div>
        </div>
        ```

### 4. CSS Hack

1. 条件Hack

    待补充

2. 属性级Hack

    **\_** : 选择IE6及以下。(\-)亦可使用，为了避免与某些带中划线的属性混淆，所以使用下划线（\_）更为合适

    **\*** : 选择IE7及以下。诸如：(\+)与(\#)之类的均可使用，不过业界对(\*)的认知度更高

    **\\9** : 选择IE6+

    **\\0** : 选择IE8+和Opera15以下的浏览器

3. 选择符级Hack

    待补充

### 5. CSS 垂直外边距合并问题(父子元素之间、兄弟元素之间)

1. 父子元素之间

    ![Father-sonMarginMerge](./images/Father-sonMarginMerge.png)

    - 代码：

        ```
        /* CSS */
        .box {height: 50px;width: 50px;line-height: 50px;}
        .parent{height: 120px;width: 120px;}

        .box{
            margin-top: 20px; /* 设置子元素的外边距 */
        }

        /* HTML */
        <div class="parent">
            <div class="box"></div>
        </div>
        ```

    - 原因：子元素外边距传递给父元素

    - 解决方法：

        + 使父容器形成BFC(最好再触发hasLayout) 略
    
        + 使用 ```:before``` / ```:after``` 隔开父与第一个/最后一个子元素，阻止传递

            ```
            /* CSS */
            parent:after ,
            parent:before {
                display: "table";
                content: " ";
            }
            ```

2. 兄弟元素之间
