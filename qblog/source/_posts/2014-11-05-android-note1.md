---
date: 2014-11-05 22:40:12
layout: post
title: 安卓笔记-Building Your First App
categories: 日志
tags: android
---
##安卓笔记-Building Your First App

暂时支持四种布局   

* Linear Layout
* Relative Layout
* List View
* Grid View

###wrap_content和match_parent的区别
* wrap_content:根据内容的大小来布局
* match_parent:尽可能跟父视图一样大小

wrap_content tells your view to size itself to the dimensions required by its content.
match_parent (named fill_parent before API Level 8) tells your view to become as big as its parent view group will allow.

布局中不推荐使用绝对值,而采用wrap_content,match_parent,dp这三种
dp:density-independent pixel units 解释:密度独立的像素单元

padding: setPadding(int, int, int, int)
getPaddingLeft(),...

####通俗布局

-------------


weight默认为0,如果为多个视图中的一个视图指定weight大于0,这个视图将会填充完其他视图填充剩余的视图,为了提高布局效率,需要将其layout_width="0dp",因为布局是相对的,在布局的时候会对所有的视图进行一遍计算,将其设置为0可以优先配置好其他,然后剩余给到这个视图


布局位置:

获取方法: ```getLeft() getRight() getTop() getBottom()```
例如: getLeft()等于20意味着视图跟左边间距为20;


Load the XML Resource 

``` 
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main_layout);
}
```

使用一个Button的例子

1. 在xml中创建一个Button

```
<Button android:id="@+id/my_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/my_button_text"/>
```
2. 使用

```
Button myButton = (Button)findViewById(R.id.my_button)
```

Intent演示:

```
/** Called when the user clicks the Send button */
public void sendMessage(View view) {
    Intent intent = new Intent(this, DisplayMessageActivity.class);
    EditText editText = (EditText) findViewById(R.id.edit_message);
    String message = editText.getText().toString();
    intent.putExtra(EXTRA_MESSAGE, message);
    startActivity(intent);
}
```


