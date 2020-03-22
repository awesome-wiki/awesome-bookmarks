# Java 经验总结

## 对象拷贝

避免用 Apache Beanutils 进行属性的 copy。 说明：Apache BeanUtils 性能较差，可以使用其他方案比如 Spring BeanUtils：

```java
//apach
BeanUtils.copyProperties(to, from)
// spring
BeanUtils.copyProperties(from, to);
```

## 循环中的字符串拼接

一般的字符串拼接在编译期间 java 会进行优化，但是在循环中字符串拼接，java 编译期就无法做到优化，需要使用 `StringBuilder` 进行替换：

```java
// 一般字符串拼接
String a = "a";
String b = "b";
String c = "c";
String s = a + b + c; 
// 循环字符串拼接
StringBuilder sb = new StringBuilder();
for (int i = 0; i < 10; i++) {
    sb.append(i);  // 循环中，java编译器无法进行优化，所以要手动使用StringBuilder
}
```

参考：
- [Java 字符串拼接效率分析及最佳实践](https://segmentfault.com/a/1190000007099818)
- [教你消灭 Java 代码的“坏味道”](https://mp.weixin.qq.com/s?__biz=MzI3NzE0NjcwMg==&mid=2650124774&idx=2&sn=5bbd57d953644186db318f596579b9f7&chksm=f36bacc7c41c25d19d81d33f068c24e0e549ffb5554d3390ad3f1243549b836d469836ab7714&mpshare=1&scene=1&srcid=&sharer_sharetime=1568872265144&sharer_shareid=ae8eb1508a08c1b134df82bb484ea38d#rd)

## 将一切转为 POJO 对象

依赖：
```shell
<dependency>
    <groupId>com.alibaba</groupId>
    <artifactId>fastjson</artifactId>
    <version>1.2.58</version>
</dependency>
```

```java
User user = JSONObject.parseObject(jsonStr, User.class);
```

除此以外，还有：
- 需要操作 Excel ，例如从 Excel 中读取出用户的信息，然后进行批量的插入操作 EasyPoi
- 将配置文件转换成 POJO 对象  owner
- 处理 shell 命令时可能会用到的工具  JCommander

更多阅读[将一切都转成 POJO 对象再说](https://mp.weixin.qq.com/s?__biz=MzA3MTQ2MDgyOQ==&mid=2247484244&idx=1&sn=1c1a8cf5db57f8f4af0b0150a5b986a7&chksm=9f2c71e6a85bf8f0885a4864d54b450edbd8c06d16157da54445cf539cdddc339a700e01bd90&mpshare=1&scene=1&srcid=&sharer_sharetime=1567818428762&sharer_shareid=ae8eb1508a08c1b134df82bb484ea38d#rd)