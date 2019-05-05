### Work_Helper Project (Ionic)

****
	
|Author|Toka|
|---|---
|E-mail|919210262@qq.com

****
	
### The problems that I have met are in developing ionic3 apps<br>
* [Ionic Api document](https://ionicframework.com/docs/api)<br>
* #### The style of the ion-button inside the component is lost after adding the component<br>	
	* Solution : Add IonicModule module to module.ts in the component<br>
	* Tip : add componrnt => ionic -g componrnt \[name\] <br>
	* [Reference document](https://www.jianshu.com/p/048f8a6c8952)<br>
	
* #### Data cannot be updated in time on the pages：
	* Solution : <br>
	```javascript
	import { NgZone } from '@angular/core' 
		this.zone.run( () => { 
			//core   
		}) 
	```
	* Tip : constructor\(private zone:NgZone\)<br>
	* [Reference document](http://www.jason-z.com/post/30)<br>

* #### Cover the original style of the ionic component
	* Solution : CSS has higher priority than ionic css<br>
	``` 
	Universal Selector (*) < Element (Type) Selector < Class Selector < Attribute Selector < Pseudo Class < ID Selector < Inline Style < !important 	
	```
	* [Reference document]()<br> 

* #### 接口请求的Url,空格，斜杠/都不能多不能少，这是电脑测试不出来的bug
	ENOENT: no such file or directory, open 'C:\Users\Toyoka\WorkProject\work-helper\work-helper-app\plugins\EAccountSDK\www\eaccount.js'

* #### 管道pipe 
	* 创建指令 ：ionic g pipe '管道名字'
	* html中管道的名字，是你自定义管道ts中的name值
	```
	{{ 输入数据 | 管道名字 }} 
	```
* #### ionic 页面的渲染和异步请求是并列进行的，请求的数据(如果json对象有多层对象)，页面渲染，加载数据时，若请求数据还未获取，则默认为undefined，嵌套对象则会报错，其属性undefined
	* tips: 请求时间过长时，页面若有请求数据的展示，需添加 ngIf 判断对象是否存在，等对象获取后再展示。
* #### 组件Components
	* 日期选择 datetime
	```html
	<ion-datetime displayFormat="YYYY年MM月" cancelText='取消' doneText='确认'>
    </ion-datetime>
	```
	* 加载动画 spinner
	```html
	<ion-spinner name="bubbles"></ion-spinner>
	```
	* 模态框
	```typescript
	let modal = this.modalCtrl.create(ModalPage);//创建新的页面——ModalPage
	addModal.onDidDismiss(id => {   //传回参数存入id 并执行操作
      if (id) {		
        this.submit()
      }
    })
    modal.present();//页面展示
	```	
	* events事件,发布、订阅
	```
	// 父页面  订阅消息，退出时销毁页面
	events.subscribe('user:out', () => {
      this.viewCtrl.dismiss()
    })
	   
	ionViewWillUnload() {
		this.events.unsubscribe('user:out');
	}
	// 子页面  发布消息  (父子页面消息名统一)
	this.events.publish('user:out')	
	```
	* 锚点,Content组件
	```javascript
	import { Content } from 'ionic-angular';
	@ViewChild(Content) content: Content;
	ionViewDidEnter() {
		this.content.scrollToBottom();
	}
	```
	* Md5加密
	```javascript
	import { Md5 } from 'ts-md5/dist/md5';
	// 参数只能是字符串类型
	Md5.hashStr(param) 
	```
	* pop 回调方法
	```
	// 回调函数
	CallbackFunction = (params) => {
      return new Promise((resolve, reject) => {
        if (typeof (params) !== 'undefined') {
          resolve('ok');
          //判断返回时否勾选
          if (params.do === "no") {
            console.log('进入回退函数')
          }
        } else {
          reject(Error('error'))
        }
    });
	}
	```
* #### Ionic插件
	* photo-library
		* [Reference document](https://www.jason-z.com/post/26)<br>
	1. saveImage()方法不报错
		1. requestAuthorization不定义option的时候，默认write权限是false
		```
		photoLibrary.requestAuthorization({
		  "read": true,
		  "write": true
		}).then(()=>{})
		```
		2. android的写权限增加AndroidManifest.xml
		```
		<platform name="android">
		  <config-file target="AndroidManifest.xml" parent="/*">
			<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
		  </config-file>
		</platform>
		```
		3. 图片地址并且带有参数,则添加"&ext=.jpg"强制下载图片
		```
		url+'&ext=.jpg'
		```
		
* #### 注：在每次请求的时候打印日志，不用每次console.log。
	
* #### 生命周期	
| 生命函数 | 描述 |
| ------------- | ----------- |
| ionViewDidLoad      | 在页面加载的时候触发，且仅在页面创建的时候触发一次，适合做一些一次性的处理，比如从服务器拉取用户数据存到缓存中。	|
| ionViewWillEnter    | 在页面刚刚开始切换时触发。你可以在这时对页面的数据进行预处理。（非激活状态）	|
| ionViewDidEnter     | 用户已经进入到新页面了（页面处于激活状态）	|
| ionViewWillLeave    | 当将要从页面离开时触发（激活状态）	|
| ionViewDidLeave     | 离开页面时触发（页面处于非激活状态）	|
| ionViewWillUnload   | 当页面将要销毁同时页面上元素移除时触发	|
| ionViewCanEnter     | 用于限制是否可以进入某个页面	|
| ionViewCanLeave     | 用于限制是否可以离开这个页面	|

	* constructor()只有在页面初始化的时候执行一次
****

### Css<br>
* #### 动画
	```css
	// 旋转 rotate
	transform: rotate(-20deg); //正数表示顺时针旋转，负数表示逆时针旋转
	// 移动 translate
	transform: translate(x,y) // 水平方向和垂直方向同时移动
	transform: translateX(x)  // 水平方向移动
	transform: translateY(y)  // 垂直方向移动
	// 缩放 scale
	transform: scale(X,Y) // 元素进行缩放,X，Y两个方向的缩放倍数是一样的。并以X为准。
	transform: scaleX(x)  // 元素只在X轴(水平方向)缩放元素
	transform: scaleY(y)  // 元素只在y轴(垂直方向)缩放元素
	// 扭曲 skew
	transform: skew(x,y) // 扭曲方向(水平,垂直)
	transform: skewX(x) // 扭曲方向(水平)
	transform: skewY(y) // 扭曲方向(垂直)
	// 矩阵 matrix
	
	// 改变元素基点 transform-origin
	transform-origin(X,Y):用来设置元素的运动的基点（参照点）。
	```	
* #### 显示多行，且有行数限制
	* 多行控制: white-space:(normal 正常换行/nowrap禁止换行)
	```css
	display: -webkit-box;
	-webkit-box-orient: vertical;
	-webkit-line-clamp: 3;
	overflow: hidden;
	```
* #### flex  
	* 排列方向：flex-direction: row/column/row-reverse/column-reverse
	* 垂直居中: display:flex;align-items:center
	* 多行控制: flex-wrap：nowrap(单行)/wrap(多行)/wrap-reverse(反向多行)
	* 等分布局：
		```css
		外层 displat:flex; justify-content:space-around(内层div均匀分布)/space-between(内层div两端对齐)
		内层 flex-grow:1;(使每个div所占比例相同) flex:0 0 33.33%; (三等分)
		```
* #### 栅格系统(grid-row-col)
	* 栅格系统都会自动给每行(row)的分12列(col).
	```
	每列占屏比例设置：col-12/显示列数
	例：占3列也就是 3/12=4 => col-4 
	```
	* 不同屏幕对应的参数
	```
	col-xs-超小屏幕 手机 (<768px),
	col-sm-小屏幕 平板 (≥768px),
	col-md-中等屏幕 桌面显示器 (≥992px)(栅格参数)
	```
* #### 行内显示，有超出则隐藏并添加省略 (...)
	```css
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
	```	
* #### 水印
	# 满屏效果(遮盖层)
	```css
	position:fixed;
	top: 0;
	right: 0;
	bottom: 0;
	left: 0;
	```
	# canvas 实现
	```html
	  <canvas id="waterMark" width='140' height='140'></canvas>
	```
	```javascript
	watermark() {
	  let canvas = <HTMLCanvasElement>document.getElementById('waterMark');
      var ctx = canvas.getContext('2d');
      canvas.width = document.getElementById('gridheight').clientWidth;
      // 绘制文字内容
      for (let p = 0; p < 4; p++) {
        for (let q = 0; q < 6; q++) {
          // 绘制文字  注意：：绘制斜体文字 旋转以后会发生位移，所以必须在旋转之后进行位置的调整；
          let text = this.user.userName + this.lastPhone;
          ctx.save();//保存原来的状态  绘制字体都是需要旋转倾斜  那么之前绘制的图片就要进行状态的保存
          ctx.rotate(-Math.PI / 6);//绘制倾斜字体
          ctx.translate((q * -12), -(5 * p));//发生位移进行位移的恢复
          ctx.font = "12px serif";
          ctx.fillStyle = '#999';
          ctx.fillText(text, ((p * 100)), ((q * 60) + 60));
          ctx.globalAlpha = 0.5;
          ctx.restore();//状态的恢复
        }
      }
    }
	```
****

### Angular<br>
* #### Command
	* 在html标签里的item 不用{{}}表示，直接是调用即可。
	1. ngIf
	   ```html
	   <div *ngIf="condition">...</div>
	   ```
	   * 作用：" "内是判断条件，boolean类型

	2. ngFor (外标签内容不定)
	   ```html
	   <li *ngFor="let item of items;let i =index ">{{item}}</li>
	   ```
	   * 作用："item为局部变量，items为ts文件内的数组，同理,i 代指 index属性为索引，用于跟踪item位置"
			
	3. ngForOf
	   ```html
	   <ng-template="ngFor let item of items; index as i; trackBy: trackByFn">
	   {{item}}
	   </ng-template>
	   ```
	   * 作用：可添加筛选条件，选取数组的某一部分。	
	   
	4. ngClass
	   ```html
	   <span [ngClass]="{'text-danger': i==0}">{{item}}</span>
	   ```
	   * 作用：给标签动态添加class样式属性
	   * [Reference document](https://semlinker.com/ng-quick-start/)<br>
		  
	5. pipe
	   * 管道分为 纯管道 和 非纯管道
	      * 纯管道：只有检查到输入值发生纯变更时，才会执行纯管道。纯变更指的是，原始类型值(String,Number,Boolean,Symbol)的改变，或者对象引用的改变(对象值改变不是纯变更，不会执行)。
	      * 非纯管道：在每个组件的变更检测周期执行。
```
	{{ 输入数据 | 管道名字 : 管道参数 }} 

	{{ 输入数据 | 管道名字 }} 
```

****

### Javascript 
* #### Grammar
	* 深拷贝和浅拷贝
	```
	基本类型--名值存储在栈内存中
	引用数据类型--名存在栈内存中，值存在于堆内存中，但是栈内存会提供一个引用的地址指向堆内存中的值
	假设a为引用数据类型，b对a进行拷贝，由于a与b指向的是同一个地址，所以自然b也受了影响，这就是所谓的浅拷贝了。
	浅拷贝，是将目标对象值和引用都拷贝给新对象。
	深拷贝，是创建一个对象，并拷贝目标对象各个层级的属性。
	
	// JSON对象的parse和stringify (深拷贝)
	var target = JSON.parse(JSON.stringify(source));
	```
	* ajax异步请求
	
	* 序列化：
		```javascript
		//由JSON字符串转换为JSON对象
		let last=obj.toJSONString()

		let obj = JSON.parse(str)  
		
		let obj = eval('(' + str + ')')
		
		//将JSON对象转化为JSON字符
		var last=obj.toJSONString() 

		var last=JSON.stringify(obj)
		```
	* 延时
		```
		// 作用是由于渲染速度造成图片不显示的bug,采用延时解决
		setTimeout( ()=>{},time)
		```
****

### ES6 Grammar<br>
* #### Command
	* let (块级作用域)
		1. 作用：let命令在其所在的代码块内有效。
		2. 只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
		```javascript
		let param = 1;
		```
		
		```javascript
		for (let i = 0; i < 10; i++) {
			...
		}
		console.log(i);
		// i is not defined
		var tmp = 123;
		if (true) {
		  tmp = 'abc'; // ReferenceError 这里的tmp和外代码块的tmp不是一个。
		  let tmp;
		}
		```
		
	* const (只读的常量，一旦生命，不能改变)
		* 作用：const命令在其所在的代码块内有效。
		```javascript
		const param = 1;
		```
	* 解构赋值
		* 解构：允许按照一定模式，从数组和对象中提取值，对变量进行赋值
		```javascript
		//数组
		let a = 1;
		let b = 2;
		let c = 3;
		// 等同于下面(数组形式)
		let [a,b,c] = [1,2,3];
		
		/*-----------------------*/
		
		let [x = 1] = [undefined];
		x // 1
		let [x = 1] = [null];
		x // null
		
		//对象 
		let { foo, bar } = { foo: "aaa", bar: "bbb" };
		foo // "aaa"
		bar // "bbb"
		
		/*-----------------------*/
		
		let { foo: baz } = { foo: "aaa", bar: "bbb" };
		baz // "aaa"
		foo // error: foo is not defined
		//先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。
		
		//字符串
		const [a, b, c, d] = 'code';
		a // "c"
		b // "o"
		c // "d"
		d // "e"
		```
	* tips:
		* 如果解构不成功，变量的值就等于undefined
		* 只有当一个数组成员严格等于undefined，默认值才会生效
		* foo是匹配的模式，baz才是变量。真正被赋值的是变量baz，而不是模式foo
		* 只要等号右边的值不是对象或数组，就先将其转为对象。
		* undefined和null无法转为对象，不能进行解构赋值。
	* 作用：
		1. 交换变量的值
		```javascript
		let x = 1;
		let y = 2;
		[x, y] = [y, x];
		```
		2. 接收函数返回的单值或多值
		```javascript
		// 返回一个数组
		function example() {
		  return [1, 2, 3];
		}
		let [a, b, c] = example();	
		```
		3. 提取json数据 (最多)
		```javascript
		let { id, status, data: number } = jsonData; //jsonData为json对象
		```
		4. 函数参数的定义和设默认值
		5. 遍历Map结构
		6. 作为模块的指定(公共)方法
	* 字符串扩展
		* 字符串遍历 (for...of循环)
		```javascript
		for (let codePoint of 'foo') {
		  console.log(codePoint)
		}
		// "f"
		// "o"
		// "o"
		```
		* 字符串匹配(includes(), startsWith(), endsWith())  字符串重复(repeat()函数) 提示字符串格式补齐(padStart(x,y),padEnd(x,y))
		* 提示字符串格式。
		```javascript
		// includes()：返回布尔值，表示是否找到了参数字符串。
		// startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部。
		// endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部。
		let s = 'Hello world!';

		s.startsWith('Hello') // true	s.startsWith('world', 6) // true
		s.endsWith('!') // true			s.endsWith('Hello', 5) // true
		s.includes('o') // true			s.includes('Hello', 6) // false
		
		// repeat(n): 返回一个新字符串，表示将原字符串重复n次,n取整。n = Infinity 或 n < -1 则报错.
		'na'.repeat(Infinity)
		// RangeError
	
		// padStart(x,y)：从头部补齐 x是字符串补全生效的最大长度，y是用来补全的字符串。
		// padEnd(x,y): 从尾部补齐 
		'12'.padStart(10, 'YYYY-MM-DD') // "YYYY-MM-12"
		
		//正则匹配
		matchAll()
		```
	* 对象扩展
		* 属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串[object Object]
		* name()属性可获取函数名。
		* Object.getOwnPropertyDescriptor() 获取对象属性的描述(每个属性都对应一个描述对象)
		```javascript
		let obj = { foo: 123 };
		Object.getOwnPropertyDescriptor(obj, 'foo')
		// 描述对象如下 
		//	{ 
		//    value: 123,
		//    writable: true,
		//    enumerable: true,   该属性为可枚举性(false 表示某些操作下会忽略当前属性(如本例中的foo) )
		//    configurable: true
		//  }
		
		Object.assign (target, source1,source2, source3, …);
		//第一个参数是目标对象，后面的都是源对象。(深拷贝)
		``` 
		* for...in循环：只遍历对象自身的和继承的可枚举的属性。(继承表示从原型继承的基础属性) 
		* Object.assign()：忽略enumerable为false的属性，只拷贝对象自身的可枚举的属性。(浅拷贝)
		* tips: 
			1. 大多数时候，我们只关心对象自身的属性。所以，尽量不要用for...in循环，而用Object.keys()代替。
			2. toString和length属性无法遍历(enumerable)
	* Promise() 
		* 问题：是代码冗余，请求任务多时，一堆的then，也使得原来的语义变得很不清楚。此时我们引入了另外一种异步编程的机制：Generator。

****

### ES7 Grammar<br>
* #### Command
	* includes(): 查找一个值在不在数组里,若是存在则返回true,不存在返回false.
	* tips: 对象类型的数组，二维数组，这些，是无法判断的.
	```javascript
	//接收俩个参数：要搜索的值和搜索的开始索引
	['a', 'b', 'c', 'd'].includes('b', 1)      // true
	['a', 'b', 'c', 'd'].includes('b', 2)      // false
	
	//处理 NAN === NAN => flase
	let demo = [1, NaN, 2, 3]
	demo.indexOf(NaN)        //-1
	demo.includes(NaN)       //true
	```
	* Generator 

* #### Command
	* asayc await
	
****

### Project Packaging (Ioinc) <br>
* #### 环境：
	*  nodejs
	*  jdk			(java的开发基础类库，因为是android平台)
	*  SDK			(安卓开发集成包，集成了安卓的开发工具，插件，API等等) 
	*  gradle		( JAVA界的Weboack ，支撑app的编译，打包的流程) 
	
* #### 工具
	*  gitbash
	*  VSCode	
	
* #### 打包指令
	```
	ionic cordova build android 
	ionic cordova build ios 
	
	ionic cordova run android  打包测试
	```

* #### 问题：
	* Error: xcodebuild was not found. Please install version 7.0.0 or greater from App Store
		* 原因: windows系统 没有xcode IDE
	
	* [文档](https://blog.csdn.net/qq_20264891/article/details/79319408)<br> 
	
###	Regular Expression  正则表达式<br>
* #### 字符串中截取指定字符
	```
	/"[^"]+"/g   
	```
* ####  去除字符串中的指定符号	
	```
	.replace(/\"/g, "")
	```
* ####  保留小数点后两位	
	```
	.replace(/^(\-)*(\d+)\.(\d\d).*$/, '$1$2.$3')
	```
	
****

### NPM
* #### npm全称为Node Package Manager，是一个基于Node.js的包管理器，用来安装项目所需依赖。
	* 常用命令：
		* npm install
		* npm start
		* 使用淘宝 NPM 镜像： npm install -g cnpm --registry=https://registry.npm.taobao.org (npm => cnpm)
	* 常见错误：
		* -errno -4058 
		1、安装源的问题，具体报错时会有写。改为淘宝镜像即可。
		2、你没有在工程目录下启动项目，所以npm start后，找不到项目进而报错。
 
### Yarn
* #### JS 包管理工具，正如官方文档中写的，Yarn 是为了弥补 npm 的一些缺陷而出现的。
	* 常用命令：
		* 
		* yarn install 安装依赖  yarn remove [package] 删除依赖包
		* yarn upgrade 更新包版本
		* yarn start 启动
		* yarn run build 打包
	* 常见错误：
		
* #### npm和yarn区别
	| npm | yarn |
	| ------------- | ----------- |
	|  npm install  |  yarn	|
	|  npm install [package] |  yarn add  [package]	|	
	|  npm uninstall [package]   | yarn remove [package]	|		
	|  npm update |  yarn upgrade	|	
 
 
****

### 前端优化 
* #### 优化
	* html

	* css
		图片尽量放在一张图内，通过图片定位获取局部图
	* javascript
		* dns预解析
		* dom操作(重绘(盒子模型的原位置不变)、回流(盒子模型的原位置改变))
		* 减少请求数
****

### 关于计算机 
* #### 工作原理
	* 操作系统
		* Unix: 我们现在所用的电脑的操作系统最初是Unix。
		* Linux(Linus(作者) +minix): unix => mini-Unix
 	* 时间戳：格林威治时间自1970年1月1日(00:00:00 GMT)至当前时间的总秒数。
		* 计算机产生的年代和应用的时限综合取了1970年1月1日作为UNIX TIME的纪元时间。
		* 英国格林威治：世界标准时间，是本初子午线上的地方时。
		* UTC( GMT = UTC ) ＋ 时区差(东加西减) ＝ 本地时间 (中国以北京时间为准，北京在东八区) 
		* 起初计算机操作系统是32位，而时间也是用32位表示。32位能表示的最大值是2147483647。1年365天的总秒数是31536000，2147483647/31536000 = 68.1，也就是说32位能表示的最长时间是68年，而实际上到2038年01月19日03时14分07秒，便会到达最大时间，过了这个时间点，所有32位操作系统时间便会变为10000000 00000000 00000000 00000000 (即1901年12月13日20时45分52秒)，造成时间回归的现象。
		* 解决：64位操作系统可以表示到292,277,026,596年12月4日15时30分08秒。
	* MD5加密
		1. 为任何文件产生一个同样独一无二的“数字指纹”，如果任何人对文件做了任何改动，其MD5值也就是对应的“数字指纹”都会发生变化。
		2. “数字指纹”是一个文件名相同，文件扩展名为.md5的文件，在这个文件中通常只有一行文本，例如：
		```
		MD5 (tanajiya.tar.gz) = 38b8c2c1093dd0fec383a9d9ac940515   (举个栗子)
		```
		3. 
****

	
	