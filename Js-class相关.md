### 提升
函数声明会提升，但是类声明不会提升，不声明就使用会报错。

### 声明方式方式（两种）
```
    class test = {
        constructor(){

        }
    }
```
```
    //类表达式
    let test = class {
        constructor(){

        }
    }
```
### 构造函数
1. `constructor([...arguments]){...} //可不传参数`
2. ```
    super([arguments]); 
    // 调用 父对象/父类 的构造函数

    super.functionOnParent([arguments]); 
    // 调用 父对象/父类 上的方法
    //在继承类中，使用this之前必须使用super（）
    ```
    ###装饰器
    装饰器是一种在编译时执行的代码，可以为class或对象方法增加新的属性或者其他操作

    基本的使用
  ```
function test (){
    target.canEdit = true
}



