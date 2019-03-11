# CSS视口相关

### visual viewport 视觉视口

用户正在看到的网站的区域，也就是移动设备物理屏幕的可视区域，不同设备不同尺寸

![visualViewport](../images/visualViewport.png)

### layout viewport 布局视口

1. 早期，由于移动设备屏幕太小，不能很好地访问网页

2. 后来，**移动设备的浏览器** 都 **默认设置** 了一个 **viewport meta标签**，定义一个虚拟的 **布局视口(layout viewport)**，用于解决页面在移动端的显示问题。大部分移动端浏览器都将这个设置为 **980px**，所以PC上的网页基本能在手机上呈现，只不过元素看上去很小，一般默认可以通过手动缩放网页 (Apple 首先提出)

![layoutViewport](../images/layoutViewport.png)

### ideal viewport 理想视口(完美视口)

1. **类似布局视口**，但 **宽度和视觉视口相同**

2. 通过 **配置 viewport meta标签 来设置 layout viewport 达到 ideal viewport**

    属性名|值|说明
    --|:--:|--
    width|正整数或device-width|定义视口的宽度，单位为像素
    height|正整数或device-height|定义视口的高度，单位为像素
    initial-scale|[0.0-10.0]|定义初始缩放值
    minimum-scale|[0.0-10.0]|定义缩小最小比例，它必须小于或等于maximum-scale设置
    maximum-scale|[0.0-10.0]|定义放大最大比例，它必须大于或等于minimum-scale设置
    user-scalable|yes/no|定义是否允许用户手动缩放页面，默认值yes

    > width：如果不指定该属性(或移除 viewport meta 标签)，则 layout viewport 宽度为厂商默认值(大部分为 980px)。如果设置为 device-width，则此时 layout viewport 就是 ideal viewport，因为宽度与设备 visual viewport 宽度一致了。

        <meta name="viewport" content="width=device-width" />

    > initial-scale：如果将页面缩放比例设置为1，也可以得到 ideal viewport

        <meta name="viewport" content="initial-scale=1.0" />