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

#### 归约和汇总

`Collectors.maxBy和Collectors.minBy`用于计算流中的最大或最小值。

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
Optional<Integer> max = numbers.stream()
    .collect(Collectors.maxBy(Integer::compare));
Optional<Integer> max = numbers.stream()
    .collect(Collectors.minBy(Integer::compare));
```

`Collectors.summingInt`接受一个把对象映射为求和所需的`int`的函数。

```java
List<Double> doubles = Arrays.asList(1.0, 2.0, 3.0, 4.0, 5.0);
int total = doubles.stream()
    .collect(Collectors.summingInt(d -> (int)d.longValue()));
```

`Collectors`还是提供了求和`long`字段的`summingLong`和求和`double`字段的`summingDouble`，还有求和平均数：`Collectors.averagingInt、Collectors.averagingLong和Collectors.averagingDouble`。`summarizing`操作可以同时求出总和、平均值、最大值和最小值，其返回类型为`IntSummaryStatistics`。

`joinging`工厂方法返回的收集器会把对流中每一个对象应用`toString`方法得到的所有字符串连接成一个字符串。

```java
String shortMenu = menu.stream().map(Dish::getName).collect(joining());
```

`joining`在内部使用了`StringBuilder`来把生成的字符串逐个追加起来。此外，如果流中元素实现了`toString()`，可以直接使用对象流执行`collect`，无需对元素进行`map`操作。`joining`工厂具有一个重载版本可以接受元素之间的分界符。

```java
String shortMenu = menu.stream().map(Dish::getName).collect(joining(", "));
```

广义上的归约操作可以用`reducing`工厂方法定义，`reducing`接受3个参数。

（1）第一个参数是归约操作的起始值，页就是流中没有元素时的返回值。

（2）第二个参数就是得到归约元素的函数。

（3）第三个参数是一个`BinaryOperator`，将两个项目累积成一个同类型的值。

```java
int totalCalories = menu.stream().collect(reducing(
		0, Dish::getCalories, (i, j) -> i + j));
```

同样，`reducing`也接受单参数形式。可以版单参数`reducing`工厂方法创建的收集器看作三参数方法的特殊情况，它把流中的第一个项目作为起点，把恒等函数（即一个函数仅仅是返回其输入参数）作为一个转换函数。

#### 分组

`Collectors.groupingBy`工厂方法返回的收集器可以轻松实现分组任务。

```java
Map<Dish.Type, List<Dish> dishesByType = 
    menu.stream().collect(groupingBy(Dish::getType));
```

多级分组可以使用由双参数版本的`Collectors.groupingBy`工厂方法创建的收集器，可以接受`Collector`类型的第二个参数。

```java
Map<Dish.Type, Map<CaloricLevel, List<Dish>>> dishesByTypeCaloricLevel = 
    menu.stream().collect(
		groupingBy(Dish::getType, 
                   groupingBy(dish -> {
                       if (dish.getCalories() <= 400)
                           return CaloricLevel.DIET;
                       else if (dish.getCalories() <= 700)
                           return CaloricLevel.NORMAL;
                       else
                           return CaloricLevel.FAT;
                   }))	
	)
```



#### 分区

分区是分组的特殊情况：由一个谓词（返回一个布尔值的函数）作为分类函数，称为分区函数。分区函数返回一个布尔值，这意味这得到的分组`Map`的键值类型是`Boolean`，于是最多可以分为两组——`true`为一组，`false`是一组。

```java
Map<Boolean, List<Dish>> partitionedMenu = 
    menu.stream().collect(partioningBy(Dish::isVegetarian));
