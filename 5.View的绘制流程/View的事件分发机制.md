
- ##  View树的绘制流程

#### 为什么会有事件分发机制

视图重叠，那么点击事件到底由谁来处理。这个需要由事件分发机制来决策。



#### 三个重要的事件分发方法

1.dispatchTouchEvent

2.onInterceptTouchEvent

3.onTouchEvent



【父控件】dispatchTouchEvent返回false（onInterceptTouchEvent不拦截返回false），向下分发调用【子view】的dispatchTouchEvent；

若【父控件】dispatchTouchEvent返回true（onInterceptTouchEvent至少有一个返回true），调用自己的onTouchEvent；无论自己的onTouchEvent返回true事件被消费；返回false，事件会向父控件的父控件onTouchEvent进行传递



事件分发流程：Activity->PhoneWindow -> DecorView -> ViewGroup -> View

责任链模式：onInterceptTouchEvent 触发下一个责任链

