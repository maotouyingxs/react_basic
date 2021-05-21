# react学习
## 1. [react介绍](/资料/2_介绍.md)
   - 中文官网:https://react.docschina.org/
## 2. [类的基本知识](/资料/3_类的基本知识.md)
## 3. [组件](/资料/4_组件.md)- 组件的定义
 - **注意**：
    - 组件名必须首字母大写
    - 虚拟DOM元素只能有一个根元素
    - 虚拟DOM元素必须有结束标签
 - **渲染类式组件标签的基本流程**
    - React内部会创建组件实例对象
    - 调用render()得到虚拟DOM, 并解析为真实DOM
    - 插入到指定的页面元素内部 
## 4. [组件的三大属性1—state](/资料/5_组件的三大属性1—state.md)
- **理解**
  - state是组件对象最重要的属性, 值是对象(可以包含多个key-value的组合)
  - 组件被称为"状态机", 通过更新组件的state来更新对应的页面显示(重新渲染组件)

- **注意**   组件中render方法中的this为组件实例对象
组件自定义的方法中this为undefined，如何解决？
   - 强制绑定this: 通过函数对象的bind()
   - 箭头函数
   - 状态数据，不能直接修改或更新
## 5. [组件三大核心属性2—props](/资料/6_组件三大核心属性2—props.md)
### 1.理解
- 每个组件对象都会有props(properties的简写)属性
- 组件标签的所有属性都保存在props中

### 作用
- 通过标签属性从组件外向组件内传递变化的数据
- 注意: 组件内部不要修改props数据
- 
## 6. [组件三大核心属性3—refs与事件绑定](/资料/7_组件三大核心属性3—refs与事件绑定.md)
   1. **理解**
      - 组件内的标签可以定义ref属性来标识自己
   2. **事件绑定**
      - 通过 onXxx 属性指定事件处理函数(注意大小写)
          - React 使用的是自定义(合成)事件, 而不是使用的原生DOM事件
          - React 中的事件是通过事件委托方式处理的(委托给组件最外层的元素)
      - 通过 event.target 得到发生事件的 DOM 元素对象 -- 不要过度使用 ref

   3. **高阶函数与函数的柯里化**
      - 高阶函数：如果一个函数符合下面两个规范中的任何一个，那么函数就是高阶函数
           1. 若 A 函数，接收的参数是一个函数，那么 A 就可以称之为高阶函数
           2. 若 A 函数，调用的返回值依然是一个函数，那么 A 就可以称之为高阶函数
                  常见的高阶函数有：Promise、setTimeout、arr.map()等待
      - 函数的柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码方式。
---
## 7. [组件的生命周期](/资料/8_组件的生命周期.md)
   1. **生命周期的三个阶段（旧）**
      1. 初始化阶段: 由ReactDOM.render()触发---初次渲染
          1. constructor()
          2. componentWillMount()
          3. render()
          4. componentDidMount() ===> 常用
           --- 一般做一些初始化的是，例如开启定时器，发生网络请求，订阅消息
      2. **更新阶段: 由组件内部this.setSate()或父组件重新render触发**
          1. shouldComponentUpdate()
          2. componentWillUpdate()
          3.render()
          4. componentDidUpdate()
      3. **卸载组件: 由ReactDOM.unmountComponentAtNode()触发**
          1. componentWillUnmount() --- 
            一般做些收尾的事，例如：关闭定时器、取消订阅
---
### 生命周期的三个阶段（新）
   1. **初始化阶段: 由ReactDOM.render()触发---初次渲染**
       1. constructor()
       2. getDerivedStateFromProps 
       3. render()
       4. componentDidMount()
   2. **更新阶段: 由组件内部this.setSate()或父组件重新render触发**
       1. getDerivedStateFromProps
       2. shouldComponentUpdate()
       3. render()
       4. getSnapshotBeforeUpdate
       5. componentDidUpdate()
   3. **卸载组件: 由ReactDOM.unmountComponentAtNode()触发**
       1. componentWillUnmount()
---
### 重要的勾子
1. render：初始化渲染或更新渲染调用
2. componentDidMount：开启监听, 发送ajax请求
3. componentWillUnmount：做一些收尾工作, 如: 清理定时器
### 即将废弃的勾子
1. componentWillMount
2. componentWillReceiveProps
3. componentWillUpdate

---

# 面试题
## 1. react/vue 中的 key 有什么作用？ （key 的内部原理是什么？）[答案](/资料/1_经典面试题.md)