const类型定义：指明变量或对象的值是不能被更新,引入目的是为了取代预编译指令 

**************常量必须被初始化*************************

cons的作用
  （1）可以定义const常量     例如：

```c++
    const int Max=100;
 	int Array[Max];   
```


  （2）便于进行类型检查      例如：
       

```c++
	void f(const int i) { .........}
```

​    编译器就会知道i是一个常量，不允许修改；
  （3）可以保护被修饰的东西，防止意外的修改，增强程序的健壮性。
​    还是上面的例子，如果在函数体内修改了i，编译器就会报错；
​    例如： 
​       

```c++
	void f(const int i) { i=10;//error! }
```

  (5) 为函数重载提供了一个参考。
     

```c++
class A
     {
      ......
      void f(int i)    {......} file://一个函数
      void f(int i) const {......} file://上一个函数的重载
      ......
     };
```

   (6) 可以节省空间，避免不必要的内存分配。
     例如：
       

```c++
\#	   define PI 3.14159     file://常量宏
       const doulbe Pi=3.14159; file://此时并未将Pi放入ROM中
       ......
       double i=Pi;        file://此时为Pi分配内存，以后不再分配！
       double I=PI;        file://编译期间进行宏替换，分配内存
       double j=Pi;        file://没有内存分配
       double J=PI;        file://再进行宏替换，又一次分配内存！
```

​     const定义常量从汇编的角度来看，只是给出了对应的内存地址，而不是象#define一样给出的是立即数，所以，const定义的常量在程序运行过程中只有一份拷贝，而#define定义的常量在内存中有若干个拷贝。
   （7） 提高了效率。
​      编译器通常不为普通const常量分配存储空间，而是将它们保存在符号表中，这使得它成为一个编译期间的常量，没有了存储与读内存的操作，使得它的效率也很高。

使用const
  （1）修饰一般常量,常数组，常对象
　　 修饰符const可以用在类型说明符前，也可以用在类型说明符后。   例如：  

```c++
	int const x=2;　　
或　 const int x=2;

	int const a[5]={1, 2, 3, 4, 5};  
或  const int a[5]={1, 2, 3, 4, 5};

​   class A;　   
    const A a; 
或  A const a;
```


  （2）修饰指针
  

```c++
	const int *A;  或 int const *A; //const修饰指向的对象，A可变，A指向的对象不可变

    int *const A;       //const修饰指针A，   A不可变，A指向的对象可变 

    const int *const A;   //指针A和A指向的对象都不可变
```

  （3）修饰引用
 　   const double & v;   该引用所引用的对象不能被更新
　（4）修饰函数的返回值：
    const修饰符也可以修饰函数的返回值，是返回值不可被改变，格式如下：
      const int Fun1(); 
      const MyClass Fun2();
  （5）修饰类的成员函数：
    const修饰符也可以修饰类的成员函数，格式如下：
     

```c++
 class ClassName 
   {
       public:
      　  　int Fun() const;
      　    .....
       }；
```

​    这样，在调用函数Fun时就不能修改类里面的数据 
  （6）在另一连接文件中引用const常量
​     extern const int i;   //正确的引用
​     extern const int j=10; //错误！常量不可以被再次赋值
  


*******************放在类内部的常量有什么限制？

  

```c++
  class A
    {
     private:
      const int c3 = 7;        // err
      static int c4 = 7;        // err
      static const float c5 = 7; // err
     ......
 };
```

 初始化类内部的常量
    1 初始化列表：

```c++
  class A
     {
     public:
        A(int i=0):test(i) {}
     private:
        const int i;
     }；
```

​     2 外部初始化，例如：

```c++
  class A
     {
     public:
        A() {}
     private:
        static const int i; 
     }；
     const int A::i=3;  
```

