
# 软件开发现有问题
开始：开发完毕，初次使用

结束：软件升级和维护，代价非常大，大到不如重新开发。但是重新开发意味着以前的努力白费了。所以出现了一些设计思想和框架 为的是实现软件生命周期的利益最大化。你可以不修改，去添加新的类（开闭原则），实现代码的升级。但是原来的代码中是new的原来的对象，意味着你还得改代码 即存在耦合

 
# 0 什么是微服务
-整个应用必须构建成一系列小服务的的组合  
eg：把原来mvc中的esrvice单独弄成一个模块 这个模块只提供接口  
-原来的单体架构：把所有服务都封装在一个应用中                                     
好处：易于开发和测试 吧war包复制多份放到服务器就好了  
坏处：难于维护 动一个 其它都要重新部署
-微服务：每个功能独立出来 用的时候用哪个调用哪个 动态组合
好处：节省资源 每个独立 好维护  


# 1 sp什么东西
-不用写配置文件的ss框架（springboot用注解）  
-spring 框架有两个主要原则：依赖注入 控制反转  
-特性  
使用 Spring 项目引导⻚面可以在几秒构建一个项目  
Spring容器、日志、自动配置AutoCongfiguration、Starters，方便对外输出各种形式的服务，如 REST API、WebSocket、Web、Streaming、Tasks  
非常简洁的安全策略集成  
支持关系数据库和非关系数据库  
支持运行期内嵌容器，如 Tomcat、Jetty  
强大的开发包，支持热启动  
自动管理依赖  
自带应用监控  
支持各种 IDE，如 IntelliJ IDEA 、NetBeans  
-与tmocat的关系  
它把tomcat直接内嵌了  以前弄完app要把代码部署到tomcat中（其实就是把各种文件放到固定的文件夹下） 现在就是sp直接给你把这些弄好了

# IOC和DI 控制反转和依赖注入
https://blog.csdn.net/L_GRAND_ORDER/article/details/112136702#:~:text=Spring%20IOC%20%28%E6%8E%A7%E5%88%B6%E5%8F%8D%E8%BD%AC%29%E6%80%9D%E6%83%B3%E7%AC%94%E8%AE%B0,IOC%20%E6%8E%A7%E5%88%B6%E5%8F%8D%E8%BD%AC%20%E5%9F%BA%E6%9C%AC%E7%90%86%E5%BF%B5%E5%B0%B1%E6%98%AF%E5%B0%86%E7%A8%8B%E5%BA%8F%E6%8E%A7%E5%88%B6%E6%9D%83%E4%BB%8E%E7%A8%8B%E5%BA%8F%E5%91%98%E6%89%8B%E4%B8%AD%E4%BA%A4%E7%BB%99%E7%94%A8%E6%88%B7%E8%87%AA%E5%AE%9A%E4%B9%89%EF%BC%8C%E4%BB%8E%E8%80%8C%E9%81%BF%E5%85%8D%E4%BA%86%E5%9B%A0%E4%B8%BA%E7%94%A8%E6%88%B7%E4%B8%80%E4%B8%AA%E5%B0%8F%E9%9C%80%E6%B1%82%E7%9A%84%E5%8F%98%E5%8C%96%E4%BD%BF%E5%BE%97%E7%A8%8B%E5%BA%8F%E5%91%98%E9%9C%80%E8%A6%81%E6%94%B9%E5%8A%A8%E5%A4%A7%E9%87%8F%E4%BB%A3%E7%A0%81%E3%80%82%20%E6%A1%88%E4%BE%8B



# 2 javaconfig
-相当于xml 它的替代 是一个java类
-可以创建类 放入到spring中
-用两个注解：
@Configuration 放在文件上面 意思是这个类是config 
@Bean(name = "") 创建方法   返回值是对象 方法上用@bean 意思是把返回值对象注入到容器中 其中的name就是id 必须和类名一样
 -使用注解比xml文件方便
Application ctx = new AnnotationConfigApplicationContext(xxx.class)
XXX xxx = ctx.getbean("xxx")
-自动配置原理


# 3 @ImportResource
-作用：导入其他的配置文件，和当前文件合并为一块儿 作为配置使用
-使用：@importResource(value = "classpath:applicationContext.xml，classpath=“”")

# 4 以下是4种使用配置文件给类中赋值的方式
@PropertyResource： 
-你逼酱 你非要用不是application命名的配置文件 就用这个引入
-与value连用 
-首先要明白spring框架有ioc  所有对象由工厂创建   这里的vo里的类上都有component注解 就是说允许创建对象  这里的PropertyResource就是规定工厂在创建对象的过程中去PropertyResource后面规定的配置文件中找相应的值  componentsacn就是一顿扫描 把需要创对象的都扫出来
@value：
不逼酱  你用application 但是是properties   就得手动用value一个个弄：eg：@Value("${person.name}") 从配置文件取值    @Value("#{11*2}") spring表达式   @Value("true") 字面量
@configurationpropeties   
-不逼酱 用官方指定的配置文件 弄好后可以用yaml牛逼的地方 就是这个方法：属性绑定 不需要你一个个value赋值
-作用是将配置文件中配置的每一个属性的值映射到这个组件中 将对应的属性绑定 只有这个组件是容器中的组件才能用这个功能（@component：把普通pojo实例化到spring容器中，相当于配置文件中的<bean id="" class=""/>）； 
- @ConfigurationProperties最适用于所有具有相同前缀的分层属
-用于自定义配置项比较多的情况
-pretix前缀就是点前面的 比如 school.name
-如果想给自己的配置信息加上鼠标悬浮出现的描述信息的话要加一个依赖：spring-boot-configuration-processor
运行的时候写环境变量
-环境变量会覆盖yaml/proopetites配置

 
# 5 application propety和yaml
-property：server。port=8080
-yaml：server：
                         port：8080
