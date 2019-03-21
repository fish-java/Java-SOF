# 如何轻松的打印一个数组？
``` java
int[] intArray = new int[] {1, 2, 3, 4, 5};
System.out.println(intArray);     // prints something like '[I@3343c8b3'
```

## Answer
Java 5之后，可以使用
`Array.toString(arr)`
``` java
String[] array = new String[] {"John", "Mary", "Bob"};
System.out.println(Arrays.toString(array));
// [John, Mary, Bob]
```