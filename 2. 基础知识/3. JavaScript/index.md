# JavaScript 高阶

JavaScript 高阶导航
## 页面跳转的几种方法

```javascript
1.
window.location.replace("www.baidu.com")
2.
window.location.href = 'www.baudu.com'
3.
window.history.go(-1)   //返回上一页
window.history.go(-2)   //返回上两页
window.history.go("www.baudu.com") //跳转
4.
window.history.back()   // 返回上一页
5.
window.history.forward()   //返回下一页
6.meta
<meta charset="utf-8" http-equiv="refresh" content="3;url=www.baidu.com"> //3秒后跳转到baidu
```


## 通过resize函数监听窗口变化，然后把fixed属性改为static即可解决
```javascript
var windheight = $(window).height();  /*未唤起键盘时当前窗口高度*/
$(window).resize(function(){
   var docheight = $(window).height();  /*唤起键盘时当前窗口高度*/        
   if(docheight < windheight){            /*当唤起键盘高度小于未唤起键盘高度时执行*/
      $(".submit").css("position","static");
   }else{
      $(".submit").css("position","fixed");
   }           
});
```