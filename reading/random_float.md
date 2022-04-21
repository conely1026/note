# 随机浮点数

c++ 11 

```c++
random_device re ; 
mt19937 rng {re()} ;

uniform_real_distribution<double> uni {0 , 1} ;  //[0,1]
uniform_int_distribution<int> uni  ;
uni(rng) ;


```



