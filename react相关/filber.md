### 背景：react v15 存在的问题

大量的同步计算阻塞了浏览器的 ui 渲染。js 计算，布局计算，页面绘制都是占用主线程的。调用 setstate 更新页面 ui 时，react 会遍历所有节点计算差异，元素多占用主线时间长就会出现掉帧。  
dom diff 也会有同样的问题：

1. 树结点过多导致递归调用战越来越深。
2. 不能中断执行，页面等待递归完成才能重新渲染

### 解决

把一个任务拆分成若干小块，一块是一个 filber。  
渲染一个 react app 是在调用一个函数，这个函数中又在调用若干个函数，形成一个调用栈。旧的 react 会调用到栈空为止。filber 实现了自己的组建栈，是一个链表。可以灵活的暂停，继续，丢弃任务。  
filber 实现方式是使用浏览器的 requestidlecallback（）  
官方解释：window.requestIdleCallback()会在浏览器空闲时期依次调用函数，这就可以让开发者在主事件循环中执行后台和低优先级的任务，而且不会对像动画和输入响应等用户交互这些延迟触发但关键的事件产生影响。函数一般会按先进先调用的顺序执行，除非函数在浏览器调用它之前就到了它的超时时间。

### 拆分

filber 按照 virtual dom 结构拆分，只是结点所带的信息不一样。

### Fiber 的工作循环

1. 找到根结点优先级最高的 workInProgress tree ，取其待处理的结点
2. 检查当前结点是否需要更新，不需要的话，直接 4
3. 标记一下，更新自己（组建更新 props context 等，dom 记下 dom change），进行 reconcileChildrn 并返回 workInprogress.child
4. 不存在 child 说明是叶子结点，向上收集依赖
5. 把 child 或者是 sibling 当作 nextUnitwork 进入库下一个工作循环，如果回到 workInProgress tree 的跟结点，工作循环结束
6. 进入 commit 阶段

### fiber 工作阶段

1. diff render 和 reconciliation 主要构建 workInprogress tree，其实是 diff 过程
2. complete diffProperties 标记 tag，收集 effect
3. commit 提交阶段，应用更新

### workInProgress 双缓冲池技术

fiberRoot 下的所有节点，都会在算法过程中尝试创建自己的镜像。通过这种方式可以把树的总体数量限制在 2，最大限度避免内存使用量因算法过程不断增长
