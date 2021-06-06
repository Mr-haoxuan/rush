### 基础数据类型
普通类型：NULL,undefined，boolean，number，string，symbol   
复杂类型：obj

类型判断 ：typeof、 instanceof 、construct

### 作用域
1、js本身是函数作用域，内部可以访问外部，外部不能访问内部  
2、新增 let 创造了块级作用域

### var,let,const
1、var会变量提升  
2、let const 要先赋值再使用，不可以重复定义

### this指向
普通函数 ：谁调用指向谁在的上下文    
箭头函数： 指向定义的变量所在的上下文   
改变：   
1、bind 返回一个函数  
2、call（this，arg1，2，3，4，5），apply（this，[arguments]）返回结果

### 数组常用方法
分割:  slice（index，长度）, splice（index，lastIndex）  
转stirng：join

### 字符串常用方法
转数组 slite
分割 slice（index，lastindex）
分割、插入 splice

### 原型链

### new的原理
注意构造函数执行return 对象/新建的对象

### eventLoop

### promise/async awite 

.all全部成功或者有一个reject才执行后面的回调
.allSellted 
.race 谁先有结果就用谁的状态
.any 只要有成功的就resolve
.finally 不管什么最后都执行


### 内存泄漏