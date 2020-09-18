
- ##  View树的绘制流程

#### 什么是ListView

列表视图



#### Adapter方法

完成数据源到视图列表的适配和显示。



getView方法，有多少个视图就会调用多少次。



#### ListView生成了那么多的视图，为什么没有产生oom呢？

ListView的recycleBin机制



Recycler优化

getView（View convertView）

(1)convertView[0...5]是为null的；但是当0被移出屏幕时，convertView是不为空的，可复用的。此时6再移入屏幕时，将会复用不为空的convertView;   【ListView的recycleBin机制】



(2)view是一个二叉树的过程，每一次遍历都会省去这些。



(3)三级缓存，对图片和视频做缓存，保证listview滑动的流畅性。



(4)监听滑动事件，保证listview滑动过程中，不加载图片。【做分页就可以了，必要性不强】



注意点：避免半透明的使用。比不透明的绘制更耗时间。

