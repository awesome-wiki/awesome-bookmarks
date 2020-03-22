# Java Map 相关的常用操作

```java
Map<String, String> hashMap = new HashMap();
        // 增加元素
        hashMap.put("name", "michael");
        hashMap.put("age", "27");
        // key 存在，会被覆盖
        hashMap.put("age", "28");
        // key 存在，不会覆盖
        hashMap.putIfAbsent("age", "30");
        // key 不存在，成功赋值
        hashMap.putIfAbsent("sex", "man");
        System.out.println(hashMap);

        // 获取元素
        System.out.println(hashMap.get("name"));
        // 如果没有key值，也不会报错，返回 null
        System.out.println(hashMap.get("michael"));
        // 如果key有值，就取已有的值，Java 8 开始具有的方法
        System.out.println(hashMap.getOrDefault("age", "29"));
        // 如果没有key值，就取设置的默认值
        System.out.println(hashMap.getOrDefault("school", "DUT"));
        System.out.println(hashMap);

        // 遍历
        // 方法一
        Iterator iterator1 = hashMap.keySet().iterator();
        while (iterator1.hasNext()) {
            String key = (String) iterator1.next();
            System.out.println(key + "=" + hashMap.get(key));
        }
        // 方法二
        Iterator iterator2 = hashMap.entrySet().iterator();
        while (iterator2.hasNext()) {
            Map.Entry entry = (Map.Entry) iterator2.next();
            String key = (String) entry.getKey();
            String value = (String) entry.getValue();
            System.out.println(key + "=" + value);
        }
        // 当循环中只需要 Map 的主键时，迭代 keySet() 是正确的。但是，当需要主键和取值时，迭代 entrySet() 才是更高效的做法，比先迭代 keySet() 后再去 get 取值性能更佳

        // map 大小
        System.out.println("size():" + hashMap.size());
        System.out.println("values():" + hashMap.values());

        // 替换元素
        System.out.println(hashMap);
        // key 存在，替换OK
        hashMap.replace("name", "Michael");
        System.out.println(hashMap);
        // key 不存在，不会报错，也不会添加
        hashMap.replace("place", "HangZhou");
        System.out.println(hashMap);

        // 判断key是否存在
        System.out.println(hashMap.containsKey("name"));
        // 判断value是否存在
        System.out.println(hashMap.containsValue("name"));

        // 删除元素
        // key 存在，删除时，返回key对应的值
        System.out.println(hashMap.remove("age"));
        System.out.println(hashMap);
        // key 不存在，删除时，返回null
        System.out.println(hashMap.remove("year"));
        System.out.println(hashMap);
        // key 存在，参数和 key 对应的value 值一致，返回 true，key 元素被删除
        System.out.println(hashMap.remove("sex", "man"));
        System.out.println(hashMap);
        // key 存在，参数和 key 对应的value 值不一致，返回 false，key 元素不被删除
        System.out.println(hashMap.remove("name", "qq"));
        System.out.println(hashMap);
```