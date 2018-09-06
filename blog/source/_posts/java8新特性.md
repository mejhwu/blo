---
title: Java 8 新特性
date: 2018-09-05
categories: java
mathjax: true
---

# Java 8 新特性

## Lambda表达式

lambda表达式可理解为简洁地表示可传递的匿名函数的一种方式：没有名称，有参数列表、函数主体、返回类型。

lambda表达式有3个部分：

1. 参数列表
2. 箭头(->)
3. lambda主体

下面是一个lambda表达式的例子：

```java
(int a, int b) -> a + b;
```

在上面的例子中，`(int a, int b)`是参数列表，参数类型可省略`（a, b)`。lambda主体为`a + b`。

### 函数式接口

函数式接口就是只定义了一个抽象方法的接口，比如

```java
public interface Comparator<T> {
    int compare(T o1, T o2);
}

public interface Runnable {Su
    void run();
}
```

lambda表达式允许直接以内联的形式为函数式接口的抽象方法提供实现，并把整个表达式作为函数式接口的实例。类似与匿名内部类，lambda表达式相对与匿名内部类而言更加简洁：

```java
Runnable r1 = () -> System.out.println("Hello World 1");

Runnable r2 = new Runnable() {
    public void run() {
        System.out.println("Hello World 2")
    }
}
```

函数式接口的抽象方法的签名就是lambda表达式的签名，这种抽象方法叫做函数描述符。在将lambda表达式作为参数传递或赋值给变量的时候需要做类型检测，要求lambda表达式的签名与函数式接口的抽象方法的签名一致。

常见的函数时接口有：

```java
@FunctionalInterface
public interface Predicate<T>{
    boolean test(T t);
}

@FuncationInterface
public interface Consumer<T> {
    void accept(T t);
}

@FuncationInterface
public interface Function<T, R> {
    R apply(T t)
}
```

`@FunctionInterface`用于标注该接口会设计为一个函数式接口，如果使用`@FunctionInterface`定义了一个接口，但它不是函数式接口的时候编译器就会返回一个提示原因的错误。

除了以上3个通用的函数式接口外，java8还提供了一些专为特定类型设计的接口。

| 函数式接口          | 函数描述符          | 原始类型特化                                   |
| :------------------ | ------------------- | ---------------------------------------------- |
| `Predicate<T>`      | `T -> boolean`      | `IntPredicate, LongPredicate, DoublePredicate` |
| `Consumer<T>`       | `T -> void`         | `IntConsumer, LongConsumer, DoubleConsumer`    |
| `Functino<T,R>`     | `T -> R`            | `IntFuncation<R>, IntToDoubleFunction, ... `   |
| `Supplier<T>`       | `() -> T`           | `BooleanSupplier, IntSupplier, ...`            |
| `UnaryOperator<T>`  | `T -> T`            | `IntUnaryOperator, LongUnaryOperator, ...`     |
| `BinaryOperator<T>` | `(T, T) -> T`       | `IntBinaryOperator, LongBinaryOperator, ...`   |
| `BiPredicate<L, R>` | `(L, R) -> boolean` |                                                |
| `BiConsumer<T, U>`  | `(T, U) -> void`    | `ObjIntConsumer<T>, ObjLongConsumer<T>, ...`   |
| `BiFunction<T,U,R>` | `(T, U) -> R `      | `ToIntBiFunction<T, U>, ...`                   |

### 类型检测

Lambda的类型是从使用Lambda的上下文中推断出来的，上下文中Lambda表达式需要的类型称为目标类型。统一个Lambda表达式可以与不同的函数式接口联系起来，只要它们的抽象方法的签名能够兼容。比如`Callable`和`PrivilegeAction`的抽象方法的方法签名都是无参数并返回一个T。

```java
Callable<Integer> c = () -> 42;
PrevilegedAction<Integer> p = () -> 42;
```

### 方法引用

方法引用就是让你可以重复使用现有的方法定义，并可以想Lambda表达式一样传递。

方法引用主要有三类：

（1） 只想静态方法的方法引用（如`Interger`的`parseInt`方法，写作`Integer::parseInt`）

（2） 指向任意类型实例方法的方法引用（如`String`的`length`方法，写作`String::length`）

（3） 指向现有对象的的实例方法。

方法引用可以与Lambda相对应。

（1） Lambda   ———      `(args) -> ClassName.staticMethod(args)`

​           方法引用  ———      `ClassName::staticMethod`

（2） Lambda   ———      `(arg0, arg1) -> arg0.instanceMethod(arg1)`

​           方法引用  ———      `ClassName::instanceMethod`

（3） Lambda   ———      `(args) -> expr.instanceMethod(args)`

​           方法引用   ———      `expr::instanceMethod`

对于一个现有的构造函数，可以利用它的名称和关键字`new`来创建一个引用：`ClassName::new`。

```java
Supplier<Apple> s = Apple::new;
Apple a = s.get();

等价于

Supplier<Apple> s = () -> new Apple();
Apple a = s.get();
```

## 流

流简单来说就是“从支持数据处理操作的源生成的元素序列”。流操作的两个重要特点：

1. 流水线 —— 很多流操作本身会返回一个流，这样多个操作就可以链接起来，形成一个大的流水线。
2. 内部迭代 —— 与使用迭代器显示迭代不同，流的迭代操作是在背后进行的。