-yaml注意缩进 可以在json formatter网站检查
-yaml格式
     person:
        name: 12
        list（数组）:
            - code
            - music
        map: {k1: v1,k2: v2}

# 6 resource自动注入
-在容器中去找对应类名的对像注入

# 7 多环境配置
-有开发，测试，上线环境三种主要的不同的环境，每个环境的端口，上下文件，数据库url， 用户名，密码都不太一样，这时就需要多环境配置
-使用方式：1 创建名称不同的多个配置文件：application-环境.properties/yml eg:application-test.properties
                       2 在application.properties文件中指定用哪个: spring.profiles.active=dev


# 8 目录结构



# 9 后端三层架构
-这里的dto和entity都是封装数据的  dto更多是处理前端来的json格式的文件  entity是数据库的  两个不相通





# 9 创建springboot方法
-start.springboot.io
-直接创建maven项目 导入父依赖和springweb依赖：然后在resource创建一个application.properties文件

# 10 @SpringBootApplication
-主要有以下三个：
     @componentScan：扫描本包以及子包下的注解
     @springBootConfiguration：当作配置文件用。也就是说可以吧bean注入到容器
     @EnbaleAutoConfiguration(starter的核心功能)：吧大多数要用的例如mybaits创建好bean 注入到容器中
                                                             维护外部的配置文件 ：application.property
Starter是启动依赖，它的主要作用有几个。
Starter组件以功能为纬度，来维护对应的jar包的版本依赖，
使得开发者可以不需要去关心这些版本冲突这种容易出错的细节。
Starter组件会把对应功能的所有jar包依赖全部导入进来，避免了开发者自己去引入依赖带来的麻烦。
Starter内部集成了自动装配的机制，也就说在程序中依赖对应的starter组件以后，
这个组件自动会集成到Spring生态下，并且对于相关Bean的管理，也是基于自动装配机制来完成。
依赖Starter组件后，这个组件对应的功能所需要维护的外部化配置，会自动集成到Spring Boot里面，
我们只需要在application.properties文件里面进行维护就行了，比如Redis这个starter，只需要在application.properties
文件里面添加redis的连接信息就可以直接使用了。

# 14 jsp使用
-导入jsp依赖：

-main下创建webapp目录用来存jsp 但是创建好后一般发现无法新建jsp 需要把main添加为外网资源目录才行

-指定jsp存放目录



# 15 手动获取容器
-ApplicationContext ctx = springapplication.run(Application.class, args)
   ctx.getbean("xxx")

# 16 js303校验
-类上记得加@validate


# 17 post和get请求区别
（1）post请求更安全（不会作为url的一部分，不会被缓存、保存在服务器日志、以及浏览器浏览记录中，get请求的是静态资源，则会缓存，如果是数据，则不会缓存）
（2）post请求发送的数据更大（get请求有url长度限制，http协议本身不限制，请求长度限制是由浏览器和web服务器决定和设置）
（3）post请求能发送更多的数据类型（get请求只能发送ASCII字符）
（4）传参方式不同（get请求参数通过url传递，post请求放在request body中传递）
（5）get请求的是静态资源，则会缓存，如果是数据，则不会缓存
（6）get请求产生一个TCP数据包；post请求产生两个TCP数据包（get请求，浏览器会把http header和data一并发送出去，服务器响应200返回数据；post请求，浏览器先发送header，服务器响应100 continue，浏览器再发送data，服务器响应200 返回数据）


