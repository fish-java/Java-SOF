# 如何将String转换成Int？
`"123"` -> `123`

## Answer
``` java
String s = "124";
Integer integer = Integer.valueOf(s);
int i = Integer.parseInt(s);
```
如果字符串不符合格式，会抛出`NumberFormatException`。
（至于什么样的字符串能转化整数，大家都懂吧，这个东西用语言
描述太难了）

