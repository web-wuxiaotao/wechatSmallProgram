# wechatSmallProgram
# 微信小程序研究
#### 微信小程序官方文档给出了app.js, app.json, app.wxss. 先从这三个文件说起. - app.js 这个文件是整个小程序的入口文件,开发者的逻辑代码在这里面实现,同时在这个文件夹里面可以定义全局变量. - app.json 这个文件可以对小程序进行全局配置,决定页面文件的路径,窗口表现,设置网络超时时间,设置多tab等. - app.wxss 是小程序的公共样式表.(为了适应广大的前端开发者，WXSS 具有 CSS 大部分特性。 同时为了更适合开发微信小程序，对 CSS 进行了扩充以及修改。)

##一、 首先说的是配置文件app.json.这是官方给的例子
		{
			"pages": [ "pages/index/index", "pages/logs/index" ],
			"window": { "navigationBarTitleText": "Demo" },
			"tabBar": { "list": [{ "pagePath": "pages/index/index", "text": "首页" }, { "pagePath": "pages/logs/logs", "text": "日志" }] }, 
			"networkTimeout": { "request": 10000, "downloadFile": 10000 },
			"debug": true
		}
* 官方给出了app.json五个配置项列表
	*  **pages**
	*  **window**
	*  **tabBar**
	*  **networkTimeout**
	*  **debug**
	##1.pages
	### 它的作用是配置小程序的页面,这个配置项是必填的,它接受一个数组,里面的每一项都是字符串,从上面给出的代码: "pages": [ "pages/index/index", "pages/logs/index" ] 可以看出,每一项分别对应的都是实现文件的路径以及他的文件名. *需要注意的是，这个配置里面的第一行配置是它的初始页面,例如上面代码的初始页面就是index*
	
	##2. window
	### 这个配置项是用来设置小程序的状态栏、导航条、标题、窗口背景色。他给出了六个属性
	* **navigationBarBackgroundColo**
		* 是用来设置导航栏背景颜色,这个属性要输入的是十六进制颜色值.
	* **navigationBarTextStyle**
		* 它是用来导航栏标题颜色的,它的输入类型是字符串(String)，不过暂时只支持（black/white）两种颜色
	* **navigationBarTitleText**
		* 这个属性用来设置导航栏标题内容
	* **backgroundColor**
		* 这个属性用来设置窗口背景色，输入的是十六进制颜色值
	* **backgroundTextStyle**
		* 这个属性我的理解是设置窗口内容的样式的,官方给出的标准说明是下拉背景字体、loading 图的样式,这个属性同navigationBarTextStyle属性一样目前仅支持两种颜色(dark和light).
	* **enablePullDownRefresh**
		* 这个属性是设置是否开启下拉刷新,默认是开启的,注意: 在这个配置文件(app.json)中如果关闭了下拉刷新,当你在你自己开发的页面中想要设置下拉刷新也是行不通的,也就是说如果你想要在以后页面中使用下拉刷新这个功能,就必须保证这个配置文件中的这一项设置是打开的.
	###示例代码
		{
		  "window":{
		    "navigationBarBackgroundColor": "#ffffff",
		    "navigationBarTextStyle": "black",
		    "navigationBarTitleText": "微信接口功能演示",
			"backgroundColor": "#ffffff",
		    "backgroundColor": "#eeeeee",
		    "backgroundTextStyle": "light"
		  }
		}
	##3. tabBar
	###如果我们的小程序是一个多 tab 应用（客户端窗口的底部或顶部有 tab 栏可以切换页面），那么我们可以通过 tabBar 配置项指定 tab 栏的表现，以及 tab 切换时显示的对应页面。
	###注意： 通过页面跳转（wx.navigateTo）或者页面重定向（wx.redirectTo）所到达的页面，即使它是定义在 tabBar 配置中的页面，也不会显示底部的 tab 栏。
	###tabBar 是一个数组，只能配置最少2个、最多5个 tab，tab 按数组的顺序排序。
	* **color** &nbsp;&nbsp;&nbsp; 设置tab上文字默认的颜色
	* **selectedColor** &nbsp;&nbsp;&nbsp; 设置tab上文字选中后的颜色
	* **backgroundColor** &nbsp;&nbsp;&nbsp; 设置tab的背景颜色
	* **borderStyle** &nbsp;&nbsp;&nbsp; 设置tab上的边框颜色，仅支持**black/white**
	* **position** &nbsp;&nbsp;&nbsp; tab栏的位置，分别为上：**top**、下：**bottom**。
	##4. networkTimeout
	###用来设置网络请求的超时时间，四个属性：
	* **request** &nbsp;&nbsp;&nbsp; 用来定义wx.request的超时时间，单位毫秒，默认为：60000
	* **connectSocket** &nbsp;&nbsp;&nbsp; 用来定义wx.connectSocket的超时时间，单位毫秒，默认为：60000
	* **uploadFile** &nbsp;&nbsp;&nbsp; 用来定义wx.uploadFile的超时时间，单位毫秒，默认为：60000
	* **downloadFile** &nbsp;&nbsp;&nbsp; 用来定义wx.downloadFile的超时时间，单位毫秒，默认为：60000
