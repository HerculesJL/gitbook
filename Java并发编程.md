## 第一章：Lambda表达式
### 1.2 无类型参数
#### （1）单参数
**lambda**表达式的基本结构：
>f->{ } 

代码举例：
```
List<Fruit> fruits = Arrays.asList(......);

fruits.forEach(f -> {
  System.out.println(f.getName());
});
```
>无类型指的是不给f指代类型，Lambda表达式自动从上下文获取类型为fruit。

![](https://style.youkeda.com/img/ham/course/j5/j5-1-2-1.svg)

注意点：Lambda表达式要配合上下文、跟其他方法配合使用。

#### （2）多参数
代码举例：实现sort方法
```
List<Student> students = new ArrayList<Student>();
students.add(new Student(111, "bbbb", "london"));
students.add(new Student(131, "aaaa", "nyc"));
students.add(new Student(121, "cccc", "jaipur"));

// 实现升序排序
Collections.sort(students, (student1, student2) -> {
  // 第一个参数的学号 vs 第二个参数的学号
  return student1.getRollNo() - student2.getRollNo();
});

students.forEach(s -> System.out.println(s));

```

### 1.3有类型参数
```
fruits.forEach((Fruit f) -> {
  System.out.println(f.getName());
});
```
>与无参数的区别就是fruit的存在。加上类型fruit只是为了代码更容易读

### 1.5双冒号操作符
使用双冒号操作符会将当前遍历的对象直接作为参数传给要用的函数
#### （1）语法含义
![](https://style.youkeda.com/img/ham/course/j5/j5-1-5-1.svg)


#### （2）双冒号操作符的两种不同用法
首先介绍静态方法和动态方法的区别：
1. **静态方法**属于类所有，类实例化之前即可使用。
1. 非静态方法可以访问类中的任何成员，静态方法只能访问类中的静态成员。
1. 类中的非静态变量必须在实例化之后才能分配内存；
1. static内部只能出现static变量和其他static方法!而且static方法中还不能使用this等关键字，因为它是属于整个类。
1. 静态方法效率上要比实例化高，静态方法的缺点是不自动进行销毁，而实例化的则可以做销毁。
1. 主要区别：**静态方法**在创建对象前就可以使用了，非静态方法必须通过new出来的对象调用。
##### 用法一：静态方法调用
使用`LambdaTest::print`代替`f->{LambdaTest.print(f)}`
##### 用法二：非静态方法调用
再非静态方法中，print()不再标识为static，所以需要实例对象来调用
`fruits.forEach(new LambdaTest()::print);`
##### 用法三：多参数
```
Collections.sort(students, (student1, student2) -> {
  // 第一个参数的学号 vs 第二个参数的学号
  return student1.getRollNo() - student2.getRollNo();
});
```

在定义了compute(Student s1,Student s2)后，可以更改为：
`Collections.sort(students, SortTest::compute);`

>系统会自动获取上下文的参数，并按上下文定义的顺序传递给指定的方法。

>通过习题发现：在**类**重写`public String toString(){}`方法后可以通过`System.out.println(对象名)` 直接按照toString内的格式打印内容。

