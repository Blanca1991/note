## 我的理解CSS中的 animation transition transform

#### 1. transform
transform  的字面意思是变形变换  是对html中的元素div块元素和行内块元素等的变形。

 **transform 的属性有 translate(N) 、rotate(Ndeg) 、 scale(N) 、 skew(N)**
 
 +  translate(N) 在某一轴上移动 其单位可以是px 、 ％ 、N为正数元素向右移动，N为负数元素向左移动。  
 
  
	translate的使用方法 ：
	1.  translate（N）在X轴的方向移动N ， translate（N，N）为两个数值的时候，前一个数值在X轴上移动，后一个数值在Y轴上移动。 translate（N，N，N）不是正确的使用方式，要想在Z轴上移动使用translate3d（N,N,N）。
	2.  translateX（N）在X轴上移动。
	3.  translateY（N）在Y轴上移动。
	4.  translateZ（N）在X轴上移动，使用时还要在父级的div上配合perspecive:length,length必须为px不能使用％。
	5.  translate3d（N)，综合使用X轴，Y轴，Z轴。也需要在父级div上配用perspecive:length。


 +  rotate(Ndeg) 在某一轴上旋转 其单位为deg 。N为正数，顺时针旋转，N为负数，逆时针旋转。
	
	rotate(Ndeg)的使用方法：
	1. rotate(Ndeg) 单独一个值的时候，表示在Z轴上的旋转 。
	2. rotate(Ndeg，Ndeg)。
会发现没有变化，查看代码知道原来这个属性浏览器没有识别出来，这是因为默认的rotate（）只能传入一个旋转角度值，而且默认的角度是以电脑屏幕的基准面，以自己的中心为基准点进行旋转的。说白了他是一个二维的旋转。
	3. rotateX(Ndeg) rotateY(Ndeg) rotateZ(Ndeg) 分别在XYZ轴上的旋转
	4. rotate3d(Ndeg,Ndeg,Ndeg)是一个3d旋转。在浏览器当中我们同样会发现不起效果，原因还是不识别。其实这就是rotate3d和translate3d，不同的地方，translate3d传入的三个值分别会被解析为XYZ的位移距离，rotate3d()则不会这么解析，官方给出的解析方法是rotate3d(X?,Y?,Z?,angle);也就是你需要对你需要旋转的轴进行判断，如果你要沿着该轴转动那就将该轴的值设置为1，否则为0；然后在后面的angle中设置旋转的角度，需要注意的是，angle只有一个角度值。
所以上面正确的写法是：
transform:rotate3d(1，1,0,45deg);  X轴Y轴旋转45度 Z轴不旋转 。

 +  scale(N) 在某一轴上的放大和缩小，0<N<1时为缩小，N>1时为放大。
 
	scale()的使用方法：
	1. scale（N）单独一个值的时候表示在X轴上缩放N倍。scale（N,N）表示在X轴和Y轴上都有缩放。scale（N,N,N）不是正确的使用方式，没有效果。
	2. scaleX（N）X轴的缩放
	3. scaleY（N）Y轴的缩放
	4. scale3d（N,N,N）3d效果XYZ全部变化。

+	skew(Ndeg)表示的在某一轴上的倾斜角度。N<0 倾斜的角度为顺时针倾斜，N>0为逆时针倾斜。
	
	skew()的使用方法：
	1. skew（Ndeg）在X轴上倾斜N度。skew（Ndeg,Ndeg）X轴和Y轴的同时倾斜。
	2. skewX（Ndeg）X轴上倾斜。
	3. skewY（Ndeg）Y轴上倾斜。
	
+   matrix(n,n,n,n,n,n) 矩阵函数
    基本上的样式都可以通过以上的方式设计出来，矩阵处理复杂的样式。包括所有的transform的属性样式。
	[ 详细的参看另外一片文 ](http://www.zhangxinxu.com/wordpress/2012/06/css3-transform-matrix-%E7%9F%A9%E9%98%B5/)

	
  




