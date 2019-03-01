# CSS制作图形

4个属性的方向为: 上 右 下 左 （逆时针）

### 制作三角形

**通过控制 四边形 的 4 个方向的 border 来实现**

![四边形](./四边形.jpg)

**三角形 箭头 的朝向决定取 无宽高的四边形的四块border三角形的 相反 方向块**

**三角形 顶点 的 左右/上下 距离取决于 四边形 左右/上下 border的宽度**

**不需要的border颜色设为 transparent，style设为 dashed(兼容IE6)**

**其他默认设置为 height: 0;width: 0;font-size: 0;line-height: 0;overflow: hidden;**

1. 例：一个箭头向上的等腰三角形，底50px，高50px，颜色为#3366ff。

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
    // 因为箭头向上，所以取无宽高的四边形的四块border三角形的下块，又因为题目三角形高为50px，所以上border为0，下border的宽度为50px。
    // 因为题目三角形为等腰三角形，所以顶点在中间，所以四边形左右border宽度都为25px。
    // 因为箭头向上，所以三角形底边为四边形的下边border，所以四边形上左右border都为透明色。
    ```

2. 例：一个箭头向上的非等腰三角形，底50px，高50px，顶点左边40px，顶点右边10px，颜色为#3366ff。
   
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
    // 因为箭头向上，所以取无宽高的四边形的四块border三角形的下块，又因为题目三角形高为50px，所以上border为0，下border的宽度为50px。
    // 因为题目三角形顶点左边40px，顶点右边10px，所以四边形左border的宽度为40px，右border的宽度为10px。
    // 因为箭头向上，所以三角形底边为四边形的下边border，所以四边形上左右border都为透明色。
    ```

3. 例：对角线三角形。一个右下的三角形，即直角三角形，底50px，高50px。
   
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
    // 因为箭头向上，所以取无宽高的四边形的四块border三角形的下块，又因为题目三角形高为50px，所以上border为0，下border的宽度为50px。
    // 因为题目三角形顶点在四边形的右上角顶点，所以四边形左border的宽度为50px，右border的宽度为0。
    // 因为箭头向上，所以三角形底边为四边形的下边border，所以四边形上左右border都为透明色。
    ```