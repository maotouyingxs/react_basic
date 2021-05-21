### 1.理解
- 每个组件对象都会有props(properties的简写)属性
- 组件标签的所有属性都保存在props中

### 作用
- 通过标签属性从组件外向组件内传递变化的数据
- 注意: 组件内部不要修改props数据
- 
``` javascript
    <!-- 引入prop-types，用于对组件标签属性进行限制 -->
    <script type="text/javascript" src="../js/prop-types.js"></script>
    
        // 创建组件
        class Person extends React.Component {
            // 构造器是否接收props，是否传递个super，取决于：是否希望咋构造器中通过 this 访问 props 一般不写
            constructor(props) {
                console.log(props);
                super(props);
            }
            // 对标签属性进行类型，必要性的限制
            static propTypes = {
                name: PropTypes.string.isRequired,
                sex: PropTypes.string,
                age: PropTypes.number
            }
            // 指定默认标签属性值
            static defaultProps = {
                sex: '男',
                age: 18
            }
            render() {
                // console.log(this)
                const { name, age, sex } = this.props;
                return (
                    <ul>
                        <li>姓名：{name}</li>
                        <li>性别：{sex}</li>
                        <li>年龄：{age + 1}</li>
                    </ul>

                )
            }

        }


        // 渲染组件到页面
        ReactDOM.render(<Person name='jerry' age={17}  speak={speak}/>, document.getElementById('test1'))
        ReactDOM.render(<Person name='Tom' age={18} sex='女' />, document.getElementById('test2'))
        const person = { name: '阿猫', age: 19, sex: '女' }
        ReactDOM.render(<Person {...person} />, document.getElementById('test3'))
```