# 18 静态资源存放位置
-webjars  ：    localhost: 8080/webjars
-public/*      static/**         resources   
-优先级： resource》static》public
-注意：自己在配置文件里自定义目录后：spring.mvc.static-path-pattern=he 上面的就会失效


# 19 templates
-在template下的所有页面只能通过controller来跳转
-需要模版引擎thymeleaf的依赖

# 20 模版引擎thymeleaf
## 作用：  
模版引擎都放在服务器端，都是干差不多的事 就是把数据从后台取出来放到模版对应的坑里，然后把整个页面弄成html返回给浏览器
eg Hello ${xxx}>>>>>  Hello zhangsan
-template里的静态资源要通过controller跳转
-thymeleaf使用的时候要导入依赖 
-Thymeleaf特点：
动静结合： Thymeleaf 在有网络和无网络的环境下皆可运行，即它可以让美工在浏览器查看页面的静态效果，也可以让程序员在服务器查看带数据的动态页面效果。
Thymeleaf支持 html 原型，然后在 html 标签里增加额外的属性来达到模板+数据的展示方式。浏览器解释 html 时会忽略未定义的标签属性，所以 thymeleaf 的模板可以静态地运行；当有数据返回到页面时，Thymeleaf 标签会动态地替换掉静态内容，使页面动态显示。
开箱即用： Thymeleaf提供标准和spring标准两种方言，可以直接套用模板实现JSTL、 OGNL表达式效果，避免每天套模板、改jstl、改标签的困扰。同时开发人员也可以扩展和创建自定义的方言。
多方言支持： Thymeleaf 提供spring标准方言和一个与 SpringMVC 完美集成的可选模块，可以快速的实现表单绑定、属性编辑器、国际化等功能。
与SpringBoot完美整合，SpringBoot提供了Thymeleaf的默认配置，并且为Thymeleaf设置了视图解析器，我们可以像操作jsp一样来操作Thymeleaf。代码几乎没有任何区别，就是在模板语法上有区别。
————————————————
版权声明：本文为CSDN博主「龙源lll」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/Lzy410992/article/details/115371017
## jsp和thymeleaf区别：
改变html页面风格（Let's change the page style）
假象我们写完了页面，但是我们突然想改变一下按钮周围的颜色：从绿色改为淡蓝色。我们不确定那种蓝色更加合适，因此我们需要多次尝试不同的颜色组合。
下面看一下采用JSP和Thymeleaf的实现方式：
采用JSP修改html页面风格（Changing the page style using JSP）
第1步：将应用程序部署到开发服务器上，并启动服务器。如果服务器不启动，JSP页面不会渲染，因此这一步是必须的。
第2步：导航到需要修改的页面。通常情况下，需要修改的页面是该应用程序的所有页面中某一个，很有可能需要点击多个链接、提交多个表单、查询多次数据库后才能跳转到这个页面。
第3步：打开firebug、dragonfly或其他嵌入浏览器的web开发工具。通过这些工具我们可以修改页面风格，并直接作用到浏览器的DOM上，并显示给我们。
第4步：修改颜色。尝试多种颜色组合后，确定最合适的颜色。
第5步：复制修改过的代码，并粘贴到对应的CSS文件中。
完成！
采用Thymeleaf修改html页面风格（Changing the page style using Thymeleaf）
第1步：双击.html模板文件，在浏览器中直接打开它。由于是Thymeleaf模板，它将会正常显示，采用模板/原型（template/prototype）数据（注意订阅类型选项）：
第2步：使用文本编辑器打开.css文件。模板文件在其<link rel="stylesheet" ...>标签中链接了CSS（Thymeleaf在执行模板时会把该标签中的href替换为th:href）。因此对CSS文件的修改会显示在页面中。
第3步：修改颜色。和采用JSP一样，我们仍然需要尝试多种不同的颜色组合，使用F5刷新页面。
完成！
重大区别（That was a big difference）
步骤数量的差别并不重要（在Thymeleaf的例子中也可以使用firebug）。真正重要的区别在于其复杂性，JSP方式中每一步骤需要花费的精力和时间。采用JSP，就必须部署并启动整个应用程序，这使得JSP不如Thymeleaf方便。
下列情形将进一步体现上述区别的意义：
开发服务器并不在本地，而是远程服务器。
不仅修改CSS，而且添加或删除了一些HTML代码。
还未实现页面所需的后台逻辑
最后一点是最重要的一点：如果应用程序仍在开发中，页面展示所需的Java逻辑还未完成的情况下，我们如何给客户展示新的颜色？（因为此时java代码没弄完 你jsp编译都过不了怎么展示？）（或者想让顾客选择颜色）...
使用JSP作为静态原型不行吗？（And what about trying to use the JSP as a static prototype?）
你可能会问，我们为什么要那么费事儿的修改JSP，像Thymeleaf一样直接打开JSP不行吗？
答案是：NO。
我们可以试一下：我们要把.jsp文件的后缀名改为.html，打开后结果如下图：
页面哪去了？其实页面还是那个页面。只是为了让页面以JSP的方式执行，我们要添加许多JSP标签和特性。但是改为HTML后，浏览器就无法正确的显示了。
再一次回顾一下双击Thymeleaf模板打开后的样子：
完全不是一个级别的了。。。

# 21 thymeleaf语法
概述
-所有静态资源都要被thymeleaf接管 只要在元素属性前面加th：即可
使用前要做的
-使用前必须在html上加上命名空间：xmlns:th="http://www.thymeleaf.org" 不然
下面的有时有thymeleaf语法都不生效（命名空间：允许你通过一个网址来识别你的标记。）
-使用前要把模版引擎的缓存关闭 不然可能不生效
语法
-@{/css/....} ：链接要用
-#{...}：国际化消息取：
-fragment：html页面中可以定义碎片：<th:fragment=“xxxx”>
碎片可以插入到别的地方：<div th:insert="~{哪个页面（去除html后缀，但要带路径）:: 哪个碎片}">
注意：可以把这些公共的放到一个compont页面里
-$: 取变量
-each: 遍历
 <tr th:each="prod : ${prods}">
        <td th:text="${prod.name}">Onions</td>
        <td th:text="${prod.price}">2.41</td>
        <td th:text="${prod.inStock}? #{true} : #{false}">yes</td>
      </tr>

国际化
-webmvconguration里面有个localeResolver地区解析方法，里面大概意思是：
如果客户配置了就用客户配置的 没有就用默认的 我门需要自己配置 配置的时候
就是把http请求里面携带的lang值取出来，赋值给locael类就行
-resources下创建i18n文件夹
-i18ni下创建login.properties  和 login_zh_CN.properites 弄完后两文件自动合并
-添加英文的:login_en_US.properties(右击i18n也能创建)
eg: login.tip=请登录
-把login.tip绑定到html对应的地方
-页面左下角有个resourcse bundle按钮 点开可以可视化配置（同时配三个）
-application.properties里面配置：
-spring.message.basename=i18n.login
-想要实现点击自动切换 要自己在config配置自动化语言组件并将组件
配置到spring容器中（@Bean）


# 22 servelet和controller关系

-servlet是为了页面可以动态展示数据 通过doget  dopost方法实现相应，
通过内嵌java代码实现动态展示
-controller是mvc里的东西，表面上看功能就是servelet，但是单独拿controler
来说的的话它并没有做到网络层面的请求接受转发功能，可能只是实现了java代码
那部分。mvc里请求接收相应是dispatchsevelt实现的，所以mvc里的servelet应该是
dispatchsevelt+controller


# 23 JSP和servelet的区别
-servelt是java代码里填html：jsp没出来的 时候servelet是在java代码中拼接html代码返回给浏览器，你想想乱的很么，也很难维护么，满屏都是print打印语句，你html语法哪儿错了还没法报错因为都是字符串
-jsp是html里填java：jsp出来了，使用jsp直接可以在html页面挖坑，坑里写表达式，servlet返回过来的值被填在坑里，然后吧填好的html返回给浏览器。其实jsp底层还是拼接，只不过这些脏活累活它帮你做了，你的重点就可以放在servelt逻辑上了

-一句话：JSP是代替servelet view角色的servlet
-JSP就是servelt的封装，只不过可以直接写在html里，就能实现数据动态绑定了
-JSP最后还是翻译成servelet了：翻译规则


# 24 spring mvc自动配置
-想要扩展mvc配置比如过滤器 拦截器 格式转换器等：创建实现webMvcConfigurer接口配置类 (@confugration)   不要加@enabklemvc
-自己想要写定制化的组件 实现对应接口写完后@bean交给spring管理  spring就会给你自动装配

# 25 lombok
-动态生成get set tostring。。。
-@Data   get  set

-@AllArgsConstructor    有参
-@NoArgsConstructor      无参

# 26 repositoty
@Repository注解修饰哪个类，表明这个类具有对对象CRUD（增删改查）的功能。
被@Repository注解的类可以自动的被@ComponentScan 通过路径扫描给找到（与它的来源有关）。
与@Controller、@Service、@Component的作用类似，都是把类交给spring管理。@Repository用在持久层的接口上，这个注解是将接口的一个实现类交给spring管理。
将所标注的类中抛出的数据访问异常封装为 Spring 的数据访问异常类型。
————————————————
版权声明：本文为CSDN博主「weixin_38218035」的原创文章，遵循CC 4.0 BY-SA版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/weixin_38218035/article/details/127237933

# 27 resource 和 autowired区别
-都是用来传值的 你传个类 它就去spring工厂找对应类的对应对象
因为spring'工厂你要东西的时候它就给你new好了 所以传的是对象
-resource默认按名称找  找不到按类型
eg：User cxc 此时会先去找和cxc同名的类 找不到 去按User找如果此时User接口被两个类实现了 就报错 解决方法是酱cxc换成其中一个实现的
-autowired 正好相反 默认按类型注入
-使用autowired值为null
情况1：Bean对象并没有交给Spring管理
检查@Autowired的对象是否已经被注入到Spring容器中了；
确保使用@Autowired注解的对象也已存在Spring的容器中。
情况2：对象使用过new关键字
这是我遇到的情况，当一个对象使用过关键new时，它是不能被Spring所管理的。
所以如果在这些对象中使用@Autowired去注入对象，得到的结果也是为null


# 28 首页配置（想显示页面的初始化配置）
-静态资源托管给thymeleaf：你把路径手动改对了也能显示css这些，但是
就无法很好的动态匹配项目 就是有些自动匹配的东西你没法用 比如你弄了个下面👇说的虚拟路径，你的css访问有可能也会出问题。但是你把这些资源给thymeleaf这些事
它就会给你解决
-可以给项目加一个虚拟目录路径：
server.servlet.context-path=xxxx

# 29 Bean使用
-Bean的创建和使用
https://blog.csdn.net/liuyueyi25/article/details/83244239

# 30 controller接收请求参数的几种方法：@RequestParameter @RequestBody @pathvaiblaes @param（value="xx"）实体类 字符串
@Requestbody和@RequestParameter
Requestbody意思是取出post请求body中的数据 在变量前用这个意思是要把这个封装到指定的对象里
RequestParameter就是正常form中通过name传过来的值 
@pathvaiblaes：就是url路径里的值：@pathvariable(name="xxx")与@requestmapping（“/user/{xxx}”）中的xxx对应
@param（value="xx"）：用在变量前，就是给变量规定名字，经常在mapper（mybaties）中用到
@ResttController：相当于@ResponseBody和@Controller的结合。返回的是字符串
## 为什么要用requestparam接收参数而不是直接用变量？
写上reqeust这个注解就表示请里必须要有相关字段参数，如果没有就直接返回4xx的报错。4xx的报错意思是错误是用户自己导致的。如果不同，就不会有这种过滤功能。有没有参数都会进哪个controller方法。这对资源是一种浪费


参考：
https://blog.csdn.net/weixin_46141585/article/details/117391904

## 小坑：页面跳转后url不对
登录成功后重定向到某个页面 不然登录后url显示：xxx?user=xx,pws=xx
return "redirect:/xxx"

## 小坑：There was an unexpected error (type=Bad Request, status=400). Required String parameter 'username' is not present
-一旦我们在方法中定义了@RequestParam变量，如果访问的URL中不带有相应的参数，就会抛出异常——这是显然的，Spring尝试帮我们进行绑定，然而没有成功。但有的时候，参数确实不一定永远都存在，这是我们可以通过定义required属性：
@RequestParam(name="id",required=false)
//在参数不存在的情况下，可能希望变量有一个默认值
@RequestParam(name="id",required=false,defaultValue="0")
https://blog.csdn.net/qq_33840251/article/details/88774613

# 31 模拟数据库中的数据
-写对应的POJO类 把该有的字段都列出来
-创建一个POJO对应的Dao层做四件事：
    新建一个static map<Integer,POJO对象>的成员变量模拟数据库
    static方法中加入虚拟数据
    写一个获得所有数据的方法
    写一个通过id查对应数据的方法

-把Dao托管给spring：@repisitory（作用和component一样 专用于dao'）

# 32 拦截器
拦截器和过滤器的区别
拦截器是sprigmvc自带的 只是作用于controller层
拦截器怎么写
-在自己的配置文件里重写拦截器方法（implements HandlerInterceptor）
注意excludepathpatterens后面的是放行的

-在webmvncon类中把自己写好的拦截器注册到spring中：



# 33 get和post请求区别
1、 get是从服务器上获取数据，post是向服务器传送数据。
2、 get请求时通过URL直接请求数据，数据信息可以在URL中直接看到，比如浏览器访问；而post请求是放在请求头中的，用户无法直接看到。
3、 get传送的数据量较小，有限制，不能大于2KB；这主要是因为它受约于URL长度的限制。post传送的数据量较大，一般被默认为不受限制，但理论上，IIS4中最大量为80KB，IIS5中为100KB。
4、get请求因为数据参数是暴露在URL中的，所以安全性比较低，如密码不能暴露的就不能用get请求；post请求中，请求信息是放在请求头的，安全性较高，可以使用。
6、Get限制From表单的数据集的值必须为ASCLL字符，而Post支持整个ISO10646字符集。
说明：
1、get方式的安全性较Post方式要差些，包含机密信息的话，建议用Post数据提交方式；
2、在做数据查询时，建议用Get方式；而在做数据添加、修改或删除时，建议用Post方式；
以上就是get请求和post请求的区别有哪些？的详细内容，更多请关注php中文网其它相关文章！

# 35 @ResponseStatus   @Notblank @pattern
-REscontroller方法上用 指定返回状态
-Not类成员变量用 规定不为空  注意洗完后要用的话在引用变量前加@valide   但是在局部变量可以直接用！！！！
-pa：指定正则表达式

# 36 controller全局异常处理 
## 将异常暴露给后台
-controller包下新建ErrorResponse类 放在controller的原因是在这一层有response 可以返回友好的错误提示
-controller包下写异常处理类
@slf4j
@RestControllerAdvice
public class ControllerExpectionHandler{
@ExpectionHandler(Exception.class)
@ReasponseStatus(Httpstatus.INTERNAL_SERVER_ERROR)
public ErrorResponse hanlerExecption(Exception exception){
log.error(exception.getMessage(),exception);
return new ErrorResponse(500,exception.getMessage(),exception.getMessage())
}
}

-针对性处理exception：遇到哪个  复制哪个 处理哪个 （@exceptionhandler后面加入哪个class） 
还可以指定你想返回的状态码

可以循环取出同类异常下的所有异常


## 将异常暴露给前台

# 37 IOC
Spring Ioc容器
实现控制反转主要是BeanFactory和Applicationcontext两个接口。
BeanFactory
BeanFactory是一个管理Bean的工厂，该类会根据XML配置文件来装配Bean。
ApplicationContext
ApplicationContext是BeanFactory的子接口。创建ApplicationContext实例的方法有三种。


# 38 bean和component区别
@Component： 作用于类上，告知Spring，为这个类创建Bean。
@Bean：主要作用于方法上，告知Spring，这个方法会返回一个对象，且要注册在Spring的上下文中。通常方法体中包含产生Bean的逻辑。 相当于 xml文件的中<bean>标签。


# 40 修改和删除user
html里
<a th:href="@{/delete/}+${user.getUsername()}">
   <button type="button" class="btn btn-primary">delete</button>
</a>
controller里
@RequestMapping("/delete/{username}")
public String deleteUser(
        @PathVariable("username")
        String username
){
    userDao.deleteUser(username);
    return "redirect:/emps";
}


# 41 404 500....页面
-template下弄一个error文件夹 里面放个404.html 500.html 包相关错误会自动倒过来

# 42 注销
-session.invalidate()

# 43 注意
-contiroller别存临时变量  比如定义成员变量private map 吧来的request存到里面干个啥 这会导致很多问题 因为它会把每个reques都存 可能会引发一些问题

# 44 RESTful 架构
综合上面的解释，我们总结一下什么是RESTful架构：
　　　　（1）每一个URI代表一种资源；
　　　　（2）客户端和服务器之间，传递这种资源的某种表现层；
　　　　（3）客户端通过四个HTTP动词，对服务器端资源进行操作，实现"表现层状态转化"。

作者：AWeiLoveAndroid
链接：https://www.jianshu.com/p/84568e364ee8

# 45 RESTful feature：
## resources
-unserstandability:前后端都能懂
-completeness：一个url对应一个完整的资源（一个资源包含一些其他资源）
-linkbility: 前后端链接

## message：    
http request/response



## address：  
url（urL对应资源的那部分）定义规范
-用名词复数形式
-用小写字母
-向后兼容性：
get：如果你要变，不能直接改uri，因为这样前端也要改，可以重定向到新地址
post：把属性弄成optional  或者用版本eg：http://localhost:8080/api/v1/users/1

## method
post get put delete options

## statelessness
-idempotency密等性：相同的请求返回相同的结果  存钱50的请求发出去永远返回你余额50

## caching
作用
减少IO操作 提升performace
caching

分类
-client caching：不用发请求了
-CDN caching：存一些图片啥的
-server caching(redis spring自带caching)：就不用老去访问数据库了

# 46  openapi swaggerapi
作用
写代码的时候通过相关注释等直接把文档要的内容弄好了 使用这些文档依赖就可以直接倒出
关系
swagger维护openapi
怎么用
1.直接导入open API依赖 它会自动部署swagger-ui
<dependency>
    <groupId>org.springdoc</groupId>
    <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
    <version>2.0.2</version>
</dependency>
2. 路径后加 /v3/api-docs  访问openapi
3. 路径后加swagger-ui.html 访问swagger、

api上怎么加描述
方法上加 @Operation(summary = "xxx")


# 47 error: src refspec main does not match any.
error: failed to push some refs to 'git@github.com:ShaunChang/hello-world.git'
-本地分支与远程分支不同名或没有关联 

# 48 过滤器
步骤一：自定义过滤器
public class MyFilter implements Filter{
@Override
public void doFilter(xxxx){
xxxxx
filterChiain.doFilter(serverletRequest,servletResponse)
}
}
步骤二：把过滤器加入容器中
@Configuration
public class WebApplicationConfig{

@Bean
public FilterRegistrationBean filterRegistrationBean(){
FilterRegistrationBean bean = new FilterRegistrationBean();
bean.setFilter(new MyFilter());
bean.addUrlPatterns("/user/*");
return bean;
}
}


# 49 aoplication配置字符编码
server.servlet.encoding.charset=utf-8
server.servlet.encoding.force=true

# 50 mybaits 操作mysql
## 步骤
### 1 加入mybaits起步依赖
选mybatis framework和mysql driver两项
要么手动添加：
```java
<dependency>
    <groupId>org.mybatis.spring.boot</groupId>
    <artifactId>mybatis-spring-boot-starter</artifactId>
</dependency>

<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>  
    </dependency>   
```



### 2 pom.xml文件制定把java目录中的xml文件包含到classpath中
目的是使所有的xml文件都被放到target下的classes目录中，这样程序运行的
时候就有这些xml文件
```java
<resources>
<resource>
<directory>src/main/java</directory>
<includes>
<include>**/*.xml</include>
</includes>
</resource>
</resources>
```


### 3 创建实体类
-pravite属性 @Data
### 4 创建Dao接口及对应的增删改差方法
-创建StudentDao类
-创建接口方法：Student selectById(@RequestParam  Integer id);
-让项目识别mapper
第一种方法
在类名上加@Mapper告诉myubatis这是dao接口 在 Spring 程序中，Mybatis 需要找到对应的 mapper，在编译的时候动态生成代理类，让代理类去做链接数据库等那些冗余的脏活累活，实现数据库查询功能，所以我们需要在接口上添加 @Mapper 注解。
这里
第二种方法
```java
@mapper你嫌麻烦你可以在application类上写mappersacn 一下全扫描出来
@SpringBootApplication
@MapperScan("com.scut.thunderlearn.dao")
public class UserEurekaClientApplication {
public static void main(String[] args) {
SpringApplication.run(UserEurekaClientApplication.class, args);
}
}
```

### 5 创建接口对应的mapper文件 xml文件 写sql语句
-创建同名.xml文件
```java
<?xml version="1.0" encoding="UTF-8" ?>
<!DOCTYPE mapper
PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
"http://mybatis.org/dtd/mybatis-3-mapper.dtd">
<mapper namespace="dao接口的全限定名 可以右建复制">
<insert id="方法名称" parameterType="要返回的类的全限定名">
</insert>
<select id="" resultType="">
select id,name,age, from student where id=#{dao中绑定的那个值}
<selcet>
</mapper>
```

### 6 创建service接口以及实现类
-创建service接口并定义一个方法不用煮食
Student queryStudent(Integer id);
-创建serviceImpl方法实现接口 用@serviece注释
1 引入要用的Dao接口：@Resource  pravite xxxxDao xx
2 重写方法：
Student student = studentDao.selectById(id)
return student
### 7 创建controler对象访问service
第一种方法
-@Resource private xxxService xxx
第二种方法
@@RequiredArgsConstructor
1.必须声明的变量为final
​ 2.根据构造器注入的，相当于当容器调用带有一组参数的类构造函数时，基于构造函数的 DI 就完成了，其中每个参数代表一个对其他类的依赖。基于构造方法为属性赋值，容器通过调用类的构造方法将其进行依赖注入
### 8 写appplication,properties文件 配置数据库的连接信息
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/springdb?useUnicode=true&characterEncoding=UTF-8&serverTimezone=GMT%2B8
spring.datasource.username=root
spring.datasource.password=
# 51 dao和mapper分开管理
-吧xml文件放到resource下的mapper包（自建）下
-application.properties: mybatis.mapper-locations=classpath:mapper/*.xml
-pom: resource: directory:src/main/resources  include: **/*.*
# 51 mabites 日志log
-applciation.properties: 
mybatis.configuration.log-impl=org.appache.ibatis.logging.stdout.stdOutImpl
# #52 事务 没学完
springBoot用什么处理事务
使用事物管理器接口（DataSourceTransitionManager）管理事务，有不同实现类比如jdbc或mybatis
如何设置事务一些属性
-使用申明式事务，就是在xml文件配置：隔离级别，传播行为，超时时间
事务怎么用：
springboot框架
在业务方法上加@Transactional，此方法就具备了事务功能
在主启动类上加@EnableTransactionManager
aspect框架
在xml文件中配置事务控制的内容

# 53 项目依赖
    lombok
    Spring web
    spring Data JPA
    H2 database
    PostgreSQL Driver
    Validation
    Flyway Migration
    Spring boot Actuator

# 54 mapper文件
## 目的
做entity和dto之间的转化。比如把user转化为其他dto。。。。
## 如何使用
### 传统
-创建UserMapper类   
-类上加@component：不加就无法在service这样用：private final UserMapper   
-在service里引入：private final UserMapper
-UserMapper里面写上usermapperToxxx  UserMapperToxxx这些方法，方法里面就是最笨的那种写法：xxx.setxx(user.get(xxx))
### Mapper插件
-导入依赖：
implementation 'org.mapstruct:mapstruct:1.5.2.Final'
annotationProcessor 'org.mapstruct:mapstruct-processor:1.5.2.Final'
-定义userMapper接口,里面规定方法名，传入值，转出值即可
```java
@Mapper(componentModel="spring")
public interface UserMapper{
    UserGetDto mapperUserToUserGetDto(User user);
}
```
-转换过去后变量名不一样的解决办法：在方法上加：
@Mapper(source = "xxx",target = "xxx")
-转换过去后数据类型不一样的解决办法：在mapper后的uses属性中添加那个缺失的数据转换
@Mapper(componentModel="spring"，uses="UserMapper.class")

### builder
在要转换的类上加@builder
然后在转换类里写：
```java
 public PropertyGetDto mapperPropertyToPropertyGetDto(Property property){
        User user = property.getUser();
        UserGetDto userGetDto = userMapper.mapperUserToUserGetDto(user);
        PropertyGetDto propertyGetDto = PropertyGetDto.builder().typo(property.getTypo()).userGetDto(userGetDto).size(property.getSize()).id(property.getId()).build();
        return propertyGetDto;
    }
