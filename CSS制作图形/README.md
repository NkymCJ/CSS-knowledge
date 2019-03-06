# CSS制作图形

4个属性的方向为: 上 右 下 左 （逆时针）

### 制作三角形

![border四边形](./images/border四边形.jpg)

**通过控制 border四边形 的 4 个方向的 border 来实现**

**三角形 箭头 的朝向决定取 无宽高的border四边形的四块border三角形的 相反 方向块**

**三角形 顶点 的 左右/上下 距离取决于 border四边形 左右/上下 border的宽度**

**不需要的border颜色设为 transparent，style设为 dashed(兼容IE6，因为IE6下 transparent 属性无效)**

其他默认设置为 **height: 0;width: 0;font-size: 0;line-height: 0;overflow: hidden;**

1. 例：等腰三角形。箭头向上，底50px，高50px，颜色为#3366ff。

    ![三角形1](./images/三角形1.png)

    ```
    height: 0;
    width: 0;
    overflow: hidden;
    font-size: 0;
    line-height: 0;
    border-color: transparent transparent #3366ff transparent;
    border-style: dashed dashed solid dashed;
    border-width: 0 25px 50px 25px;

    // 分析：
    // 因为箭头向上，所以取无宽高的border四边形的四块border三角形的下块，
    // 又因为题目三角形高为50px，所以上border为0，下border的宽度为50px。
    // 因为题目三角形为等腰三角形，所以顶点在中间，所以border四边形左右border宽度都为25px。
    // 因为箭头向上，所以三角形底边为border四边形的下边border，所以border四边形上左右border都为透明色。
    ```

2. 例：非等腰三角形。箭头向上，底50px，高50px，顶点左边40px，顶点右边10px，颜色为#3366ff。
   
    ![三角形2](./images/三角形2.png)

    ```
    height: 0;
    width: 0;
    overflow: hidden;
    font-size: 0;
    line-height: 0;
    border-color: transparent transparent #3366ff transparent;
    border-style: dashed dashed solid dashed;
    border-width: 0 10px 50px 40px;

    // 分析：
    // 因为箭头向上，所以取无宽高的border四边形的四块border三角形的下块，
    // 又因为题目三角形高为50px，所以上border为0，下border的宽度为50px。
    // 因为题目三角形顶点左边40px，顶点右边10px，所以border四边形左border的宽度为40px，右border的宽度为10px。
    // 因为箭头向上，所以三角形底边为border四边形的下边border，所以border四边形上左右border都为透明色。
    ```

3. 例：对角线三角形。直角三角形，底50px，高50px，颜色为#3366ff。
   
    ![三角形3](./images/三角形3.png)

    ```
    height: 0;
    width: 0;
    overflow: hidden;
    font-size: 0;
    line-height: 0;
    border-color: transparent transparent #3366ff transparent;
    border-style: dashed dashed solid dashed;
    border-width: 0 0 50px 50px;

    // 分析：
    // 因为箭头向上，所以取无宽高的border四边形的四块border三角形的下块，
    // 又因为题目三角形高为50px，所以上border为0，下border的宽度为50px。
    // 因为题目三角形顶点在border四边形的右上角顶点，所以border四边形左border的宽度为50px，右border的宽度为0。
    // 因为箭头向上，所以三角形底边为border四边形的下边border，所以border四边形上左右border都为透明色。
    ```

4. 例：气泡框。等腰三角指示在右边框上。

    ![气泡框1](./images/气泡框1.png)

5. 例：气泡框。直接三角指示在右边框上。

    ![气泡框2](./images/气泡框2.png)

6. 例：气泡框。斜三角指示在右边框上。

    ![气泡框3](./images/气泡框3.png)

    ```
    .bubble {
        position: relative;
        width: 200px;
        height: 100px;
        border: 5px solid #3366ff;
        border-radius: 15px;
    }
    .bubble3::before {
        content: "";
        position: absolute;
        bottom: -5px;
        right: -45px;
        height: 0;
        width: 0;
        overflow: hidden;
        font-size: 0;
        line-height: 0;
        border-color: transparent transparent #3366ff transparent;
        border-style: dashed dashed solid dashed;
        border-width: 0 40px 40px 0;
    }
    .bubble3::after {
        content: "";
        position: absolute;
        bottom: -5px;
        right: -45px;
        height: 0;
        width: 0;
        overflow: hidden;
        font-size: 0;
        line-height: 0;
        border-color: transparent transparent #ffffff transparent;
        border-style: dashed dashed solid dashed;
        border-width: 0 40px 20px 0;
    }
    // 分析：
    // 三角形由两个三角形叠加形成
    ```