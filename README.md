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

****

### Css<br>
* #### 显示多行，且有行数限制
```Css
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
```
* #### flex  
	* 多行控制: white-space:(normal 正常换行/nowrap禁止换行)
* #### 栅格系统(grid-row-col)
	* 栅格系统都会自动给每行(row)的分12列(col).
	```
	每列占屏比例设置：col-12/显示列数
	例：占3列也就是 3/12=4 => col-4 
	```
	不同屏幕大小对应的参数
	```
	col-xs-超小屏幕 手机 (<768px),
	col-sm-小屏幕 平板 (≥768px),
	col-md-中等屏幕 桌面显示器 (≥992px)(栅格参数)
	```
* #### 行内显示，有超出则隐藏并添加为...
```Css
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
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
		/*-----------------------*/
		
		//对象 
		let { foo, bar } = { foo: "aaa", bar: "bbb" };
		foo // "aaa"
		bar // "bbb"
		/*-----------------------*/
		let { foo: baz } = { foo: "aaa", bar: "bbb" };
		baz // "aaa"
		foo // error: foo is not defined
		//先找到同名属性，然后再赋给对应的变量。真正被赋值的是后者，而不是前者。
		
		/*-----------------------*/
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
	```

* #### 问题：
	* failed to install EAccountSDK
	* Error: xcodebuild was not found. Please install version 7.0.0 or greater from App Store
		* 原因: windows系统 没有xcode IDE
	
	* [Reference document](https://blog.csdn.net/qq_20264891/article/details/79319408)<br> 
	
###	Regular Expression  正则表达式<br>
* #### 字符串中截取指定字符
	```
	/"[^"]+"/g   
	```
* ####  去除字符串中的指定符号
	```
	.replace(/\"/g, "")
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
		

#### npm和yarn区别
| npm | yarn |
| ------------- | ----------- |
|  npm install  |  yarn	|
|  npm install [package] |  yarn add  [package]	|	
|  npm uninstall [package]   | yarn remove [package]	|		
|  npm update |  yarn upgrade	|	
 
****

	
	