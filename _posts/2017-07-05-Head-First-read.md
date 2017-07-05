---
layout: post
title: Head First 设计模式
bigimg: /img/sjms/sjms.jpg
---

观察者模式
-----
![sjms](https://github.com/Victooory/victooory.github.io/raw/master/img/post/sjms/sjms1.png) <br>

 - 概述：在对象之间定义一对多的依赖，这样一来，当一个对象改变状态，依赖它的对象都会收到通知，并自动更新。
交互对象之间松耦合，可以随意加入或删除观察者，而且也不在乎观察者的具体实现，只要实现了特定接口就行
 - 实现：主题类实现subject接口( register、remove、notify)，观察者类实现observer接口(update),在subject类中用数组保存观察者，register(observer)就是把实现observer类add()到数组中，发送信息就是通过遍历数组调用每个observer的update(),在observer中，update来获取subject传过来的信息

装饰者模式
-----
![sjms](https://github.com/Victooory/victooory.github.io/raw/master/img/post/sjms/sjms2.png) <br>

 - 概述：动态的为被装饰者添加装饰，装饰者和被装饰者有共同超类，形成的新类也可再装饰，使得装饰者可以被复用的设计模式
 - 实现：在装饰者中注入被装饰着，对属性进行合并形成新类
 
工厂模式
-----
![sjms](https://github.com/Victooory/victooory.github.io/raw/master/img/post/sjms/sjms3.png) <br>

 - 概述：定义了一个创建对象的接口，但由子类决定要实例化哪个类。工厂模式用来封装对象的创建
 - 实现：定义一个抽象工厂方法，子类实现此方法制造产品；不同工厂生产的产品实现相同的接口
 - 个人理解：工厂模式加上反射机制就是IOC嘛
 
单例模式
-----
![sjms](https://github.com/Victooory/victooory.github.io/raw/master/img/post/sjms/sjms4.png) <br>

 - 概述：确保一个类只有一个实例，并提供一个全局访问点
 - 实现：构造方法设为私有，用一个静态变量来记录类本身是否被实例，调用静态方法如果该类没被实例就实例化该类，如果被实例了就返回该类的静态变量,多线程中可能同时创建两个实例，所以应该对getInstance加锁，但是由于每个此创建都要进入判断，所以：<br>
1.饿汉加载：在静态初始化器中创建单件，使得JVM在加载这个类是就创建这个单例的实例，在getInstance中返回这个实例<br>
2.双重检查加锁：对UniqueInstance加关键字volatile，检查是否已经创建，未创建再加锁，再判断是否实例化 <br>

适配器模式
-----
![sjms](https://github.com/Victooory/victooory.github.io/raw/master/img/post/sjms/sjms5.png) <br>

 - 概述：将一个类的接口，装换成客户期望的另一个接口，适配器让原本接口不兼容的类可以合作无间
 - 实现：适配器继承期望接口，取得适配对象的引用（可以用构造器），实现接口中的所有方法 
 - Duck turkeyAdapter = newTurkeyAdapter(turkey)

原则
-----
1.找出程序中会变化的方面，然后将其和固定不变的方面相分离。<br>
2.把行为声明为接口类型，用实现这个行为接口的实现类去实例化(多态)，可以在子类中对父类声明的行为接口实例化(或用set方法动态设定)<br>
3.针对接口编程，不针对实现编程。<br>
4.多用组合，少用继承。<br>
5.依赖抽象，而不是依赖具体类<br>


 








