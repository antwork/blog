---
date: 2014-11-12 22:48:12
layout: post
title: "Java多态-继承-组合学习笔记"
description: "Java多态-继承-组合学习笔记"
category: 日志
tags: java 
---


###备注:	
继承子类的方法使用@Override重载父类方法中,需要显式调用super.XX(),父类中方法才会执行.	

```	

package com.cateatcode;

// 以下是父类
public class Shape {
	public void draw () {
		System.out.println("Shape.draw()");
		
	}
	
	public void erase() {}
	
	// 父类中的方法,如果子类不重载,则默认继承父类行为
	public void baseMethod() {
		System.out.println("Shape.baseMethod()");
	}
}


package com.cateatcode;

// 以下是子类
public class Square extends Shape {
	
	@Override
	public void draw() {
		super.draw(); //显式调用父类
		System.out.println("Square.draw()");
	}
	
	@Override
	public void erase() {
		System.out.println("Square.erase()");
	}
}



```		

不包含任何类的抽象类不能被初始化		

