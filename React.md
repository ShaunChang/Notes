# 0 react开发
    步骤
    1. 设计好UI，划分组件，通过功能划分，比如不要用header body fotter 用currentcity。。。功能划分 这部分干嘛就用啥名
    2. react创建静态脚本：
        下载： npm i create-react-app -g
        创建脚手架项目：create-react-app xxx
        进入文件夹：cd xxx
        把你划分好的那些组件包和相关文件都划分好并创建相关组件
        确定各个组件的样式
        启动： npm start
    3. 确定UI satate的最小表示
    4. 确定state放置位置
    5. 添加反向数据流

    随时维护rmr原则
    readeable：
        命名见名知意
        不要用if else：  1 使用if else会导致代码变得冗长且难以维护。
                        2 如果判断条件特别多，会使程序变得复杂，难读难理解；
                        3 编写if else会带来一定的计算开销，会影响程序的执行效率；
                        4 if else会降低程序的可读性，不利于代码的复用；
                        5 if else一次只能处理两个分支 不如人家switch这些
    reuseable： propType
                propType是如何有益于代码的reuseable的？propType提供一种方式来检测传入组件的props参数是否正确，并且可以在传入参数不正确时抛出警告。它能够有效地帮助开发人员在使用和重用组件时及时发现错误，避免出现不必要的bug，从而提升代码的可重用性。
# 1 为什么学react
    1. 原生js操作dom效率低 老重排重绘  
    2. 原生js没有组件化编码（就是把html js css都按功能拆分）
# 2 react特点
    1. 虚拟dom  减少与真实dom交互 一句话：只改必须改的部分
    2. 既然我们可以用JS对象表示DOM结构，那么当数据状态发生变化而需要改变DOM结构时，我们先通过JS对象表示的虚拟DOM计算出实际DOM需要做的最小变动，然后再操作实际DOM，从而避免了粗放式的DOM操作带来的性能问题。
    3. diff算法    比较虚拟dom的东西，重复的继续用
    4. 组件化编码（就是把html js css都按功能拆分）
    5. 声明式编码（说一句话办很多事）编码
    6. 用react native使用react语法进行移动端开发

# 3 各包功能以及如何引入依赖 
    babel.min.js: 把jsx转化为js  浏览器只认识js
    react.development.js： react核心库
    react-dom.development: 扩展dom库
    prop.types: 用于对组件标签属性进行限制
    核心库必须在其他两个之前引入

# 4 如何使用react写虚拟dom
### 什么是虚拟dom
    -本质就是个object
    -虚拟dom你在开发者工具中能看到没什么东西，很轻，原生里面多的一p
    -虚拟dom最终会被转化为真实dom呈现
### 如何创建虚拟dom
    第一种方法使用jsx：
    type="text/babel"
    const VDOM = <h1>Hello,React</h1>，注意
    此处等号后的内容一定不要写引号，因为你定义的是一个虚拟dom，这是
    jsx语法，html和js可以混合使用

    第二种方法js：
    type="text/javascript"
    const VDOM = React.creatElement(标签名，标签属性，标签内容)
    eg：React.createElement('h1',{id:'title'},'Hello React')
    为什么要用jsx写法：
    此时有一个需求，在h1里面写span 用js无法写 你把hello。。换成《span》它只会按字符串显示。你只能继续用react.creatElemetn替换helloxxx那块。如果多了写起来就很麻烦。而jsx可以直接按html写法写。其实jsx最后还是翻译成了react。createelemt那种，只是你没写而已。

# 5 Render
### 作用
    ReactDom.render(虚拟dom，容器)，把xxdom渲染到某个容器
    eg：ReactDOM.render(VDOM,doucument.getElementByxx("xx"))
### 注意：
    -render同时写两个不会是两个渲染 是后面的覆盖前面的
    -一共有两个时期：初始化组件，state变化

# 6 jsx
### 本质
    就是js+html
### 语法
    定义虚拟dom不要写引号
    html中印入js表达式（不包括控制语句等，用map替代循环）用{}
    样式的类名指定要用xxxName
    内联样式: style={{key:value,xxx}}
    只能有一个根标签
    所有标签必须闭合
    标签首字母：
       小写字母开头则去找html同名元素，找不到 就报错、
       大写字母开头则去找对应组件，若没有定义 则报错

# 7 模块和组件
### 概念
    模块只是拆js，目的是复用js。组件是拆所有（js。css。html），组件包含所有局部页面要用的，复用整个代码
    模块化：js都以模块编写
### 什么是模块化代码
    module 是一组代码，用来提供其他模块所使用的功能，并能使用其他模块的功能。 export 模块提供代码，import 模块使用其他代码。模块之所以有用，是因为它们允许我们重用代码，它们提供了许多可用的稳定、一致的接口，并且不会污染全局命名空间
    为什么要用模块化编程
    一段可以实现完整功能的代码你如果不是傻逼你肯定总想复用对吧，你就想把这块代码打包放哪儿，到时候遇到相同的功能你直接调用就好了。es6出来之前没有class。一般做法是把这段代码打包放在一个xxx。js文件里，用的时候直接用<script src="xxx.js"></script>引入进来就ok。但是这样写有两个问题：
    污染全局命名空间：你在脚本中创建的所有变量（sum、 difference 等）现在都存在于 window 对象中。如果你打算在另一个文件中使用另一个名为 sum 的变量，会很难知道在脚本的其它位置到底用的是哪一个值变量，因为它们用的都是相同的 window.sum 变量。唯一可以使变量私有的方法是将其放在函数的作用域中。甚至在 DOM 中名为 x 的 id 可能会和 var x 存在冲突。
    依赖管理：必须从上到下依次加载脚本来确保可以使用正确的变量。将脚本分别保存存为不同文件会产生分离的错觉，但本质上与放在页面中的单个 <script> 中相同
