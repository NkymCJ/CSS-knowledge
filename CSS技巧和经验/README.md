# CSS技巧和经验

### 1. 行内块元素(img、a等)之间(水平、垂直)产生的几像素间距问题

+ 方法1：设置为 ```img{display:block;}```

+ 方法2：设置为 ```img{vertical-align:top;}```

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
        /* 或者 负边距 margin-right: -10px; */
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

+ 方法2：(**建议 CSS3 IE9+**) 使用 ```ul:nth-child(Xn)``` 或 ```ul:nth-of-type(Xn)```，X为列表列数，只需要 **2层结构**

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