```

`partitioningBy`工厂方法有一个重载版本，可以传递第二个收集器。

| 工厂方法            | 返回类型                | 用于                                                         |
| ------------------- | ----------------------- | ------------------------------------------------------------ |
| `toList`            | `List<T>`               | 把流中所有项目收集到一个`List`                               |
| `toSet`             | `Set<T>`                | 把流中所有项目收集到一个`Set`，删除重复项                    |
| `toCollection`      | `Collection<T>`         | 把流中所有项目收集到给定的供应源创建的集合                   |
| `counting`          | `Long`                  | 计算流中元素的个数                                           |
| `summingInt`        | `Integer`               | 对流中项目的一个整数属性求和                                 |
| `averagingInt`      | `Double`                | 计算流中项目`Integer`属性的平均值                            |
| `joining`           | `String`                | 连接对流中每个项目调用`toString`方法所生成的字符串           |
| `maxBy`             | `Optional<T>`           | 一个包裹了流中按照给定比较器选出最大元素的`Optional`，或如果流为空则为`Optional.empty()` |
| `minBy`             | `Optional<T>`           | 一个包裹了流中按照给定比较器选出最小元素的`Optional`，或如果流为空则为`Optional.empty()` |
| `reducing`          | 归约操作产生的类型      | 从一个作为累加器的初始值开始，利用`BinaryOperator`与流中的元素逐个结合，从而将流归约为单个值 |
| `collectingAndThen` | 转换函数返回的类型      | 包裹另一个收集器，对其结果应用转换函数                       |
| `groupingBy`        | `Map<K, List<T>>`       | 根据项目的一个属性值对流中的项目作分组，并将属性值作为结果`Map`的键 |
| `partitioningBy`    | `Map<Boolean, List<T>>` | 根据对流中每个项目应用谓词的结果来对项目进行分区             |

#### 收集器接口

`Collector`接口包含了一系列方法，为实现具体的归约操作（即收集器）提供了范本。`Collector`接口定义：

```java
public interface Collector<T, A, R> {
    Supplier<A> supplier();
    BiConfumer(A, T) accumulator();
    Function<A, R> finisher();
    BinaryOperator<A> combiner();
    Set<Characteristics> characteristics();   
}
```

其中：

（1）T是流中要收集的项目的泛型。

（2）A是累加器的类型，累加器是在收集过程中用于累积部分结果的对象。

（3）R是收集操作得到的对象（通常单并不一定是集合）的类型。

理解`Collector`接口声明的方法。

1. 建立新的结果容器：`supplier`方法

   `supplier`方法必须返回一个结果为空的`Supplier`，也就就是一个无参函数，在调用是它会创建一个空的累加器实例，供数据收集过程使用。

```java
public Supplier<List<T>> supplier() {
    return ArrayList::new;
}
```

2. 将元素添加到结果容器：`accumulator`方法

   `accumulator`方法会返回执行归约方法的元素。当遍历到流中第$n$个元素时，这个函数执行时会有两个参数：保存归约结果的累加器（已收集了流中的前$n-1$个项目），还有第$n$个元素本身。该函数返回`void`，因为累加器是原味更新，即函数的执行改变了它的内部状态以体现遍历元素的效果。

```java
public BiConsumer<List<T>, T> accumulator() {
    return List::add;
} 
```

3. 对结果容器应用最终转换：`finisher`方法

   在遍历完流后，`finisher`方法必须返回在累积过程的最后要调用的一个函数，以便将累加器对象转换为整个集合操作的最终结果。

```java
public Function<List<T>, List<T>> finisher() {
    return Function.identity();
}
```

4. 合并两个结果容器：`combiner`方法

   `combiner`方法会返回一个供归约操作使用的函数，它定义了对流的各个子部分并行处理时，各个子部分归约所得的累加器要如何合并。

```java
public BinaryOperator<List<T>> combiner() {
    return (list1, list2) -> {
        list1.addAll(list2);
        return list1;
    }
}
```

5. `characteristic`方法

   `characteristics`会返回一个不可变的`Characteristic`集合，它定义了收集器的行为——尤其是关于流是否可以并行归约，以及可以用哪些优化的体式。`Characteristic`是一个包含三个项目的枚举。

   `UNORDERED`——归约结果不受流中项目的遍历和累积顺序的影响。

   `CONCURRENT`——`accumulator`函数可以从多个线程同时调用，且该收集器可以并行归约流。

   `IDENTITY——FINISH`表明完成器是放回的函数是一个恒等函数，可以跳过。

### 并行数据处理

#### 并行流

并行流就是将内容分成多个数据块，并用不同的线程分布处理每个数据块的流。`parrallel`方法可以把顺序流变换为并行流，`sequential`可以把并行流转换为顺序流。

```java
stream.parallel()
      .filter(...)
      .sequential()
      .map(...)
      .parallel()
      .reduce();
