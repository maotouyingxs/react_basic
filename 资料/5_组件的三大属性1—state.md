### 1.理解
- state是组件对象最重要的属性, 值是对象(可以包含多个key-value的组合)
- 组件被称为"状态机", 通过更新组件的state来更新对应的页面显示(重新渲染组件)

### 2.注意
组件中render方法中的this为组件实例对象
组件自定义的方法中this为undefined，如何解决？
- 强制绑定this: 通过函数对象的bind()
- 箭头函数

- 状态数据，不能直接修改或更新

``` javascript
//    1.创建类式组件
        class Weather
            extends React.Component {
                // 构造器调用几次？ -- 1次
            constructor(props) {
                super(props)
                // 初始化状态
                this.state = { isHot: false, wind: '微风' }
                // 解决changeWeather 中 this 指向问题
                this.changeWeather = this.changeWeather.bind(this)
            }
            // render 调用几次？ -- 1+n次 1是初始化的那次，n是状态更新的次数
            render() {
                const { isHot, wind } = this.state
                return (
                    <h1 onClick={this.changeWeather}>今天天气很{isHot ? '炎热' : '凉爽'},{wind}</h1>
                );
            }
            // changeWeather 调用几次？ -- 点几次调用几次
            changeWeather() {
                // changeWeather 放在哪里了？ -- Weather 的原型对象上，供实例使用
                // 由于changeWeather 是作为onClick 的回调，所以不是通过实例调用的，是直接调用的，
                // 类中的方法默认开启了局部的严格模式，所以 changeWeather 中的 this 为 undefind
                // console.log('标题被点击了');
                const isHot = this.state.isHot;
                // 严重注意：状态（state） 不可直接更改
                // this.state.isHot = !isHot;
                // 严重注意：状态必须通过 setState 进行更新，且更新是一种合并，不是替换。
                this.setState({ isHot: !isHot })
            }
        }
        ReactDOM.render(
            <Weather />,
            document.getElementById('test')
        );
        // const title = document.getElementById('title')
        // title.addEventListener('click',() => {
        //     console.log('标题被点击了');
        // })
        // const title = document.getElementById('title')
        // title.onclick = () => {
        //     console.log('标题被点击了');
        // }

```
