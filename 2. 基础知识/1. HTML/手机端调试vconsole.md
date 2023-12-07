
# 为什么使用vconsole呢？
>因为手机或者平板之类的客户端软件并没有控制台，前端开发想看log日志比较麻烦，如果一直弹窗alert方法实在太挫了。所以腾讯开发了这个 js 插件。

#使用方法

## 方法1：

```
<script src="https://qdleader.github.io/qdleader/h5/vconsole.js"></script>
//或使用cdn链接 <script src="https://cdn.bootcss.com/vConsole/3.3.4/vconsole.min.js"></script>
<script>
    // init vConsole
    var vConsole = new VConsole();
    console.log('Hello world');
</script>

```



## 方法2：


# 安装
```
npm install vconsole

```
# 引入

```
import VConsole from 'vconsole';

const isDebug = true;
// 本地开发调试注入vConsole
if (isDebug) {
    new VConsole();
}
```




其他类似工具Eruda


## h5字体不局中，有时候会被切掉一块
当我们写h5时候，加上了line-height和height一致，
但是还是会碰到andriod 有的机型，如有overflow：hidden会是被切掉头部一两个像素情况
设置line-height 也不生效
解决：
display:flex;
align-items:center; 或 align-items:baseline;


## 1px 像素起因
原因很简单——CSS 中的 1px 并不能和移动设备上的 1px 划等号。它们之间的比例关系有一个专门的属性来描述：
```javascript
// 设备像素比
window.devicePixelRatio = 设备的物理像素 / CSS像素
```