### 模块化编程老的解决方案
    之后又出现了一些模块解决方案：CommonJS 是一种在 Node.js 实现的同步方法，异步模块定义（AMD）是一种异步方法，还有支持前面两种样式的通用方法——通用模块定义（UMD）这些解决方案的出现使我们可以更轻松地以包的形式共享和重用代码，也就是可以分发和共享的模块，例如 npm。但是由于存在许多解决方案，并且都不是 JavaScript 原生的，所以需要依靠 Babel、Webpack 或 Browserify之类的工具才能在浏览器中使用。
### 模块化编程新的解决方案
    JavaScript 中的模块使用import 和 export 关键字：
    import：用于读取从另一个模块导出的代码。
    export：用于向其他模块提供代码。
    模块与常规脚本不一样的地方：
    模块不会向全局（window）作用域添加任何内容。
    模块始终处于严格模式。
    在同一文件中把同一模块加载两次不会出问题，因为模块仅执行一次
    模块需要服务器环境。
    接下来把前面的的 functions.js 文件更新为模块并导出函数。在每个函数的前面添加 export 。
    export function sum(x, y) {
      return x + y
    }
    
    export function difference(x, y) {
      return x - y
    }
    
    export function product(x, y) {
      return x * y
    }
    
    export function quotient(x, y) {
      return x / y
    }
    使用imoort：
    import { sum, difference, product, quotient } from './functions.js'
    
    const x = 10
    const y = 5
    
    document.getElementById('x').textContent = x
    document.getElementById('y').textContent = y
### 组件化：
    应用以多组件方式实现
### 组件
    组件中的render中的this是实例对象
    组件中自定义方法的this味undefined
    组件就是个自动机 不同状态显示不同结果
### 组件勾造器
    只干两件事
    -为事件处理函数绑定实例
    -初始化state
    能不写构造器吗
    可以。绑定this可以用箭头函数搞定。初始化state可以用state={xxx}搞定
    构造器必须接受props吗
    取决于你是否想在构造器中使用this.props。要就必须传 ，不然this.prosp会报错：undefined

# 8 函数式组件
### 定义
    function demo(){
    return <h2>dddd</h2>
    }
### 注意
    不要在if condition和while中使用函数组件
### hooks优点
    使用hooks就能在函数式组件中使用state了
    更加简洁
    使用hooks可以把state分开 在class 组件中它们都在一起 是一坨大的对象
### 常用hooks有哪些
    usestate（）：1. 返回两个值，第一个state，第二个setstate(默认值)，通过解构得到state和setstate：const[xxx,setxxx] = useState(默认值)
    useEffect(): 就是didmount和didupdate的合并，
                 后面的[]叫依赖项，空的话表示只运行一次，也就是只在组件加载的时候运行一次，不会随着组件的更新而更新。想更新的时候也用的话就在【】中放上要变的state
                 可以写多个
### 使用
    注意组件用标签包住，且首字母必须大写，标签必须闭合
    ReactDOM.render(<Demo/>,document.getElementById("xxx"))
### 原理
    react解析组件标签，找到了组件，发现是函数组件，调用该函数，将虚拟dom转化为真实dom然后渲染
### this
    函数式组件没有this
    原本应该是window，但是显示出来时undifiended，原因是因为babel翻译完后会开启严格模式，严格模式下不允许this指向window
### props
    注意接收props的时候带{}：
    const About = ({xx,xx,xx})=>{}

