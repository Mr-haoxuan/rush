# setSate相关

```
  state初始 0 

    setState({this.state+1})
    setState({this.state+1})
    setState({this.state+1})
    console.log(this.state) 

```
上面这种情况被称作setState批处理

## 什么时候会批处理
批处理（看起来是异步）：合成事件（react中得onClick，onChange等）
同步更新：原生时间，setTimeout，setInterval，promise等异步操作

## 批处理过程
1. setState 放入事务队列中
 获取当前组件的instance（实例）
 将要更新的state放入一个数组里
 将要更新的component instance 给 enqueueUpdta (入队列)
2. 判断是否处于批处理/更新状态
3. 是:把当前组件push进dirtyComponents  
不是：执行batchupdate()
2.
3. 判断是否处于 batch update （isbatchingUpdate）  
4. 为true 将当前的组件放在dirtyComponents数组中  
为false 遍历dirtyComponents 处理update state事务

```javascript

import { Input, InputNumber } from 'antd';

const Test = () => {
  const obj = {};

  Object.defineProperty(obj, 'age', {
    set: (e) => {
      if (xxx) {
        return;
      }
      obj['age'] = e;
      React.forceUpdate();
    }
  })

  const handleInputChange = (key, e) => {
    const value = e.target.value || e;

    obj[key] = value;
  }

  return (
    <>
      <Input value={obj.name} onChange={handleInputChange.bind(null, 'name')} />
      <InputNumber value={obj.age} onChange={handleInputChange.bind(null, 'age')} />
    </>
  )
}

```