```


# 55 为何能使用private final xxx代替@Resource
原因
注意文章的第一句话有构造方法的Bean是可以通过private final来引入的，而上述的Controller中是加了@AllArgsConstructor注解的，它会给这个类加上全参的构造函数，这样就会在该类初始化时同步给属性初始化，也就是调用各引用Bean的初始化方法
因此就可以使用private final的形式来进行引用bean了
注意同一个类不要使用两种引入方式，要么用private final，要么用@Autowried


# 56 unit test
## 什么是unit test
前端来说一个组件测试，后端来说一般指一个类的测试
## unit test的意义是什么或者说为什么不直接弄个class在里面写测试
你想想，现在比如要测试dao文件，如果不用单元测试，那势必会执行dao中的数据库操作，如果此时你的数据库没有启动起来，首先这一步你就错了，后面的dao的结果肯定错。你的工作重心是在dao层的代码逻辑，而你的测试却是由一个不相干的数据库的问题而导致了失败。很冤枉。所以在unit case中所有的依赖部分的代码和数据可以自己模拟，那个方法其实压根就没有执行。一句话，单元测试目的是排除干扰。
## service等普通类测试步骤
1 类上加@ExtendWith(MockitoExtension.class)  
2 用@mock引入测试此类中用到的额外的成员变量  
3 用@InjectMocks注解引入你想测试的类 
4 import static org.mockito.Mockito.*;  import static org.junit.jupiter.api.Assertions.assertEquals;
5 测试方法
其中写when 。。thenreturn中写的都是你要测的那个方法中用到的外部方法，这些方法在上面已经被mock过了，所以是假的，代码走到那儿的话不会执行，你要模拟执行一遍，返回假数据。那么为什么要把这些mock呢？直接用不就行了。原因是为了保证这个测试的纯粹。本测试不想测试这些依赖方法，就用mock的方式模拟返回数据

```java
 @Test
    void getUser() {
            User user = new User();
            Long userId = 1L;
            user.setId(userId);
            user.setPassword("11111");
            user.setName("cxc");
            user.setEmail("943294932423");

            UserGetDto userGetDto = new UserGetDto();
            userGetDto.setEmail("943294932423");
            userGetDto.setName("cxc");

            when(userRepository.findById(userId)).thenReturn(Optional.of(user));
            //注意这里是userRepository.findById(userId),不是service.findUser方法 因为@mock的是注意这里是userRepository
            when(userMapper.mapperUserToUserGetDto(user)).thenReturn(userGetDto);
            assertEquals(userService.getUser(userId),userGetDto);

            }
