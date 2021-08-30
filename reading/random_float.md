# 随机浮点数

c++ 11 

```c++
mt19937 rng {random_device{}()} ;

uniform_real_distribution<double> uni {0 , 1} ;
uniform_int_distribution<int> uni  ;
uni(rng) ;


```



