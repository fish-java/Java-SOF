# Java 支持方法的参数可以有默认值吗？
``` java
void method(String p1, int p2, bool p3=false);
```

## Ansower
Java不支持这种特性，
如果你真的有需求，你可以
- 通过方法的重载间接的支持默认
的参数值
- 使用工厂模式

### 重载
这个很简单
``` java
void method(String p1, int p2, bool p3){
  // ....
};
void method(String p1, int p2){
  bool p3 = false;
  // ... 
};
```
这样就相当于给p3一个默认的参数值。

但是有的时候如果参数太多，就不适合了。
就要用到下面的工厂方法

### 工厂方法
``` java
public class StudentBuilder
{
    private String _name;
    private int _age = 14;      // this has a default
    private String _motto = ""; // most students don't have one

    public StudentBuilder() { }

    public Student buildStudent()
    {
        return new Student(_name, _age, _motto);
    }

    public StudentBuilder name(String _name)
    {
        this._name = _name;
        return this;
    }

    public StudentBuilder age(int _age)
    {
        this._age = _age;
        return this;
    }

    public StudentBuilder motto(String _motto)
    {
        this._motto = _motto;
        return this;
    }
}
```
``` java
Student s1 = new StudentBuilder().name("Eli").buildStudent();
Student s2 = new StudentBuilder()
                 .name("Spicoli")
                 .age(16)
                 .motto("Aloha, Mr Hand")
                 .buildStudent();
```

在上面的示例中，我们没有直接
的创建一个Student对象，而是
通过StudentBuilder来创建一个工厂，
然后在这个工厂中预先设定了一些模板，

#### comments
问： 我有个疑问，我什么
我们要创建一个StudentBuilder
而不是直接这样写
```
Student s1 = new Student().age(16)
```

答：你这种写法
有两个坏处
- 实例化有些字段没有初始化，可能存在
安全隐患
- 很多时候，我们创建一个Student之后，
并不希望他有一个`.age()`方法，这个
方法可能会被滥用。