```

#### 分支/合并框架

分支/合并框架的目的是以递归方式将并行任务拆分为更小的任务，然后将每个子任务的结果合并起来生成整体结果。它是`ExecutorService`接口的一个实现，它把子任务分配给线程池（称为`ForkJoinPool`）中的工作线程。

要把任务提交到线程池，必须创建`RecursiveTask<R>`的一个子类，其中`R`是并行化任务（以及所有子任务）产生的结果，或者如果任务不返回结果，则是`RecursiveAction`类型（当然它可能会更新其他非局部机构）。要定义`RecursiveTask`，只需要实现它唯一的抽象方法`compute`：

```java
protected abstract R compute();
```

工作窃取：在实际应用中，任务差不多被平均分配到`ForkJoinPool`中的所有线程上。每个线程都为分配给它的任务保持一个双向队列，每完成一个任务，就会从队列头上取下一个任务开始执行。当有线程很早就完成了分配的所有任务，就开始随机选择一个别的线程，从队尾取下一个任务执行。

#### `Spliterator`

`Spliterator`接口。

```java
public interface Spliterator<T> {
    boolean tryAdvance(Consumer<? super T> action);
    Spliterator<T> trySplit();
    long estimateSize();
    int characteristics();
}
```

`tryAdvance`方法会顺序使用`Spliterator`中的元素。`trySplit`可以将一些元素划分出去分给第二个`Spliterator`（由该方法返回），让它们两个并行处理。`estimateSize`方法估计还剩下多少元素要遍历。`characteristics`方法将返回一个int，代表`Spliterator`本身特性集的编码。

`spliterator`的特性

| 特性         | 含义                                                         |
| ------------ | ------------------------------------------------------------ |
| `ORDERED`    | 元素有既定的顺序（例如List），因此`Spliterator`在遍历和划分式也会遵循这一顺序 |
| `DISTINCT`   | 对于任意一对遍历过的元素x和y，`x.equals(y)`返回false         |
| `SORTED`     | 遍历的元素安装一定的预定义的顺序排序                         |
| `SIEZED`     | 该`Spliterator`由一个已知大小的源建立（例如`Set`），因此，`estimateSize()`返回的是准确值 |
| `NONNULL`    | 保证遍历的元素不会为`null`                                   |
| `IMMUTABLE`  | `Spliterator`的数据源不能修改，这意味这在遍历时不能添加、删除或修改任何元素 |
| `CONCURRENT` | 该`Spliterator`的数据源可以被其他线程同时修改和无需 同步     |
| `SUBSIZED`   | 该`Spliterator`和所有从它拆分处理的`Spliterator`都是`SIZED`  |

## 默认方法

默认方法由`default`修饰符修饰，并像类中声明的其他方法一样包含方法体。

```java
public interface Sized {
    int size();
    default boolean isEmpty() {
        return size() == 0;
    }
}
```

同时`implements`多个接口时冲突解决的方法：

1. 类中的方法优先级最高，类或父类中声明的方法的优先级高于任何声明为默认方法的优先级。
2. 如果无法依据第一条件进行判断，那么子接口的优先级更高：函数签名相同时，优先选择拥有最具体的默认方法的接口，即如果B继承了A，那么B就比A更加具体。
3. 最后，如果还是无法判断，继承了多个接口的类必须通过显示覆盖和调用期望的方法。

## Optional

变量存在时，`Optional`类只是对类简单封装。变量不存在时，缺失值会被建模成一个“空”的`Optional`对象，有方法`Optional.empty()`返回。`Optional.emtpy()`方法是一个静态工厂方法，它返回`Optional`类的特定单一实例。`Optional`对象可执行与流类似的操作，如`filter、map、flatMap`等。

`Optional`类的方法

| 方法          | 描述                                                         |
| ------------- | ------------------------------------------------------------ |
| `empty`       | 返回一个空的`Optional`实例                                   |
| `filter`      | 如果值存在并且满足提供的谓词，就放回包含该值的`Optional`对象；否则返回一个空的`Optional`对象 |
| `flatMap`     | 如果值存在，就对该值执行提供的mapping函数，返回一个`Optional`类型的值，否则返回一个空的`Optional`对象 |
| `get`         | 如果该值存在，将该值用`Optional`封装返回，否则抛出一个`NoSuchElementException`异常 |
| `ifPresent`   | 如果值存在，就执行使用该值的方法调用，否则什么也不做         |
| `isPresent`   | 如果值存在就返回true，否则返回false                          |
| `map`         | 如果值存在，就对该值执行mapping操作                          |
| `of`          | 将指定值用`Optional`封装之后返回，如果该值为null，则抛出一个`NullPointerException`异常 |
| `ofNullable`  | 将指定值用`Optional`封装之后返回，如果该值为null，则返回一个空的`Optional`对象 |
| `orElse`      | 如果有值就将其返回，否则返回一个默认值                       |
| `orElseGet`   | 如果有值则将其返回，否则返回一个由指定的`Supplier`接口生成的值 |
| `orElseThrow` | 如果有值则将其返回，否则抛出一个有指定的`Supplier`接口生成的异常 |

## 组合式异步编程

### `Future`

`Future`的设计初衷是对将来某个时刻会发生的结果进行建模，它建模了一种异步计算，返回一个执行运输结果的引用，当运算结束后，这个引用被返回给调用方。要使用`Future`，只需要将耗时的操作封装在一个`Callalbe`对象中，再将它提交给`ExecutorService`。

```java
ExecutorService executor = Executors.newCachedThreadPool();
Future<Double> future = executor.submit(new Callable<Double> {
    public Double call() {
        return doSomeLongComputation();
    }
});
doSomethingElse();
try {
    Double result = future.get(1, TimeUnit.SECONDS);
} catch(ExecutionException ee) {
    // 计算抛出一个异常
} catch(InterruptedException ie) {
    // 当前线程在等待过程中被中断
} catch(TimeoutException te) {
    // 在Future对象完成之前超过已过期
}
```

### `CompletableFuture`

`complete`方法可以结束`CompletableFuture`对象的运行，并设置变量的值。

`CompletableFuture`提供的工厂方法`supplyAsync`创建`CompletableFuture`对象。

```java
public Future<Double> getPriceAsync(String product) {
    return CompletableFuture.supplyAsync(() -> calculaterPrice(product));
}
```

`supplyAsync`方法接受一个生成者（Supplier）作为参数，返回一个`CompletableFuture`对象，该对象完成异步执行后会读取调用生产者方法的返回值。生产者方法会交由`ForkJoinPool`池中的某个执行线程（`Executor`）运行。

## 时间和日期

java8提供了新的时间和日期库。

`LocalDate`只提供了简单的日期，不包含当天的时间信息，也不附带任何与时区相关的信息。

```java
LocalDate date = localDate.of(2014, 3, 18);
int year = date.getYear();
Month month = daet.getMonth();
int day = date.getDayOfMonth();
DayOfWeek dow = date.getDayOfWeek();
int len = date.lengthOfMonth();
boolean leap = date.isLeapYear();

