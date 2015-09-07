# table
表格的渲染组件
[DEMO请点我](http://lovewebgames.com/jsmodule/table.html "table的demo")
![](example/table.jpg)

*如上图所示，功能基本包括常用表格中遇到的分页、搜索、删除、AJAX操作。由于是用的HANDLEBARS渲染的，所以样式可能很好的控制，要加新的功能也较容易。*
#调用例子
##html
	<div class="form">
		名称: <input type="text" name="gname"> <a href="#" id="search">search</a>
	</div>
	<div id="tab-list" ajaxurl="list.json">
		loading...
	</div>
	<div id="pager"></div>
##模板
	<script type="text/x-handlebars-template" id="tpl-list">
		<table class="tab-list">
			<thead>
				<tr>
						<th class="first-cell">序号</th>
						<th>商品条码</th>
						<th>商品名称</th>
						<th>状态</th>
						<th>操作</th>
				</tr>
			</thead>
			<tbody>
				{{#each data}}
				<tr>
						<td class="first-cell">{{@index}}</td>
						<td>{{goods_bn}}</td>
						<td>{{goods_name}}</td>
						<td>上架</td>
						<td><a class="js-ajax" js-ajax-param="id={{goods_id}}" href="action.json">下架</a> <a class="js-delete" href="action.json">删除</a></td>
				</tr>
				{{/each}}
			</tbody>
		</table>
	</script>
##js
	<script>
		var table = new Table($('#tab-list'), $('#tpl-list'), $('#pager'), {}, $('#search'));
		table.init({type:'post'});
	</script>


----------
*参数将以hash值显示在url中,所以在这个版本里只支持ie8+浏览器，如果要支持低版本的，请使用1.0.7版本*
#属性和方法
##hash:true
	是否用url hash值的形式来表达分页和搜索条件，默认为true,但如果出现两个分页时，为导致互相影响，应保证只有一个对应hash
##constuctor:function(table, temp, page, param, search, callback)
	构造函数，table是指存放表格的容器，可以是一个空的div，也可以是table里的一个tbody；
	temp是指表格的模板，这里是script节点的jquery对象
	page 需要放置分页控件的容器
	param 初始化带的参数 type json
	search 搜索按钮节点，你的祖先级中要有一个class为form的节点，会利用[query](https://github.com/tianxiangbing/query)格式化里面为参数，进行查询数据操作
	callback 加载后的回调
	
##init:function(settings)
	init是启动方法，目前的settings中仅包含{type:'get'} ，ajax请求的类型