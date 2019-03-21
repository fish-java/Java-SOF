# 如何跳出双重循环？
``` java
for (Type type : types) {
    for (Type t : types2) {
         if (some condition) {
             // Do something and break...
             break; // Breaks out of the inner loop
         }
    }
}
```
上面的break只能跳出第一重循环

## Answer
你可以给循环添加一个label
``` java
outLoop:
for (int i = 0; i < 4; i++) {
  for (int j = 0; j < 4; j++) {
    if(i == 2 && j == 2){
      break outLoop;
    }
  }
}
```

## Answer 2
上面使用label的方法是正解，但是
在实践中你应该把你的双重循环
放在一个单独的函数中，然后使用return
退出函数
``` java
 public class Test {
    public static void main(String[] args) {
        loop();
        System.out.println("Done");
    }

    public static void loop() {
        for (int i = 0; i < 5; i++) {
            for (int j = 0; j < 5; j++) {
                if (i * j > 6) {
                    System.out.println("Breaking");
                    return;
                }
                System.out.println(i + " " + j);
            }
        }
    }
}
```

## Answer 3
我从来不我使用label，这回让代码
难以理解
``` java
boolean finished = false;
for (int i = 0; i < 5 && !finished; i++) {
    for (int j = 0; j < 5; j++) {
        if (i * j > 6) {
            finished = true;
            break;
        }
    }
}
```