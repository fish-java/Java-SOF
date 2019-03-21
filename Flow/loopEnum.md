# 如何遍历一个 enum类型
``` java
public enum Direction {
   NORTH,
   NORTHEAST,
   EAST,
   SOUTHEAST,
   SOUTH,
   SOUTHWEST,
   WEST,
   NORTHWEST
}
```
使用for loop之类的方法？

## Answer
你可以视同`.values()`
``` java
for (Direction dir : Direction.values()) {
  // do what you want
}
```