```

## mockMVC
1 成员变量加入mockMVC：  
private MockMvc mockmvc;  
2 在@BeforeEach方法下初始化mockmvc 可以只通过自己要测的那个类初始化 这样加载的资源就少环境相对干净  
写法一：
类名上加springbootest注释
@BeforeEach
void setup(){
 mockmvc = MockMvcBuilders.standaloneSetup(new 你要测的类名()).build();}  
 写法二： 在测试类名上加@WebMvcTest(xxxx.class) 然后在下面直接autowired mockmvc beforeeach也不要了   
3 在测试类中用perform模拟请求然后用andExpect测试是否符合预期：
```java
@Test
void xxx(){
get请求：mockmvc.perform(MockMvcRequestBuilder.get("controller  url"))
post请求：mockmvc.perform(MockMvcRequestBuilders.post("url").content(asJsonString(new User(xx,"xxx","xxx"))).contentType(MediaType.APPLICATION_JSON).accept(MediaType.APPLICATION_JSON))
.andDO(print())
.andExpect(status().isok())
.andExpect(content().string("xxx"))}
.andExpect(jsonPath("$.id").value("xxx"))   就是测响应的json里具体某个属性的值
```
小坑：applciation starter failed ：找不到。。dao 原因是没有把所有要的类扫描 记住这是一个“干净”的环境   
解决方法一：@WebMvcTest({IndexController.class,UserDao.class}) .  
解决方法二：
```java
@ComponentScan(basePackages = {"com.tobacco.casemanagement"})
class IndexControllerTest {
    @Autowired
    private MockMvc mvc;

