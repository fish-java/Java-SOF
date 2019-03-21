# 如何避免 `obj != null` 这个语句？
271526

为了避免 `NullPointerException`这个异常，
我们经常这样写代码
``` java
if (someobject != null) {
    someobject.doCalc();
}
```
有没有更好的替代方法？

## Comments
1. 鼓励使用null回让我们的代码更加
的不可靠和难以阅读

2. 不使用null是一个明智的选择，抛出
一个异常而不是返回一个null。

3. 这就是我现在使用 Scala的一个原因。在
Scala中任何变量都不是nullable。

## Answers1