流中的数据只能遍历一次，遍历完后，这个流就已经被消费掉了。

`java.util.stream.Stream`接口中定义了许多操作，可以大致分为两类，中间操作和终端操作。中间操作会返回另外一个流，终端操作会从流的流水线生成结果。

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
long res = numbers.stream()
    .filter(n -> n > 3)
    .map(n -> n * n)
    .count();
```

| 操作     | 类型 | 返回类型  | 函数描述符    |
| -------- | ---- | --------- | ------------- |
| filter   | 中间 | Stream<T> | T -> boolean  |
| map      | 中间 | Stream<R> | T -> R        |
| limit    | 中间 | Stream<T> |               |
| sorted   | 中间 | Stream<T> | (T, T) -> int |
| distinct | 中间 | Stream<T> |               |
|          |      |           |               |

| 操作    | 类型 | 目的                                           |
| ------- | ---- | ---------------------------------------------- |
| forEach | 终端 | 消费流中的每个元素并对其应用Lambda。返回void。 |
| count   | 终端 | 返回流中元素的个数。返回long。                 |
| collect | 终端 | 把流归约成一个集合，比如List、Map、Integer。   |

### 筛选和切片

`Stream`接口支持`filter`，该操作会接受一个谓词（一个返回`boolean`的函数）作为参数，并返回一个包括所有符合谓词的元素的流。

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> odds = numbers.stream()
    .filter(n -> n % 2 == 1).collect(toList());
```

`distinct()`方法会返回一个元素各异（根据流锁生成元素的`hashCode`和`equals`方法是实现）。

```java
List<Integer> numbers = Arrays.asList(1, 2, 1, 3, 3, 2, 4);
numbers.stream().filter(i -> i % 2 == 0)
    .distinct().forEach(System.out::println);
```

`limit(n)`方法会返回一个不超过给定长度的流，所需的长度作为参数传递给`limit`。

```java
List<Integer> numbers = Arrays.asList(1, 2, 1, 3, 3, 2, 4, 5, 6, 7, 8);
numbers.stream().filter(i -> i % 2 == 0)
    .limit(3).forEach(System.out::println);
```

`skip(n)`方法返回一个扔掉了前n个元素的流，如果流中元素不足n个，则返回一个空流。`limit(n)`和`skip(n)`是互补的。

```java
List<Integer> numbers = Arrays.asList(1, 2, 1, 3, 3, 2, 4, 5, 6, 7, 8);
numbers.stream().filter(i -> i % 2 == 0)
    .skip(2).forEach(System.out::println);
```

### 映射

`map`方法接受一个函数作为参数，这个函数会被应用到每个元素上，并将其映射成一个新的元素，返回一个新元素的流。

```java
List<String> words = Arrays.asList("Java 8", "Lambdas", "In", "Actions");
List<Integer> wordLengths = words.stream()
    .map(String::length).collect(toList());
```

`flatMap`方法将一个流中的每个值都换成另一个流，然后把所有的流连接起来成为一个流。简而言之，就是把流中的函数参数所产生的流中的元素提取出来后组合为一个新的流。

```java
List<String> words = Arrays.asList("Java 8", "Lambdas", "In", "Actions");
List<String> uniqueCharacters = 
    words.stream()
    .map(w -> w.split(""))   // 返回Stream<String[]>
    // Array::stream将String[]转换为Stream<String>, flatMap将所                             // 有Stream中的String提取出来并合成为一个新的Stream<String>
    .flatMap(Arrays::stream)  
    .distinct()
    .collect(toList())
```

### 查找和匹配

`anyMatch`可以检查流中是否有一个元素能匹配给定的谓词。

`allMatch`检查流中的元素是否都能匹配给定谓词。

`noneMatch`确保流中没有任何元素与给定谓词匹配。

`findAny`方法将返回当前流中的任意元素。

`findFirst`方法查找流中第一个元素。

### 归约

`reduce`操作可以将流中所有元素反复结合起来，得到一个值，这样的查询操作被称为归约操作（将流归约为一个值）。

```java
// 元素求和
int sum = numbers.stream().reduce(0, (a ,b) -> a + b);
```

`reduce`接受两个参数：

1. 一个是初始值。
2. 一个`BinaryOperator<T>`来将两个元素结合起来产生一个新值。

`reduce`还有一个重载变体，它不接受初始值，但是会返回一个`Opetional`对象。

```java
Opetional<Integer> sum = numbers.stream().reduce((a, b) -> a + b);
```

### 构建流

可直接使用静态方法`Stream.of`方法，通过显示值创建一个流，它接受任意数量的参数。

```java
Stream<String> stream = Stream.of("Java 8", "Lambdas", "In", "Action");
stream.map(String::toUpperCase).forEach(System.out::println);
```

可以使用`empty`得到一个空流。

```java
Stream<String> emptySteam = Stream.empty();
```

可以使用静态方法`Arrays.stream`从数组创建一个流，它接受一个数组作为参数。

```java
int[] numbers = {2, 3, 5, 7, 11, 13};
int sum = Arrays.stream(numbers);
```

`Stream API`提供了两个静态方法来从函数生成流：`Stream.iterate`和`Stream.generate`。这两个操作可以创建无限流。

```java
Stream.iterate(0, n -> n + 2).limit(10).forEach(System.out::println);
Stream.generate(Math::random).limit(5).forEach(System.out::println);
```

### 收集器

