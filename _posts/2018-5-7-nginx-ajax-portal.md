---
categories: software
tags: [webServer] 	
---
# web site structure
to build a website with high performance
![web_struct1](/assets/img/web_struct1.png)

# nginx
## install nginx
```sh
#ubuntu16.04 lts

``` 
## nginx setting
```sh
#ubuntu16.04 lts

# proxy

# balance

```

# static page
## tools
1. https://www.zhihu.com/question/19561454
2. http://jsbin.com/?html,output

## features
1. top nav fix , would always show however scroll up or down
2. left nav menu column would show if width >1024
3. content would flow in blocks
4. there is an introduce board in head of page ,

## html code 
```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width">
<script src="https://code.jquery.com/jquery.min.js"></script>
<link
	href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css"
	rel="stylesheet" type="text/css" />
<script
	src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>

<title>JS Bin</title>
</head>
<body>
	<div class="container-fluid">
		<div class="row nav">nav bar</div>
		<div class="row board">introduce board</div>
		<div class="row main">
			<div class="col-lg-2 col-md-3 hidden-sm hidden-xs">left menu</div>
			<div class="col-lg-10 col-md-9 col-sm-12 col-xs-12">content
				with flowing blocks</div>
		</div>
		<div class="row footer">
			<div class="col-lg-4 col-md-6 col-sm-12 col-xs-12">1</div>
			<div class="col-lg-4 col-md-6 col-sm-12 col-xs-12">2</div>
			<div class="col-lg-4 col-md-6 col-sm-12 col-xs-12">3</div>
		</div>
	</div>
</body>
</html>
```

## ajax block
```html
# ajax 
<div class="col-lg-4 col-md-6 col-sm-12 col-xs-12> 
	load from outside url
</div>
```

# web app
## java
## python