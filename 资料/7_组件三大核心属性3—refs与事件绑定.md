### 1.理解
- 组件内的标签可以定义ref属性来标识自己
### 2.事件绑定
- 通过 onXxx 属性指定事件处理函数(注意大小写)
    - React 使用的是自定义(合成)事件, 而不是使用的原生DOM事件
    - React 中的事件是通过事件委托方式处理的(委托给组件最外层的元素)
- 通过 event.target 得到发生事件的 DOM 元素对象 -- 不要过度使用 ref
- 
### 3高阶函数与函数的柯里化
- 高阶函数：如果一个函数符合下面两个规范中的任何一个，那么函数就是高阶函数
     1. 若 A 函数，接收的参数是一个函数，那么 A 就可以称之为高阶函数
     2. 若 A 函数，调用的返回值依然是一个函数，那么 A 就可以称之为高阶函数
            常见的高阶函数有：Promise、setTimeout、arr.map()等待
- 函数的柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码方式。
---
### 1. 字符串形式的ref
```javascript
        // 创建组件
        class Demo extends React.Component {
            // 展示左侧数据
            showData = () => {
                const { input1 } = this.refs;
                alert(input1.value)
            }
            // 展示右侧数据
            showData2 = () => {
                const { input2 } = this.refs
                alert(input2.value)
            }
            render() {
                return (
                    <div>
                        <input ref='input1' type='text' placeholder='点击按钮提示数据' />
                        &nbsp;
                        <button onClick={this.showData}>点我提示左侧数据</button>
                        &nbsp;
                        <input ref='input2' onBlur={this.showData2} type='text' placeholder='失去焦点提示数据' />
                    </div>
                )
            }

        }


        // 渲染组件到页面
        ReactDOM.render(<Demo />, document.getElementById('test'))
```
---
### 2. 回调函数形式的ref
```javascript
        // 创建组件
        class Demo extends React.Component {
            // 展示左侧数据
            showData = () => {
                const { input1 } = this;
                alert(input1.value)
            }
            // 展示右侧数据
            showData2 = () => {
                const { input2 } = this
                alert(input2.value)
            }
            render() {
                return (
                    <div>
                        <input ref={(currentNode) => { this.input1 = currentNode }} type='text' placeholder='点击按钮提示数据' />
                        &nbsp;
                        <button onClick={this.showData}>点我提示左侧数据</button>
                        &nbsp;
                        <input ref={c => this.input2 = c} onBlur={this.showData2} type='text' placeholder='失去焦点提示数据' />
                    </div>
                )
            }

        }


        // 渲染组件到页面
        ReactDOM.render(<Demo />, document.getElementById('test'))
```
---
### 3. createRef
```javascript
        // 创建组件
        class Demo extends React.Component {
            /*
                React.createRef()调用后可以返回一个容器，该容器可以存储被 ref 所标识的节点,该容器是“专人专用”的
            */
            myRef = React.createRef()
            myRef2 = React.createRef()
            // 展示左侧数据
            showData = () => {
                alert(this.myRef.current.value)
            }
            // 展示右侧数据
            showData2 = () => {
                alert(this.myRef2.current.value)
            }
            render() {
                return (
                    <div>
                        <input ref={this.myRef} type='text' placeholder='点击按钮提示数据' />
                        &nbsp;
                        <button onClick={this.showData}>点我提示左侧数据</button>
                        &nbsp;
                        <input ref={this.myRef2} onBlur={this.showData2} type='text' placeholder='失去焦点提示数据' />
                    </div>
                )
            }

        }


        // 渲染组件到页面
        ReactDOM.render(<Demo />, document.getElementById('test'))
```
