---
title: java note
weight: 20
menu:
  notes:
    name: Java Note
    identifier: java-stream
    parent: java
    weight: 20
---

{{< note title="Java 各类集合 / 数组之间的标准互转套路" >}}

## 核心认知

1. 对象流 vs. 基本类型流
   - `Stream<T>：List<Integer> / Set<Integer>`
   - `IntStream / LongStream / DoubleStream：int[] / long[] / double[]`

## List / Set / Map 之间的转换

### 1. List ⇄ Set（去重 / 保序）

##### List → Set（去重）

```java
// 使用Stream
Set<Integer> set = list.stream()
        .collect(Collectors.toSet());

// ⚠️保序去重
Set<Integer> set = new LinkedHashSet<>(list);
```

##### Set → List

```
List<Integer> list = set.stream().toList();
```

### 2. Map ⇄ List / Set（高频）

#### Map → key / value 集合

```
Map<String, Integer> map = ...

Set<String> keys = map.keySet();
Collection<Integer> values = map.values();
```

#### Map → List（entry）

```java
List<Map.Entry<String, Integer>> entries =
        new ArrayList<>(map.entrySet());
```

#### list → map（元素本身当 key）

```java
List<Integer> list = ...

Map<Integer, Integer> map = list.stream()
        .collect(Collectors.toMap(
                x -> x, // 数本身
                x -> 1, // 先记一次
                Integer::sum   // 处理重复 key
        ));
```

## List / Set ⇄ 数组

### 1. List< Integer> ⇄ int[]

##### List< Integer> → int[]

```java
int[] arr = list.stream()
        .mapToInt(Integer::intValue)
        .toArray();
```

##### int[] → List< Integer>

```java
List<Integer> list = Arrays.stream(arr)
        .boxed() // 📌boxed()：基本类型 → 包装类型
        .toList(); // 使用toList方法，得到的list是不可变的
```

### 2. Set< Integer> ⇄ int[]

##### Set → int[]

```
int[] arr = set.stream()
        .mapToInt(Integer::intValue)
        .toArray();
```

##### int[] → Set

```
Set<Integer> set = Arrays.stream(arr)
        .boxed()
        .collect(Collectors.toSet());
```

{{< /note >}}
