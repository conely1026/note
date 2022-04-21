1. #### C风格强制转换

   ```c++
   int a=1;
   char b = (char)a;
   ```

    这种转换适用于面向过程的没有类的概念的c语言的转换，然而这样的转换符也能不分青红皂白的应用于类和类的指针，没有安全检查。

2. #### const_cast

   用法：const_cast<type_id> (expression)

   用于修改类型的const或volatile属性，一般用于强制消除对象的常量性，c中不提供消除这const的机制

3. #### static_cast

   用法：static_cast<type_id> (expression)

   **在编译期间完成类型转换**.

   该转换和c风格的转换很类似，没有运行时类型检查，所以无法保证转换的安全性。主要有以下几种用法：

   **a. 将原有的自动类型转换** , 如 : short转为int, int转为double, 非const转为const类型

   ```c++
   short sh;
   int i = static_cast<int>(sh);
   const int ci = static_cast<const int>(i);
   ```

   **b. void 指针和具体类型指针之间的转换 **

   ```c++
   void *vp;
   int *ip = static_cast<int*>(vp);
   ```

   **c. 有转换构造函数或者类型转换函数的类与其它类型之间的转换(转换的安全性需要开发人员来保证)**

   如 : A是B的基类

   ```c++
   B *b;
   A *a = static_cast<A *>(b);	// 这种建议使用dynamic_cast来转换
   ```

   **d.不能用于无关类型之间的转换 , 如 : int* 转为double* 等**

   ```c++
   int *pi;
   double *di = static_cast<double *>(pi); // error
   ```

4. #### dynamic_cast

   　	用法：dynamic_cast<type*>(expression)

   　　他只用于对象和引用，主要用于执行安全的向下转型，他可以将指向子类的父类指针转换为子类指针，但是要求父类有虚函数，如果转换为指针类型失败则返回NULL，如果是引用类型转换失败则跑出bad_cast的异常

5. #### reinpreter_cast

   　　用法：reinpreter_cast<type_id> (expression)

   　　type_id可以是指针，引用，算术类型，函数指针或者成员指针，这个操作符可以在非相关的类型之间转换，操作只是简单的从一个指针到别的指针的值的二进制拷贝，在类型之间指向的内容不作任何类型的检查和转换。

   `reinterpret_cast`这种转换**仅仅是对二进制位的重新解释(修改), 不会借助已有的转换规则对数据进行调整**, 非常简单粗暴, 风险很高, 一般我们不推荐使用.
   
   > **但是既然c++规定了这中转换， 那么什么时候用合适？在IBM C++指南中明确说了**
   >
   > - 从指针类型到一个足够大的整数类型
   > - 从整数类型或者枚举类型到指针类型
   > - 从一个指向函数的指针到另一个不同类型的指向函数的指针
   > - 从一个指向对象的指针到另一个不同类型的指向对象的指针
   > - 从一个指向类函数成员的指针到另一个指向不同类型的函数成员的指针
   > - 从一个指向类数据成员的指针到另一个指向不同类型的数据成员的指针
   >
   > **总结来说：reinterpret_cast用在任意指针（或引用）类型之间的转换；以及指针与足够大的整数类型之间的转换；从整数类型（包括枚举类型）到指针类型，无视大小**。
   
   就像下面这样`static_cast`无法做的但`reinterpret_cast`就可以完成， 但是赋值等操作却会运行时报错， 这就是`reinterpret_cast`不安全之处， 它能让代码通过编译， 操作时却会报错， 一般建议`reinterpret_cast`只有将转换后的类型值转换回到其原始类型来使用， 做一个中间临时转存。
   
   ```c++
   int *pi = NULL;
   double *di = reinterpret_cast<double *>(pi);
   ```
   
   

note：关于static_cast 和 dynamic_cast的区别：

a. static在转换时不进行安全性检查，完全需要开发者自己考虑, dynamic 在转换的时候会进行安全性检查，如果是指针类型的转换失败返回NULL，如果是引用类型的转换失败，则跑出bad_cast 异常。

b. static主要是用于值类型之间的转换，而dynamic只能用于对象的指针和引用的cast，dynamic是向下的转换，而且要求父类有虚函数，否则会编译出错。