    @Test
    void loginController() throws Exception {
        mvc.perform(MockMvcRequestBuilders.get("/login?username=cxc&password=123"))
                .andDo(print())
                .andExpect(status().isOk());
    }
```


# 57 @Entity @Table(name = "xx")
@Entiry：这个类被映射为数据库中的同名表 默认为类名
```java
@Getter
@Setter
@Entity
public class Property {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String typo;
    private Integer size;

    //这里你想直接显示owner id对应的哪个user 就得在代码里接着查一步 告诉代码依赖关系以及根据什么查
    @ManyToOne
    @JoinColumn(name = "owner_id")
    private User user;

    @CreationTimestamp
    private OffsetDateTime created_time;
    @UpdateTimestamp
    private OffsetDateTime updated_time;
}
```
@Table：类名与表名不同时通过这个注解指定

# 58 状态码
## 删除
@ResponseStatus(HttpStatus.NO_CONTENT)
## post
@ResponseStatus(HttpStatus.CREATE)
## 其他的暂时没看到

# 59 联表查询两种方式、
## 推荐方式二 更加oop 且所有方法都在自己service里 不需要跨类调动 更加结偶
## 方式一 调用对应的service层查询
比如要通过userid查对应的property。在usercontroller调用propertyservice的findPropertubyUseriid方法
```java
public List<PropertyGetDto> findPropertyByUserId(Long userId){
        List<Property> byUser_id = propertyRepository.findByUser_id(userId);
        List<PropertyGetDto> propertyGetDtos = byUser_id.stream().map((property) -> {
            return propertyMapper.mapperPropertyToPropertyGetDto(property);
        }).toList();
        return propertyGetDtos;
    }
```
## 方式二 在entity表中就一步到位让它自动查好给你放那儿即@ManytoOne
user entity中
```java
    @OneToMany(mappedBy = "user")
    private List<Property> propertyList;
```
property entity中
```java
    @ManyToOne
    @JoinColumn(name = "owner_id")
    private User user;
```
userService方法
```java
public List<PropertyGetDto> findPropertyByUserId(Long userId){
        User user = findUser(userId);
        List<Property> byUser_id = user.getPropertyList();
        List<PropertyGetDto> propertyGetDtos = byUser_id.stream().map((property) -> {
            return propertyMapper.mapperPropertyToPropertyGetDto(property);
        }).toList();
        return propertyGetDtos;
    }
```