LocalDate today = LocalDate.now();

// 使用TemporalField读取LocalDate的值
int year = date.get(ChronoField.YEAR);
int month = date.get(ChronoField.MONTH_OF_YEAR);
int day = date.get(ChronoFiled.DAY_OF_MONTH);
```

`LocalTime`类表示一天中的时间，比如`13:45:20`。可以使用`of`重载的两个工厂方法创建`LocalTime`的实例。

```java
LocalTime time = LocalTime.of(13,45.20);
int hour = time.getHour();
int minute = time.getMinute();
int second = time.getSecond();

LocalDate date = LocalDate.parse("2014-03-18");
LocalTime time = LocalTime.parse("13:45:20");
```

可以向`parse`方法传递一个`DateTimeFormatter`，该类的实例定义了如何格式化一个日期或时间对象。

`LocalDateTime`是`LocalDate`和`LocalTime`的合体。它同时表示了日期和时间，但不带有时区信息。

```java
LocalDateTime dt1 = LocalDateTime.of(2014, Month.MARCH, 18, 13, 45, 20);
LocalDateTime dt2 = LocalDateTime.of(date, time);
LocalDateTime dt3 = date.atTime(13, 45, 20);
LocalDateTime dt4 = date.atTime(time);
LocalDateTime dt5 = time.atDate(date);

