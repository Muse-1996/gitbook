# snabbdom DEMO

```text
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>Document</title>
</head>
<script src="https://cdn.bootcss.com/snabbdom/0.7.2/snabbdom.min.js"></script>
<script src="https://cdn.bootcss.com/snabbdom/0.7.2/snabbdom-class.min.js"></script>
<script src="https://cdn.bootcss.com/snabbdom/0.7.2/snabbdom-props.min.js"></script>
<script src="https://cdn.bootcss.com/snabbdom/0.7.2/snabbdom-style.min.js"></script>
<script src="https://cdn.bootcss.com/snabbdom/0.7.2/snabbdom-eventlisteners.min.js"></script>
<script src="https://cdn.bootcss.com/snabbdom/0.7.2/h.min.js"></script>
<body>
	<button id="change">更改</button>
	<div id="container"></div>
</body>
<script>
	var snabbdom = window.snabbdom

	//定义patch
	var patch = snabbdom.init([
		snabbdom_class,
		snabbdom_props,
		snabbdom_style,
		snabbdom_eventlisteners
	])

	//定义 h
	var h = snabbdom.h

	var container = document.getElementById('container')

	//生成vnode
	var vnode = h('ul#list',{},[
		h('li.item',{},'item1'),
		h('li.item',{},'item2'),
	])

	patch(container,vnode)

	document.getElementById('change').addEventListener('click',function (argument) {
		//生成 new vnode
		var newVnode = h('ul#list',{},[
			h('li.item',{},'item1'),
			h('li.item',{},'itemb'),
			h('li.item',{},'itemc'),
		])

		//对比出差异 根据差异进行渲染 
		patch(vnode,newVnode)
	})
</script>
</html>
```