# 9 类式组件
### js class类
    class Person{
    Constructor(xx,xx){
    this.xx=xx;(这里的this指实力对象)
    this.xx=xx;
    }
    speak(){
    console.log(‘我叫${this.name}')
    }}
### js继承
    class Student extends Person{
    constructor(name,age,grade){
    super(name,age)//传进去的是你想复用父类的
    this.grade=grade
    }}
    注意：如果a继承b a有构造器 那么a必须在构造器中使用super（）
### 类式组件
    必须继承React.compont
    必须重写render（）方法且有返回值（返回html）
    eg: class  MyComponent extends React.componont {
    render(){
    return <div........>
    }
    }
    ReactDOM.render(<Mycompont/>,document.getElementnbyId("xxx"))
### 类的构造器可以干的事
    给方法绑定this  
    初始化state
### 原理
    react解析组件标签，找到了组件
    发现是类组件，new出来实例，通过该实例调用render方法
    将render返回的虚拟dom转为真实dom。然后呈现出来

# 10 简单组件和复杂组件
    有状态的就是复杂组件

# 11 状态
### 生活：
    状态影响着行为，你状态不好，影响你考试成绩低。
### react状态
    指的是数据
### 状态的存在意义
    状态驱动着结果，这个数据，驱动着这个展示结果

# 12 组件实例的三大核心属性state pros
### state
    state中存对象 用key value表示
    初始化state
        通过构造器
        class xx extends React.Component{
        constructor(props){
        super(props)
        this.state = {isHot:true,wind:'xxx'}
        }
        render(){
        return xxx
        }
        }

    改变state
        1 改变state的函数写在类中
        -改变实例中的state可以直接在类中定义对应的改变状态的方法，因为可以直接用this，用this就能点出来state
        2 将函数中的this绑定为实例对象的this，将函数赋值给实例对象
        -注意此时方法中默认为局部严格模式， 此时如果调用这个方法的人是window，this就会自动为undifeied，那你就无法通过this点出state从而改变它了
        解决方法是在构造器中绑定实例对象this。构造器最后一行那句话意思是：实例对象（因为构造器中的this就是实例对象）点出来chageweather，就去实例对象找changeweather，发现没有，就去原型对象找，找到了。因为本来这个方法就绑定在原型对象上。是原型对象的changewather方法，然后给这个方法用bind。bind做两件事：1 改你函数里的this ，传进去的是this，由于在构造器，就是实例对象的this 2 生成一个新的函数。最后，把这个生成的新函数赋值给你的实例对象。这样，你的实例对象就多了一个this指向实例对象的方法。你去consolo。log你就发现此时自身也有了这个方法了
        3 react中不能直接改state 要用react原型对象中的setstate（）方法修改
    
        改变state简写方式
        0 初始化state   
        直接在class内：state={xxx,xxx}.这个相当于a=1 。类中直接写赋值语句的意思是给这个class的实例对象直接追加一个属性a 值为1
        1 改变state的函数写在类中   不变
        2 将函数中的this绑定为实例对象的this，将函数赋值给实例对象（赋值语句➕箭头函数）
        为什么要用赋值语句加箭头函数呢》？我使用普通函数创建方法，弄个箭头函数，然后用this不行吗。虽然不在实例身上，最后不也可以顺上去找到原型上那个函数吗？
        回答：不好意思 不能这么写
        -同理0，使用xxx=xxx的形式先把这个函数赋值给实例变量
        -用箭头函数绑定this

    react中不能直接改state 要用react原型对象中的setstate（）方法修改   不变
    
### props
    意义：
    给组件定义属性，定义好后就会重新render一个新的组件

    批量导入props
        const p = {name:'xxx' age:xxx}
        ReactDOM.render(<Person {...p}>  document.get...)    等价于愚蠢写法：ReactDOM.render(<Person name={p,name}  age={p.age}>  document.get...) 
        props限制：默认值 是否必须要 数据类型（你不规定这个你比如后面要显示的时候有数子处理需求，由于你没限制人家有可能传个字符串过来，原本比如加的方法就成字符串拼接了）
        -在15.xxx版本之前都是xxx.propTypes = {name.React.ProTypes.string.isrequired.....}这样规定
        -在15之后取消了  理由是这样弄会让react很庞大 有时候有的人也不需要 就把这个弄了个单独的包  你要用的时候再导入prop.types.js:
        xxx.propTypes = {name.ProTypes.string.isrequired.....}
        -限制类型或必要性
        xxx.propTypes = {name.ProTypes.string.isrequired.....，speak:PropTypes.func(限制传入的必须是一个函数)}
        -限制默认值
        xxx.defaultProps = {xxx：‘xxx’}
    怎么用props
        普通方式：
        1 把props值结构出来：
        render(){
        const {xx,xx} = this.props
        return (
        <h1>{xx}</h1>
        )
        }
        2 props限制放在class外面
        
        简写方式:所有东西都在类里面 很清晰
        1 
        2 把proptype属性放在类里面 其实上面的那句话的意思就是给类的prptype属性赋值  注意是类上的 不是实例对象的 所以前面加个static即可
        static propTypes = {name.ProTypes.string.isrequired.....，speak:PropTypes.func(限制传入的必须是一个函数)}
### refs
    概念
    每个组件标签都可以规定refs，用来标识自己。作用和id一样。

    注意
    this.refs得到的是真实dom‘不是虚拟dom
    
    如何使用
    1 标签中直接定义：<h1 ref="xxx">     以后可能废弃 不推荐
    用：const {你给ref取的名字} = this.refs
    2 回调函数 <h1 ref={c => this.你给ref取的名字=c}/> 这里的c其实是ref对应的这个标签实例
    用：const {你给ref取的名字} = this
    3 createAPI（官方建议）
    注意：createRef创建出来的ref容器专人专用 就是一个容器存一个标签对象
    ref容器名1 = React.createRef()
    ref容器名 2= React.createRef()
    <h1 ref={this.ref容器名1}/> ref后的东西是一个createREF（）方法创建出来的ref容器，这句话意思是吧本ref放到这个容器里
    <h1 ref={this.ref容器名2}/>
    
    函数式ref调用问题
    首次render只执行一次。以后每次更新的时候，即state改变的时候会执行两次。以为state变会导致会重新调用render，这时候为了确保渲染没问题，会先清空一下，再赋值当前元素
    
    不要过度使用ref：事件发生的dom和你要操作的dom是一个dom的话用event.target拿到这个事件发生的dom

# 13 React事件绑定
    react推荐在html内内联绑定onclick
    用onClick（大写C）
    绑定的不能是一个函数名，即不要写Onclick=xxx() 要写Onclick=xxx，要加{}
    不能写onClick={demo()}这样意思是把dome函数的返回值绑定在onclick上。demo函数没有返回值，就是undefined，你点了没效果，而且同时这个函数会被执行。

# 14 类中的this
    类中的方法供实例调用，所以一个方法中直接调另一个方法不行 要写成this.xxx()
    自己定义的类中的方法中的this只有在类的实例对象调用这个方法时this才是实例对象
    类中的方法自动开启了严格模式。this不能指向window，执行为undifined。下图中用实例还是用引用调用都是指向了堆中那个方法。由于这个方法是一个普同方法。但是它不是用a=1这样的方式写，所以在类的原型上。p1.study()的时候其实在对象身上没有找到，就顺着原型链去找，找到了，由于是普通方法，this动态绑定给调用者。一看。是原型调用，打印出p1这个对象。第二次是引用调用，其实和在类外面就是我们在script标签中直接定义一个方法一样，一看this。windows调用，但是！由于在类中，自动开启严格模式，所以最后输出undefined

# 35 箭头函数和普通函数中的this
    小结：
    通过引用来调用箭头函数方法，方法中的this依然指向创建的实例对象。
    原因：箭头函数中的this，只和定义改箭头函数的位置有关系，即，箭头函数中的this始终是该箭头函数所在作用域中的this。而箭头函数所在的作用域中的this指向foo实例对象。
    问：如果全局使用箭头呢？
    
    
    通过引用调用普通函数方法，方法中的this会指向undefined。
    原因：因为普通函数中的this是动态绑定的，始终指向函数的执行环境，上面的例子中在全局环境中调用getAge方法，但是this确是undefined而不是window。原因在于class声明和class表达式中会默认使用严格模式。
    作者：卷舒
    链接：https://juejin.cn/post/6923086072855396366


# 15 ...展开运算符
    有4个用法：如果直接...p:展开一个数组（不能展开对象）  链接两个数组  
                         如果包花括号{...p}  ：浅拷贝一个对象，复制对象的同时修改/增加其属性
    注意：在react的props里使用{...p} 这里的花括号表示你现在在rect要写js语句了  不是上面第二个花括号的功能。rect里这样写就是展开一个对象！它牛逼，把不能的事能了。但是注意，这种牛逼只限于标签属性的传递上使用

# 16 阻止表单提交
    给dom的onsubmit绑定回调函数  函数里面通过event.preventDefault()阻止事件触发、

# 17 非受控组件
    所有输入类dom（inoput textbox.....）的值你现用现取

# 18 受控组件
    所有输入类dom随着输入把值维护到状态里 你用的时候直接从状态中取即可

# 19 受控和非受控组件区别
    推荐受控 。因为人家一个ref都没有 ，上面告诉你了少用ref

# 20 高阶函数
    什么是高阶函数？符合下面任意一个就算
    函数入参是一个函数
    函数返回值是一个函数
    eg：上面受控组件要一个dom维护一个state有重复代码 写成一个 但是onchange后必须接的是一个函数，这时你又要传参 就用高阶函数存参数 处理后返回目标回调函数。常见的高阶有：promise settimeout map。。。 注意这里取入参的值需要加【】

# 21 函数的柯里化
    观念
    通过函数调用继续返回函数的方式。实现多次接收参数后统一处理的函数编码方式。
    eg 
    为什么要用？直接把所有值传进去不行吗
    如图所示的错误例子：必须使用柯里化，因为event你没法传

# 22 卸载组件
    ReactDom.unmountComponentAtNode(document.getElementById('xxxx'))

# 23 组件生命周期：挂载--卸载
    对应几个特定的组件生命时间点，调用特定的不同的生命周期回调函数 左边是挂载 右边是更新：
    旧版本
    1 有父组件 且父组件第二次刷新时
    2正常的state更新流程
    3强制更新：不想更新state只想更新dom
    
    componentWillMount：组件挂载前
    componentdidmount：组件挂载完毕后
    compinentwillunmount: 组件将要卸载的时候
    
    shoulderComponentUpdate: 更新阀门  返回boolean  为真时才会有后续
    componentWillupdate：组件将要更新
    componentDidUpdate:  组件更新完毕
    componentWillReceiveProps:  父组件render的时候调用  有个坑：第一次传的不算
    新版本
    绿色框内那个忽略


# 24 组件中的css
    style={{opacity:this.state.xxx}}

# 25 原型对象方法和实例对象方法
    原型对象:无赋值动作
    xxx(){}：创建了一个普通方法放在了原型对象上，供实例使用
    实例对象:有赋值动作
    xxx = ()=>{}

# 26 虚拟dom中的key

    如何通过key比较虚拟dom
    
    为什么不能用索引值作为key：1 逆序添加删除引发无必要dom渲染   2 导致错误输入类dom更新。所以只要没有逆序添加和删除等破坏顺序的动作且只用于展示 用index也没事
    1 因为每个新数据插入进来，而此时都是头部插入的 会打乱所有的顺序 这样一来所有的dom都会不一样 本来能复用的不能复用了  如上图。
        解决：用数据id作为key
                     往后面添加
    
    2 如果dom内嵌套输入类dom  数据会发生错乱。因为diff会一层一层比较下去，发现input各个属性都一样（因为虚拟dom没有value值！只有放在页面上的真实dom才有value），把我的给你用，但是没想到此时input里面有输入值


# 27 react脚手架：
    为什么使用脚手架
    上面的编码你会发现在f12提示不要在生产环境使用babel。。。并且每个页面都有进入好几个js库这种动作 有时候代码多的话半天反应不过来 会有白屏问题。影响效率。所以使用脚手架会简单快速编码
    
    什么是脚手架
    xxx脚手架就是帮助程序员快速创建一个基于xx库的模版项目。里面包含：
    包含所需配置（语法检查，jsx编译，自动打开浏览器）
    下载好了相关依赖 可以直接运行一个简单效果
    
    使用脚手架好处
    模块化 组件化  工程化（写完代码，编译，压缩，兼容性等都一条龙给你弄好。像汽车生产线一样）
    
    如何使用脚手架
    下载： npm i create-react-app -g
    创建脚手架项目：create-react-app xxx
    进入文件夹：cd xxx
    启动： npm start

# 28 脚手架文件目录介绍：标红的是主要的
    node_modules：
    用的依赖包
    public：存静态文件。 html css  图片等
    -index.html: vue和react都是spa（single page application）开发。整个应用就一个index.html:
    
    -robots.txt: 爬虫规定文件。规定哪些你能爬 哪些不能
    -mainfest.json: 手机app加壳配置  加上壳后 html网页app变成安卓或者ios

    src
    -index.js: 入口，其实就是ReactDOM.render。注意：<React.stricctMode>放在这儿的目的是为了检查你写的一些子组件是否合理。比如你写了个ref=“”这种方式的ref 它会给你检查出来告诉你 这个东西弃用了 由于react中经常发生这样的事 你有时候不知道 所以给你检查检查
    简单写法：
    import React from 'react';
    import ReactDOM from 'react-dom';
    import App from './App';
    
    
    ReactDOM.render(<App/>, document.getElementById('root'))
    原生写法：
    
    -App.js：所有的组件放这儿，这是一个整体
    -index.css: 一些通用的css
    -ReportWebVitals：用于记录性能的
    -SetUpTests。js：用于做组件测试的

# 29 组件文件夹命名规范
    第一种命名
    所有组件在component中，各自创建各自的包 包中包含css 外部js 组件js文件
    组件js文件和外部js文件如何区分：
    方法一：大写组件名
    方法二：组件文件结尾为jsx
    第二种命名
    所有组件在component中，各自创建各自的包。包中组件的css和组件都用index mingm
    这样写的好处是在impot时可以省略组件名：
    import xxx from './component/组件包名'

# 30 css模块化
    为什么要把css也模块化
    因为你不这样做到的话，一股脑把组件文件引入进去，注意此时组件自己已经引入了css。所有东西最后都要放到一个div中，这些css就会混在一起。如果有重名的标签选择器，此时就会出现css样式冲突。
    怎么弄
    1 把css文件命名为xxx.module.css
    2 引入时可以用变量接了：import xxx from './index.module.css'(原来是：import './index.css')
    3 命名组件标签的时候前面加css模块名(注意这里是花括号)：<h2 className={xxx.css中标签选择器的名字}></h2> （原来是<h2 className=“css中标签选择器的名字”></h2> ）

# 31 react插件
    安装插件
    如何使用插件
    -rcc 新建一个类组件
    -rfc 新建一个函数组件

# 32 组件化编码流程
    -拆分组件
    -实现静态组件
    -实现动态组件：动态显示数据。绑定监听事件。

# 33 父子组件如何相互传值
    父传子：props
    子传父：父中定义一个函数 参数是子要传的  里面可以改变state啥的   然后把这个函数用props传给子

# 34 数据的唯一id用什么：uuid/nanoid
    安装
    yarn add uuid/nanoid
    npm i uuid/nanoid、
    引入
    import {nanoid} from 'nanoid'
    使用
    nanoid()

# 35 import react, {xxx} from 'xxx'中的{xxx}是什么意思
    -不是对ract的解构赋值，是因为xxx是分别暴露的东西：用这种解构只是说明在from xxx的文件里有多种暴露方式
    
    import后的名字
    如果你采用的是默认暴露的方式 import后的名字你可以直接改 

# 36 兄弟组件如何通信
    方法一：共用state
    放在它们共同的父组件中（状态提升）

    方法二：消息订阅与发布
    安装
    nom PubSubJS
    引入
    import PubSub from 'pubsub-js'
    订阅消息 ：在componentDidMount中(token是用来取消订阅的)
    componentDidMount(){
    this.token = PubSub.subscribe('xxx', (msg,data)=>{
    this.setState(data)
    })
    }
    注意：var token = PubSub.subscribe('你想订阅的消息名',回调函数)
                 回调函数：funciton(msg:数据名，data：数据) {xxxxx}
    取消订阅：在componentWillUnmount
    componentWillUnmount(){
    PubSub.unsubscribe(token)
    }
    发布消息
    PubSub.publish('消息名'，'消息内容')


# 37 父子组件如何通信
    父传子
    props
    子传父
    子通过父亲给它的函数把值传回给父

# 38 ajax
    axios：需要安装
    安装
    npm add axios
    引入
    import axios from 'axios'
    使用
    axios.get('http://xxxx').then(
    response => {xxx}
    error => {xxx}
    )
    fetch：不用安装内置就有  缺点：关注分离 
    fetch(`xxxx`).then(
    response => {xxxx},
    error => {xxxx}
    )
    成功或者失败的返回是非promise值，then返回的proimise状态就是成功的 值为这个非promise值
    返回是promise值，then返回的promise就是这个promise 包括状态和值都一样


# 39 配置代理
    为什么使用代理：因为同源策略的限制 跨域请求不能回来
    ajax引擎发送请求的时候请求能过去，但是回来时被引擎过滤，因为服务器和client不在一个端口。所以使用了代理，代理的好处是它也和clent（脚手架）在一个端口，然后它没有ajax引擎的拦截，所以response回的来。其实最后还是要通过ajax引擎，只不过引擎一看，也是跟自己一样的端口返回来的值，就不拦截了

# 40 配置代理
    代理配置方式1: 3000port没有的找5000port要。 缺点：只能配置一个server
    1 package.json配置
    最后加一行：作用是把请求转发给这个目标port
    "proxy":"xxxx你想转发的目标port"
    2 重启脚手架！！
    3 将ajax请求改成和自己一个port的请求 
    
    代理配置方式2: 配置多个代理 好处：能配置多个代理  而且灵活：加api之类的前缀就走那个代理 不加就不走
    1 src中建立新文件：setupProxy.js(文件名不能变)
    2 添加文件内容
    const proxy = require('http-proxy-middleware')
    module.exports = function(app){app.use(
    proxy('/api1',{//遇见/api1前缀的请求，就会触发该代理配置
    //请求
    target:'http://localhost:5000', //转发给谁
    changeOrigin: true, //控制服务器收到的相应头中的host（为true在服务器那边拿到host值的时候就会显示上面自己配置的地址 迷惑行为 为false就是真真正正的自己的地址）字段的值
    pathRewrite:{'^/api1':''} //在真正把请求给5000服务器的时候 把/api1重写为“”
    })，
    proxy('/api2',{
    target:'http://localhost:5001',
    changeOrigin: true,
    pathRewrite:{'^/api1':''}
    })
    )}
    2 重启脚手架！！
    3 将ajax请求中加入api1 
    
    所有请求都会被转发吗？
    不是 脚手架中没有的资源才会被转发去寻找

# 41 spa应用
    首先说一下什么是多页面应用：去一个页面刷新一次，每个页面中重复的部分你也总得重复写 很笨重。
    spa：渲染不同内容时不是通过切换页面来实现，切换页面不发请求，而是通过js更新dom实现。

# 42 要给item加kehy的报错
    当你自己手写几个一摸一样的dom的时候 react会自动给你给每个打上key。 但是如果是动态生成的，比如你用map，react这时无法加key，因为这是页面到浏览器之后的事 react只能在之前做

# 43 什么是路由
    一个路由就是一个映射关系
    key是你输入的path：locahost/home'
    value: 是对应的component

# 44 怎么用路由
### 安装react-router-dom  
    npm add react-router-dom@5

### 原理
    就是改变了地址栏地址，其实就是改了history ，默认为put模式，点一个link，就把一个link压在history栈中。就把现在显示的url改成了另一个，但不发请求。路由器会检查url变化，每个地址栏地址对应一个组件。
    其实底层还是把link转为了a标签 加了listen让页面不跳转。即路由路径是特殊a标签 它不跳转

### 路由匹配顺序
    是从最开始注册的路由到最后注册的路由匹配的，最先匹配的路由一定是app里的

### 步骤
    npm add react-router-dom@5
    import  {Route,navlink...} from 'react-route-dom' 注意react-route-dom都是分别暴露 所以用花括号引入
    路由链接link和route路由要放在一个路由管理器中，可以把整个app包起来
    路由管理器：<BrowserRouter></BrowserRouter>
    把a标签换为link：<Link className="" to="/about">About</Link>
    route：<Route path="/about" component={About}/>
    
### 路由组件和普通组件的区别
    路由组件：<Route path="/about" component={About}/>应该放在page包下
    路由组件在被render的时候被自动往props传了些东西：history location match。普通组件传了什么pros就收到什么

### navlink：
    作用：点谁就给谁加一个类名 
    类名规定：activeClassName="xxxx"
    通过this。props。children获取标签体内容
    点的时候老闪怎么办：可能是你用了的bootstrap的权重太高导致的  方法是在每个新增的css后加！important

### 封装navlink
    navlink哪些classname一大堆 每次都要复制 很冗余 你把它封装成一个普通mynavlink组件，classname固定好，前面
    调用mynavlink的时候只需要传props就行：
    export defalut class MyNavLink extend Component{
    render(){
    return(
        <NavLink className="xx" className="xxx" {...this.props}>
        // 这里的。。。this。props就把前面传的所有的props都取出来放上了  其中包括children，就是前面mynavlinkl的标签题体内容
    )
    }
}

### switch：提高效率
    干嘛的：正常route会一个一个匹配path 匹配上了还会往下匹配 直到弄完为止 因为path可以重复 试想你现在有1000000个path="/about" 一个弄完还有一个 消耗资源
    用switch把所有route包起来，就会匹配一个后停止
    
    注意以最上一个为主

### 解决刷新后丢失样式问题
    多级路径下刷新可能会丢失样式，因为在页面引入css中你可能写的是./css.....这里的./就会把多级路径前面那个路径也带进去
    解决方法一：
    引入css用%PUBLIC_URL% 绝对路径 代表pulic文件夹

    解决方法二：
    用hashrouter：localhost:3000/#/atguigu/home 好处是它把#号后面的都认为是前端资源
    
    解决方法三：
    把.删除

### yarn和npm不要混用
    容易造成包的丢失。你的包被两个包管理器管，比如npm启动项目，项目下的包也都是npm管，突然，其中还有个yarn安装的包 npm找不到那个包，项目报错

### 模糊匹配和严格匹配
    默认就是模糊匹配：link：  to="/hone/xxf/xf"  <Route path="/home">    第一个对上了就行 后面的随便 注意 必须是第一个 
    精准匹配：<Route exact path="xxx" component={xxx}>
    
    注意：不要随便开启严格模式 会引发很严重的问题！！！ 原则上只要不影响页面展示你就别用严格模式。例如你给父组件开启严格模式，就意味着它下面的所有子路由全废了。比如现在 
    父路由path="/home" 子路由：path="home/news" 你点击子路由，url变为home/news，从最开始注册的路由开始匹配，父组件直接挂载失败 子组件跟着吃屎（父组件render压根就没完成）

### redirect： 默认选一个 兜底的
    放在所有路由最下面 :<Redict to="/about"/>

### 嵌套路由的写法
    一定把父组件的路由也带上，这样父组件相关的路由才不会丢。因为url地址变，跟render一样，整体会从头匹配一遍。
    不要给父开启严格模式

### 向路由组件传递参数
    react中的路由组件为什么不用props传参而要用params？
    props是父组件传递给子组件的参数，它们是静态的，不能改变；而params是用来传递动态参数的，他们是通过URL来传递参数，可以改变。
    
    params参数法（用的最多）
    1 用模版第字符串传值：<Link to="{`/home/pages/${dxxx.id}/${dxxx.title}`}">
    2 必须在路由接收，不然由于模糊匹配把后面的会省略： <Route path="/home/message/:id/:title" component={dxx}>
    3 组件里怎么取pramas呢？在match里以对象形式存好了，所以：
    this.props.match.params
    4 刷新不丢数据

    search参数法
    1 用模版第字符串传值：<Link to="{`/home/pages/？id=${dxxx.id}&title=${dxxx.title}">
    2 无需声明接收
    3 组件里怎么取search呢？在location里用urlencode形式（key=value&key=value）存好了，所以
    import qs from 'querystring'    //qs.prase可以把urlencode转化为obj
    const {search} = this.props.location
    const res = qs.parse(search)
    4 刷新不丢数据

    state参数法（跟组件的state没关系）
    1 用对象形式传值：<Link to={{pathname:'/home/state',state:{id:xxx,title:xxx}}}>
    2 无需声明接收
    3 组件里怎么取pramas呢？在match里以对象形式存好了，所以：
    const {} = this.props.location.state || {}   //这个一定要写 不然清理缓存前端会报错：找不到state 因为state都是存在history里的 默认为undefined
    this.props.location.state
    4 优点：刷新不丢数据 
           参数不在url体现 安全
    
    params和serach传值语句都可以改成state那种对象的形式 就是把后面的state换成params就行

### 开启replace模式
    好处：
    不留访问痕迹 不能回退
    
    <link replace={true} to=xxx>
    或者<ling replace to=xxx>


### 编程式路由导航
    干嘛的 
    不借助用户点击 用程序跳转link。比如需求：1 当用户点击首页图标后三秒，转到about页面，这里的about没人点 
                                      2 一个页面下有两个按钮，一个push点击用push跳转 一个replace点击用replace跳转 
    
    怎么用
    this.props.history 里面有replace forward goback go(参数为n 表示前进几步) push这些方法，安倍path放里面就行了了 param 和search传参和之前的一样
    this.props.history.replace(`/about/${id}/${xx}`)
    state：
    this.props.history.replace(`/about/xxx`,{id,title})

### 普通组件想用路由组件api怎么办
    暴露组件的时候加个withrouter：export default withRouter(xxx)

### BrowserRouter和HashRouter的区别
    1 底层原理不一样：b用的是history，能留下访问记录。ie9以下不兼容。 
                    h用的是url哈希值
    2 url b中有#
    3 刷新后b不会丢失state参数 h会
    4 h能解决样式丢失的问题
    

# 46 ReactRouter 6
### 对比上面的5有什么变化
    1. 用routes替换了switch 之前switch可以省略
    2. 用element替换了component，并且用花括号包住component：element={<About/>}
    3. 用navigate替换了redirect，<Route path="/" element={<Navigate to="xxx"/>}/> navigage就是渲染到组件视图就切换 说白了只要匹配上了不用用户点就能自动切换页面
    4. route中加入了casesensitive 大小写敏感
    5. navlink自定义点击更换类名，className后面跟箭头函数
    6. useRoutes：路由表：就是<Routes><Route path="/about" element={<About/>}></Routes>的简化形式，表内写核心mapper关系即可，useRoutes帮你生成前面那一坨
    const element = userRoutes([{path:'/about',element:<About/>}])  然后把element放在想要显示的地方即可
    7. 把所有路由放在routes文件夹下的index.js文件中，用的地方引入即可
    8. 嵌套路由：在children中定义：userRoutes([{path:'/about',element:<About/>,children:[{path:'xx',element:<About/>}]}])注意chinldren不要斜杠路径
                link中to="news"不能加斜杠，或者用./news，斜杠的意思是不管你在哪，带着/就是根了
                用outlet占坑
    9. link中的end属性，加了end意思是如果我的子集匹配了 我就失去active高亮，或者失去classname指定的样式
    10. 使用useparams接收路由参数L：const {xx,xx,xx} = useParams()
    11. usenaviget：编程式路由 const navigate = useNavigate()  
    navigate(
    '/about' ,//去哪儿，注意如果是子路由不用写/
    {//一些配置
        replace：true,
        //编程式路由导航传参只支持state
        state:{
         id:xxx,
         name:xxx
        }
    }
    )
    前进：navigate(+1)
    后退：navigate(-1)
    12. const s = useRoutes() s为boolean 表示当前组件是否被路由管理器包裹
    13. useNavigationType()  返回用户是如何来到当前页到 pop（直接通过刷新来的）put replace
    14. useoutlet 返回当前组件下属的子组件，前提是子组件要挂载上
    15. useoutletresolvedpath 给定一个url 解析出其中的path serch hashsta
### 如何使用
    1. 安装：npm i react-router-dom、



# 47 component下文件后缀:jsx index.js
    首先明白效果一样
    jsx后缀文件：一个组件文件中有可能还有其他的js文件 全都是js结尾你不知道哪个是组件js 用jsx就可以一眼识别
    index.js: 这样写的好处是在其他组件想引用你这个组件时组件名就可以省略: import xx from 'component/Welcome/Welcome(省略)'


# 48 边框双层怎么办L：两个边框在一起
    margin-bottom: -8px;

# 49 如何决定组件是否需要拆分
    1 看这个东西你是否需要复用
    2 这部分未来会变，抽出来，方便维护

# 50 context
    是啥
    一种组件间通信方式。特别实用于祖组件和后代组件间的通信，父子间可以直接用props传递，所以可以不用这个 
    
    怎么用
    1 创建context容器对象
    const XxxContext = React.createContext() 注意首字母大写，并放在所有组件都能访问的地方 
    问：react中的createContext()的圆括号()中的参数是什么
    答：CreateContext()的参数是一个JavaScript对象，它用于定义上下文的初始值。详细解释并举例如下：
    createContext() 函数接受一个可选的初始值，它可以用于在上下文树中的消费者组件中提供一些默认值，比如：

    const MyContext = React.createContext({
    name: 'Default Name',
    age: 0
    });

    在使用时，如果没有提供 Provider，消费者组件将会接收上面的默认值
    作为上下文的初始值
    2 用<XxxContext.provider></>包裹子组件、
    3 通过value把想传的值放进去：
        放字符串：<XxxContext.provider value={变量名}></>包裹子组件
        放对象：<XxxContext.provider value={{name:'xx',age: 18}}></>包裹子组件
    4 使用的人举手：
        类组件：static contextType = MyContent    this.context
        类组件/函数组件：<XxxContext.consumer>
                        {
                            value => (
                               return(`xxx${value.name}`)
                            )
                        }
                      </>
        或者在一个类中把这个context暴露出来，在需要用的组件中接收这个context：import XxxContent
                const {comments, deleteCommont} = useContext(XxxContent)

# 51 reducer
    干嘛的
    管理复杂状态的
    问：为什么不用state 答：state只能进行简单状态管理：setState（）  需求：state是一个数组。 要求：把第三个删除   setstte怎么做？？？用reducer你就可以在里面弄一些函数去处理这个了

    react中的usereducer是干嘛的
    是 React 中的一个 Hook，它接受一个 reducer 函数和一个初始化的状态值，然后返回当前状态和一个 dispatch 函数，
    它可以接受一个 action 对象来更改当前状态值，并返回新的状态值。`useReducer` 主要用于管理复杂的状态，而不是简单的 state。 
    
    dispatch是干嘛的？ dispatch 是一个函数，用于改变状态值，它接受一个 action 对象作为参数，然后根据 action 对象的属性和值来更新状态值。

    什么是action对象，举个例子？ 
    Action 对象是一个 JavaScript 对象，它用于描述一个动作，并包含一些用于更改状态的属性和值。例如：
    const action = {
      type: "ADD_TODO",
      payload: {
        text: "Learn React"
      }
    };

    怎么用
    1 写一个reducer：const myReducer = (initialDate: any, action: any) => {
                        switch(action.type) {
                            case 'add'
                                return initialData+action.number
                            case 'decrease'
                                return initialData-1
                            default:
                                return initialData
                        }
                    }
    2 创建reducer： const [num, dispatch] = useReducer(myReducer, 0)
    3 用： <div>   {num}   <button onClick={()=>{ dispatch({type:add, number: 22})  }}></div>

# 52 webstorage
    cookie session复习：
    cookie生命周期是多久
    cookie的生命周期取决于它的失效时间，如果没有设定失效时间，那么cookie就会在当前会话结束时过期，也就是浏览器关闭的时候结束。session生命周期通常为一个会话，也就是说，当用户关闭浏览器或关掉网页时，session会话就会被终止，session里的数据也就被清空。这么说session和cookie的生命周期一样？这仅仅是相似之处，session的生命周期是从用户登录到登出，而cookie在用户关闭浏览器或关掉网页后就会被销毁。举例来说，如果用户访问某个网站，那么在这个网站上cookie的存在会持续到用户关闭浏览器，而session则会在用户登出后销毁。session是服务器端开辟的内存还是浏览器开辟的内存？

	session是由服务器端开辟的内存，它会将session信息存储在服务器上，每个客户端都会有一个唯一的session ID来标识，浏览器会将这个session ID通过cookie的方式发送给服务器，服务器根据这个session ID来找到对应的session信息。

    内存多大
    cookie: 4kb: 一次会话
    sessionStorage: 5mb 登录登出
    localstorage：5mb 永久，直到用户手动清理缓存。 数据不能被爬虫抓

    怎么用localstorage
    存
    localstorage.setItem("Notes",JSON.stringify(notes))
    取
    const data = JSON.parse(locastorage.getItem("Notes"))
    注意神坑：：：useeffect有顺序！！！！！！！！！！！！！！！！！！！！！！所以把取的那个effect放在set的前面 不然存空值


# 53 classnmae/bind
    导入
    import classNames from 'calssnames/bind';
    import styles from './Item.module.css'

    const cx = classNames.bind(styles)
    <div className={cx('item',{isHightLight,})}></div>这段代码是什么意思 详细解释并举例说明

    这段代码是使用`classnames`库来实现动态类名的语法糖，用来替代多个条件判断来添加类名的写法。其中的`isHightLight`变量的值决定了最终渲染的类名是否包含`isHighLight`，如果`isHightLight`是`true`，最终渲染的类名会包含`isHighLight`，反之不包含。
    
    举个例子：
    
    let isHightLight = true
    
    <div className={cx('item',{isHightLight,})}></div>
    
    // 最终渲染的类名为：item isHighLight
    ```css中如何识别这个类名
    
    CSS中可以通过`.item.isHighLight` 来识别这个类名，这样就可以对指定的元素进行样式设置。.item.isHighLight是什么意思？
    
    `.item.isHighLight`是一种CSS选择器，表示只有拥有同时包含`item`和`isHighLight`两个类名的元素才会被选择出来，只要满足这两个类名，就可以对元素进行相应的样式设置。


# 54 react哲学 以后写react就按这个来
    1 划分组件层级
    2 静态版本
    3 状态的最小展示： React的状态最小展示原则（State Minimization Principle）是指在React组件中，只保存必要的状态，而不是所有的状态。状态最小化可以帮助组件变得更易于理解和维护，可以减少潜在的错误和复杂性。
    4 状态的正确位置：React的状态应该保存在组件本身的state属性中，而不是在全局对象或者其他地方，这样可以使得状态保持组件私有，让组件不仅更容易管理，而且更容易维护和测试。
    5 回调函数： react哲学中的回调函数需要注意什么
        1. 尽量保持回调函数的简洁，减少代码量，提高可读性。
        2. 尽量使用迭代器（Iterators）或者箭头函数，以提高代码的可读性和可维护性。
        3. 不要在回调函数中使用过多的参数，以避免参数不一致的情况。
        4. 如果回调函数包含复杂的业务逻辑，则将其封装到函数中，以便重用。

