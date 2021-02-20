# js事件
## Dom事件流
1. 捕获阶段
2. 目标阶段
3. 冒泡阶段  

从 windoe->document->html->body->目标对象
### 应用
事件委托：把并列自元素的事件绑定到同一个父元素上，通过事件冒泡触发

## 事件处理程序
### HTML事件处理程序
事件直接绑定在`html`标签的`onclick`属性上  
缺点：代码耦合，不易于维护
### DOM0级事件处理程序
```
    <input type="button" value="Click Me" id="btn">
    <script>
        var btn=document.getElementById("btn");
        btn.onclick=function(){
            console.log(this.id); // 输出 btn
        }
    </script>
```
把一个函数复制给一个事件处理程序的属性，会在冒泡的阶段被处理，要删除事件只要赋值为null  
缺点：只能绑定一个函数明，多次绑定只有最后一个生效
### DOM2级事件处理程序
使用`addEventListener()`绑定   
使用`removeEventListener()`来移除   
最后一个参数：处理时间，true 捕获，false（默认） 冒泡