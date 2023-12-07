# C006-css实现三角形★.html
```
<!DOCTYPE html>
<html>
	<head>
		<meta charset="utf-8">
		<title></title>
	</head>
	<style type="text/css">
		.trangle-top {
			width: 0;
			height: 0;
			border:50px solid transparent;
			border-bottom-color: red;
		}
		.trangle-bottom {
			width: 0;
			height: 0;
			border:50px solid transparent;
			border-top-color: red;
		}
		.trangle-left {
			width: 0;
			height: 0;
			border:50px solid transparent;
			border-right-color: red;
		}
				.trangle-right {
			width: 0;
			height: 0;
			border:50px solid transparent;
			border-left-color: red;
		}
	/* 	.tra-top {
			width: 0;
			height: 0;
			border-left:50px solid red;
			border-right:50px solid #333;
			border-bottom:50px solid green;
		} */
		
		
		
		.tra-left-top {
			width: 0;
			height: 0;
			border-left:50px solid red;
			border-right:50px solid #fff;
			border-bottom:50px solid #fff;
		}
				.tra-right-top {
			width: 0;
			height: 0;
			border-left:50px solid #fff;
			border-right:50px solid red;
			border-bottom:50px solid #fff;
		}
		.tra-left-bottom {
			width: 0;
			height: 0;
			border-left:50px solid red;
			border-right:50px solid #fff;
			border-top:50px solid #fff;
		}
		.tra-right-bottom {
			width: 0;
			height: 0;
			border-left:50px solid #fff;
			border-right:50px solid red;
			border-top:50px solid #fff;
		}
	</style>
	<body>
		<!-- 向上的三角形 -->
		<div class="trangle-top">
			
		</div>
	
		<!-- 向左的三角形 -->
		<div class="trangle-left">
			
		</div>
					<!-- 向下的三角形 -->
		<div class="trangle-bottom">
			
		</div>
		
				<!-- 向右的三角形 -->
		<div class="trangle-right">
			
		</div>
		
		
		
		
		<!-- 直角三角形 直角在左上--> 
		<div class="tra-left-top">
			
		</div>
				<!-- 直角三角形 直角在右上--> 
		<div class="tra-right-top">
			
		</div>
				<!-- 直角三角形 直角在左下--> 
		<div class="tra-left-bottom">
			
		</div>
				<!-- 直角三角形 直角在右下--> 
		<div class="tra-right-bottom">
			
		</div>
		
	</body>
</html>
```



向上的 等腰 三角形


```
.box {
  width:0;
  height:0;
  border-left:50px solid transparent;
  border-right:50px solid transparent;
  border-bottom:100px solid red;
}
```


等边三角形呢？

对于等边三角形我们知道，高是边的sqrt(3)/2倍，所以如果高为40的话，两边就是差不多23

```
.triangle {
				border-left: 23px solid transparent;  
				border-right: 23px solid transparent;  
				border-bottom: 40px solid red;  
				width: 0px;
				height: 0px;
			}
```
