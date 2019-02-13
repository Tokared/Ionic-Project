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
	```
	import { NgZone } from '@angular/core' <br>
		this.zone.run( () => { <br>
			//	core   <br>
		}) <br>
	```
	* Tip : constructor\(private zone:NgZone\)<br>
	* [Reference document](http://www.jason-z.com/post/30)<br>

* #### Cover the original style of the ionic component
	* Solution : CSS has higher priority than ionic css<br>
	* Tip:
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
```
display: -webkit-box;
-webkit-box-orient: vertical;
-webkit-line-clamp: 3;
overflow: hidden;
```
* #### flex  
	* 多行控制: white-space:(normal 正常换行/nowrap禁止换行);
	
****

### Angular<br>
* #### Command
	* 在html标签里的item 不用{{ }}表示，直接是调用即可。
	1. ngIf
	   1. 写法：<div *ngIf="condition">...</div>
	   1. 作用：""内是判断条件，boolean类型

	2. ngFor (外标签内容不定) 
	   2. 写法：<li *ngFor="let item of items;let i =index ">{{item}}</li>
	   2. 作用："item为局部变量，items为ts文件内的数组，同理,i 代指 index属性为索引，用于跟踪item位置"
			
	3. ngForOf 
	   3. 写法：<ng-template="ngFor let item of items; index as i; trackBy: trackByFn">{{item}}</ng-template>
	   3. 作用：可添加筛选条件，选取数组的某一部分。
				
	4. ngClas 
	   4. 写法：<span [ngClass]="{'text-danger': i==0}">{{item}}</span>
	   4. 作用：给标签动态添加class样式属性
	   4. [Reference document](https://semlinker.com/ng-quick-start/)<br>
		  
	5. pipe 
	   5. 管道分为 纯管道 和 非纯管道
	      5. 纯管道：只有检查到输入值发生纯变更时，才会执行纯管道。纯变更指的是，原始类型值(String,Number,Boolean,Symbol)的改变，或者对象引用的改变(对象值改变不是纯变更，不会执行)。
	      5. 非纯管道：在每个组件的变更检测周期执行。
```
{{ 输入数据 | 管道名字 : 管道参数 }} 

{{ 输入数据 | 管道名字 }} 
```	
****

### ES6 Grammar<br>
* #### Command
	* let (块级作用域)
	* 写法：let param = 1;
			* 1.作用：let命令在其所在的代码块内有效。
			  2.只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。
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
		* 写法：let param = 1;
			* 作用：const命令在其所在的代码块内有效。
	
	```javascript
		
	```

****

### Project Packaging (Ioinc) <br>
* #### 环境：
	*  nodejs
	*  jdk(java的开发基础类库，因为是android平台)
	*  SDK(安卓开发集成包，集成了安卓的开发工具，插件，API等等) 
	*  gradle( JAVA界的Weboack ，支撑app的编译，打包的流程) 
	
* #### 工具
	*  gitbash
	*  VSCode	
	
* #### 流程
	* ionic cordova build android 
	* ionic cordova build ios (windows系统 没有xcode IDE)
	
* #### 问题：
	* failed to install EAccountSDK
	* Error: xcodebuild was not found. Please install version 7.0.0 or greater from App Store
	
	* [Reference document](https://blog.csdn.net/qq_20264891/article/details/79319408)<br> 
	
###	regular expression  正则表达式<br>
* #### 字符串中截取指定字符
	/"[^"]+"/g   
* ####  去除字符串中的指定符号
	.replace(/\"/g, "")

****
 

	
	