# StringBuild 和 StringBuffer有什么区别？

## Answer
`StringBuffer`的方法是`synchronized`的，
而`StringBuild`不是。
除非你真的要在多个线程中使用同一个String，
在单线程环境中优先使用`StringBuild`，它快一点。
