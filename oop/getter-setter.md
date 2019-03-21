# 为什么使用getter/setter方法？不是多此一举吗？
1568091

``` java
public String foo;
```
上面的代码真的不如下面的吗？
``` java
private String foo;
public void setFoo(String foo) { this.foo = foo; }
public String getFoo() { return foo; }
```
下面这种写法有什么意义吗
## Answer
这样写有很多好处

#### 很好的封装了对象的行为
如果你日后希望在别人访问这个字段的
时候做出一些额外的事情，那么一开始就
使用getter/setter方法可以让你更加
轻松的修改。getter/setter方法就是
天生的拦截器
``` java
private String foo;
public void setFoo(String foo) { 
  this.foo = foo;
  System.out.println("you are setting foo");
}
public String getFoo() { 
  System.out.println("you relize you need" + 
    " do something two month later");
  return foo; }
```

#### Read only
如果你只实现了get而没有实现set，那么
这个字段就是read only

#### 隐藏了对象的内部信息。
  
``` java
private char[] name;
public void setName(String foo) {
  this.name = foo.toCharArray(); 
}
public String getName() { 
  return  String.valueOf(name);
 }
```
你以为name是String，其实它是char[].

#### 方便Debug
你可以在set get方法上打断点，
来探索运行时这个对象的属性的值是
什么时候发生改变的。很多时候这非常有用。

#### 允许子类做更多的事情
子类可以通过覆盖父类的getter settter方法，
来改变一些事情

#### 内存管理
允许你对这个字段占用的
内存手动的管理

#### 更好的访问权限控制
``` java
private String foo;
public void setFoo(String foo) { this.foo = foo; }
protected String getFoo() { return foo; }
```
getter 和 setter有不同的访问控制符

### 总结
多了getter 和 setter，你可以
做更多的事了

## Answer2
我来说说不好的地方

如果有其他程序员在setter/getter方法
做了一些奇奇怪怪的，这对后来者是一个噩梦
我曾经接手过一个程序，它用了很多setter/getter方法。
有次我遇到了一个bug，请看这样的代码
``` java
person.setName("Joe");
```
我debug了很长时间，才返现
它在setter方法中同时 set 了
 person.firstName, person.lastName, 
person.isHuman, person.hasReallyCommonFirstName,
 and calls person.update()
这真是一个噩梦。

## Answer 3
不使用setter getter的理由

1. 如果你真的需要对get / set进行
监控的话，你只需要让这个字段变为private，
然后编辑器就会提醒你你在哪些地方使用了这个
值，你前往相关的代码进行处理就行了，没必要
使用getter setter 方法

2. 在setter 方法中对字段进行校验真的很少用，
你在给对象赋值前进行处理不就行了？

3. 如果你在setter方法对参数的值做出了修改，
这对调用这个方法的人来说是一个噩梦

4. 你确实可以在子类继承的时候覆盖父类的方法，
但是，这对调用者来说真的很容易出错。

不要使用getter setter 除非你真的
有这种需求，未来可能的需求不用在乎。
