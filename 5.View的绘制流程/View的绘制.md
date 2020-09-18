
- ##  View树的绘制流程

```

1.View树的绘制流程
    handler通过发送和处理Message和Runnable对象来关联相对应线程的MessageQueue。
		（1）可以让对应的Message和Runnable在未来的某个时间点进行相应处理
		（2）让自己想要处理的耗时操作放在子线程，让更新ui的操作放在主线程。
		

```

#### View树的绘制流程

measure --> layout --> draw



#### Measure

1.ViewGroup.LayoutParams



指定视图宽度和高度的值。

具体值

match_parent：不包括padding值的。

Wrap_content：父控件包括子控件大小就可以。

【子视图它自己的大小】



2.MeasureSpec测量规格

32位

SpecMode  前两位 【测量模式】

SpecSize 	后30位 【在该测量模式下的大小】



会将这个视图的LayoutParams及结合父容器生成一个MeasureSpec。它规定了怎样去测量这个View的大小。

将MeasureSpec返还给父容器，教它如此去测量这个view的大小



三种选择：

不确定的：想多大多大

Exactly :确定的尺寸大小。

at most:父容器为子视图设置的最大尺寸 -- wrap_content



总结：在measure的过程当中，系统会将ViewGroup.LayoutParams根据父容器所施加的规则，转换成 MeasureSpec。然后根据MeasureSpec确定View的宽和高。



二.measure方法

1.measure【不可重写】 --》onMeasure

在measure生成了【宽高的测量规格MeasureSpec】



2.onMeasure(int widthMeasureSpec, int heightMeasureSpec)【可以重写】

自定义的时候，只需要复写onMeasure方法就可以了。



3.setMeasuredDimension()【测量阶段的终极】



4.总结：

​	开始于父控件ViewGroup，遍历子控件，并调用子控件的measure方法，根据父控件的MeasureSpec和子视图的LayoutParams来决定子视图的MeasureSpec。通过子视图的MeasureSpec测试出子视图的宽高，然后一层一层的向下传递，不断的保存整个父控件的测量宽高。整个measure的测量调用流程，就是整个树型的递归过程。为整个view树计算实际的大小。每一个view视图的宽高都是由父视图和它本身的layoutparams来决定的。



#### layout

1.onLayout(changed，l,t,r,b)  【在ViewGroup中是抽象的实现】



2. 如果要自定义Viewgroup的话，

   参考LinearLayout



#### Draw

1.invalidate()

请求，如果视图大小没发生变化，不会调用layout



2.requestLayout()

视图方向，尺寸发生变化，会调用重新布局。会触发measure，layout。不会触发draw

