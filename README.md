### Ionic-Project

****
	
|Author|Toka|
|---|---
|E-mail|919210262@qq.com

****
	
## The problems that I have met are in developing ionic3 apps<br>
* [Ionic Api document](https://ionicframework.com/docs/api)<br>
* ### The style of the ion-button inside the component is lost after adding the component<br>	
	* Solution : Add IonicModule module to module.ts in the component<br>
	* Tip : add componrnt => ionic -g componrnt \[name\] <br>
	* [Reference document](https://www.jianshu.com/p/048f8a6c8952)<br>
	
* ### Data cannot be updated in time on the pages：
	* Solution : <br>
		* import \{ NgZone \} from '@angular\/core' <br>
		  this.zone.run\( \(\)\ =\> \{ <br>
				//core   <br>
		  }) <br>
	* Tip : constructor\(private zone:NgZone\)<br>
	* [Reference document](http://www.jason-z.com/post/30)<br>

* ### Cover the original style of the ionic component
	* Solution : CSS has higher priority than ionic css<br>
	* Tip :  Universal Selector (*) \< Element (Type) Selector \< Class Selector \< Attribute Selector \< Pseudo Class \< ID Selector \< Inline Style \<！important<br>
	* [Reference document]()<br> 