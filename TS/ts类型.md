Ts继承了es中所有基础类型，并做了一些扩展
es基础类型：boolean,string,number,object,arrey,Function,symbol,undefined,null
Ts新增数据类型：any,void,never,枚举,元组,

###元组
    元组表示一个已知元素数量和和个数的数组，元素的类型不必一样
    ```
        let x:[number,string]
        x=[1,"one"]
        console.log(x)

        x.push(3)
        console.log(x)
        x[4]= "four" 
    ```
    元素越界：使用数组的原生方法添加越界元素不报错，访问索引的方式会报错

###函数类型
    ```
        const test = (x:number,y:number)=>{
            return x+y
        }
        上面这个函数默认知道返回类型，这个叫做类型推断

        也可以定义函数的返回类型：
        const test = (x:number,y:number):number=>{
            return x+y  
        }
    ```
###对象类型
    ```
        let obj:object = {x:1,y:2}
        obj.x = 3 //报错  Property 'x' does not exist on type 'object'.
        let obj:{x:number,y:number} = {x:1,y:2}
        obj.x = 3 //success
    ```
###undefined&null
    undefined 和 null 是所有类型的子类型

###void 
    viod表示一个表达式没有返回值
    ```
        let fun(x: number) => void
        fun = (x) => x * 3 // error

        const fun2 = (x:number):void => x * 3 //error TS2322: Type 'number' is not assignable to type 'void'.
    ```

###never 
    never表示永远没有返回
    ```
    const fun = ()=>{
        let x= 1 
        while(true){
            x+=1
        }
    }
    ```

###枚举:数字枚举、字符串枚举、异构枚举
##数字枚举
```
   enum Zonglian {
    cup,
    pen,
    computer
    }

    Zonglian[0]  // cup
    Zonglian.pen // 1

    // 如果你对索引进行一些干预则会有不同的效果
    enum ZonglianAgain {
        cup = 1,
        pen,
        computer = 5,
        banana,
    }

    ZonglianAgain.pen   // 2

    ZonglianAgain[0]    // undefined
    ZonglianAgain.banana // 6
```
ts是如何实现数字枚举的：反向映射
```
    var Zonglian={};
    (function(Zonglian){
        Zonglian[(Zonglian["cup"]=0)] = 'cup';
        Zonglian[(Zonglian["pen"] = 1)] = 'pen';
    })(Zonglian)
```
##字符串枚举
```
    enum Zonglian{
        one="一"，
        two="二"
    }

    Zonglian.one //一
    Zonglian['一'] //undefined
```
可见，字符串类型的枚举不支持反向映射
##异构枚举
异构枚举即字符串和数字的混合

##枚举的其他特征
```
    Zonglian{
        //常量枚举
        a,
        c=1+2
        //计算型枚举
        b="abc".length(),
    }
```
常量枚举在编译时会移除，当我们只需要对象的值的时候可以使用常量枚举减少代码编译后的体积