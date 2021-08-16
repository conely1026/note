# 随机浮点数

c++ 11 

` 

mt19937 rng {random_device{}()} ;

  uniform_real_distribution<double> uni {0 , 1} ;

uni(rng) ;

`

