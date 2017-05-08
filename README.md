# Avalon 分页组件

基于 [https://github.com/RubyLouvre/ms-pager](https://github.com/RubyLouvre/ms-pager).

## 使用

### 环境

Webpack [https://github.com/sayll/ie-webpack-start](https://github.com/sayll/ie-webpack-start)


### HTML 

	<xmp ms-widget="{id:'msPaging',is:'ms-paging', classes: @pagingConfig.classes, total: @pagingConfig.total, size: @pagingConfig.size, currentPage: @pagingConfig.currentPage, onPageClick: @pagingConfig.onPageClick}"></xmp>

### JS

#### 1.  引入
              
	require('./components/paging/index')

#### 2. 配置
	
	pagingConfig: {
        classes: ' gb-paging__inlineblock right--',
        total: 0,
        size: 10,
        currentPage: 1,
        onPageClick: function (e, cur) {
            vm.list(cur);
        }
    }

#### 3. 使用

	list: function (skip) {
		// 参数转换、赋值
		var size = vm.pagingConfig.size,
	        start = skip >= 1 ? ((skip - 1) * (size || 10) || 0) : 0,
			params = {
				start: start,
	            length: size
			};
		
		// ajax请求
		ajax({}).done(function (data) {
			// 渲染分页, total 为总记录数目，curr 为当前页码
			vm.pagingConfig.total = data.recordsTotal || 0
            vm.pagingConfig.currentPage = skip || 1;
		
			// 回到分页容器顶部（提升体验）
            $("html, body").animate({
                scrollTop: $("#main").offset().top
                }, 500
            );
		});		
	}
	
	
#### 4. 初始化

	vm.list();


## 其它

> 已知问题数个，欢迎各种姿势的改进、修复 bug 。



## License

The MIT license.