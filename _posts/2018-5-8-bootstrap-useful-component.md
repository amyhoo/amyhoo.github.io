---
categories: language
tags: [html]    
---
# bootstrap
a framework of responsive html pages 
## [styles](https://v3.bootcss.com/css/)
```html
### [rows and columns](https://v3.bootcss.com/css/#grid)
<div class="col-xs-1 col-sm-1 col-md-1 col-lg-1">
</div>
```

## [components](https://v3.bootcss.com/components/)
### [navbar](https://v3.bootcss.com/components/#navbar)
```html
# desgin:fix on top, a brand icon, a jump control button, a search input
<div class="row nav">
	<nav class="navbar navbar-default navbar-fixed-top">
		<div class="container-fluid">
			<!-- Brand and toggle get grouped for better mobile display -->
			<div class="navbar-header">
				<button type="button" class="navbar-toggle collapsed"
					data-toggle="collapse" data-target="#navbar-collapse-1"
					aria-expanded="false">
					<span class="sr-only">Toggle navigation</span> <span
						class="icon-bar"></span> <span class="icon-bar"></span> <span
						class="icon-bar"></span>
				</button>
				<a class="navbar-brand" href="#"><img alt="Brand" width="20"
					height="20" src=""></a>
			</div>

			<!-- Collect the nav links, forms, and other content for toggling -->
			<div class="collapse navbar-collapse" id="navbar-collapse-1">
				<ul class="nav navbar-nav">
					<li class="active dropdown"><a href="#"
						class="dropdown-toggle" data-toggle="dropdown" role="button"
						aria-haspopup="true" aria-expanded="false"> <span
							class="glyphicon glyphicon-move" aria-hidden="true"></span>
					</a>
						<ul class="dropdown-menu">
							<li><a href="#"><span
									class="glyphicon glyphicon-arrow-right" aria-hidden="true"></span></a></li>
							<li><a href="#"><span
									class="glyphicon glyphicon-arrow-left" aria-hidden="true"></span></a></li>
							<li><a href="#"><span
									class="glyphicon glyphicon-arrow-up" aria-hidden="true"></span></a></li>
							<li><a href="#"><span
									class="glyphicon glyphicon-arrow-down" aria-hidden="true"></span></a></li>
						</ul></li>
				</ul>
				<form class="navbar-form navbar-left">
					<div class="form-group">
						<input type="text" class="form-control" placeholder="Search">
					</div>
					<button type="submit" class="btn btn-default">Submit</button>
				</form>
			</div>
			<!-- /.navbar-collapse -->
		</div>
		<!-- /.container-fluid -->
	</nav>
</div>
```
### left menu nav
```html
# design a nav list
<div class="col-lg-2 col-md-3 hidden-print hidden-sm hidden-xs menu">
	<nav class="bs-docs-sidebar hidden-print hidden-xs hidden-sm affix">
		<ul class="nav bs-docs-sidenav">
			<li><a href="#">menu1</a>
				<ul class="nav">
					<li><a href="#">menu1.1</a></li>
					<li><a href="#">menu1.2</a></li>
					<li><a href="#">menu1.3</a></li>
				</ul></li>
			<li><a href="#dropdowns">menu2</a>
				<ul class="nav">
					<li><a href="#">menu2.1</a></li>
					<li><a href="#">menu2.2</a></li>
					<li><a href="#">menu2.3</a></li>
				</ul></li>
		</ul>
	</nav>
</div>
```
## [script](https://v3.bootcss.com/javascript/)
