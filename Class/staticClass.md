# Java中有没有静态类
``` java
public static class MyStaticClass{
}
```

## Answer
对于一个顶层的类来说，是不能用static关键字
修饰的，但是你可以用下面的方法间接的做到一些
事情
- 将一个类用 final 修饰，这样它就不能被继承
- 让构造函数变成 private，这样它就不能被实例化
- 让这个类所有的成员用static关键字修饰

例如
``` java
public class TestMyStaticClass {
     public static void main(String []args){
        MyStaticClass.setMyStaticMember(5);
        System.out.println("Static value: " + MyStaticClass.getMyStaticMember());
        System.out.println("Value squared: " + MyStaticClass.squareMyStaticMember());
        // MyStaticClass x = new MyStaticClass(); // results in compile time error
     }
}

// A top-level Java class mimicking static class behavior
public final class MyStaticClass {
    private MyStaticClass () { // private constructor
        myStaticMember = 1;
    }
    private static int myStaticMember;
    public static void setMyStaticMember(int val) {
        myStaticMember = val;
    }
    public static int getMyStaticMember() {
        return myStaticMember;
    }
    public static int squareMyStaticMember() {
        return myStaticMember * myStaticMember;
    }
}
```

这样做有什么好处呢？

有一些工具类，把它们实例化没有任何意义，
比如Math这个类:
``` java
public final class Math {

    /**
     * Don't let anyone instantiate this class.
     */
    private Math() {}

    /**
     * The {@code double} value that is closer than any other to
     * <i>e</i>, the base of the natural logarithms.
     */
    public static final double E = 2.7182818284590452354;
}
```
这样的类不需要实例化，只作为工具类。我们可以
按照上面的方法控制这个类的行为。