LocalDate date1 = dt1.toLocalDate();
LocalTime time2 = dt1.toLocalTime();
```

`Instant`是以Unix元年时间（传统的设定为UTC时区1970-1-1:00:00:00）开始所经历的秒数建模。

```java
Instant.ofEpochSecond(3);
Instant.ofEpochSecond(3, 0);
Instant.ofEpochSecond(2, 1_000_000_000);
Instant.ofEpochSecond(4, -1_000_000_000);
```

可以通过`Duration`和`Period`使用`Instant`。

`Temporal`接口定义了如何读取和操纵为时间建模的对象的值。

`Duration`主要以秒和纳秒衡量时间的长短。

```java
Duration d1 = Duration.between(time1, time2);
Duration d2 = Duration.between(dateTime1, dateTime2);
Duration d3 = Duration.between(instant1, instant2);
```

`Period`以年、月或日的方式对时间单位建模。

```java
Period tenDays = Period.between(LocalDate.of(2014, 3, 8),
                               LocalDate.of(2014, 3, 18));
```

创建`Duration`和`Period`对象。

```java
Duration threeMiniutes = Duration.ofMinutes(3);
Duration threeMinutes = Duration.of(3, ChronoUnit.MINUTES);

Period tenDays = Period.ofDays(10);
Period threeWeeks = PeriodofWeeks(3);
Period twoYearsSixMonthsOneDay = Period(2, 6, 1);
```

`DateTimeFormatter`类用于解析日期-时间对象。创建日期格式最简单的方法是通过它的静态工厂方法以及常量。

```java
LocalDate date = LocalDate.of(2014, 3, 18);
String s1 = date.format(DateTimeFormatter.BASIC_ISO_DATE); // 20140318
String s2 = date.format(DateTimeFormatter.ISO_LOCAL_DATE); // 2014-03-18

LocalDate date1 = LocalDate.parse("20140318", 
                                 DateTimeFormatter.BASIC_ISO_DATE);
LocalDate date2 = LocalDate.parse("2014-03-18",
                                 DateTimeFormatter.ISO_LOCAL_DATE);
```

创建`DateTimeFormatter`

```java
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd/MM/yyyy");
LocalDate date1 = LocalDate.of(2014, 3, 18);
String formattedDate = date1.format(formatter);
LocalDate date2 = LocalDate.parse(formattedDate, formatter);

DateTimeFormatter italianFormatter = 
    DateTimeFormatter.ofPattern("d. MMMM yyyy", Locale.ITALIAN);
LocalDate date3 = LocalDate.of(2014, 3, 18);
String formattedDate2 = date3.format(italianFormatter);
LocalDate date4 = LocalDate.parse(formattedDate2, italianFormatter);
```

