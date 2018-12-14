### Ionic-Project

****
	
|Author|Toka|
|---|---
|E-mail|919210262@qq.com

****
	
## The problems that I have met are in developing ionic3 apps<br>

* ### Ionic3 在添加component组件后，组件内的ionic控件的样式丢失<br>	
	* Solution : 在组件内的module.ts添加IonicModule <br>
	* Tip : add componrnt => ionic -g componrnt \[name\] <br>
	* [Reference document](https://www.jianshu.com/p/048f8a6c8952)<br>
* ### Data cannot be updated in time on the pages：
	* Solution : import \{ NgZone \} from '@angular\/core' <br>
		* this.zone.run\(\(\)\ =\> \{ <br>
			  //core   <br>
		  }) <br>
	* [Reference document](http://www.jason-z.com/post/30)<br>