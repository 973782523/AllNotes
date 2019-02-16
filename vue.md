### yarn

```javascript
初始化 
yarn init yes
添加依赖
yarn add [package]
升级依赖
yarn upgrade [package]
移出依赖
yarn remove [package]
```

### npm

```
npm i
npm init --yes
npm i gulp-pug gulp-debug gulp-sass
//生产依赖
npm i gulp -P
//开发依赖
npm i gulp -D
//不添加到package.json
npm i gulp --no-save
指定下载版本
npm i vue@2.5.15
卸载package包
npm uninstall vue  //可以使用rm  un   r
全局安装
-g
强制清除缓存 
npm cache clean --fore
```

### bower

```
它是从github下载的
初始化
bower init yes
更新
bower update  包名
卸载
bower uninstall 包名
删除缓存
bower cache clean
添加依赖
bower install 包名
```

### webpack

```js
初始化
npm init -y
    全局安装
    npm install webpack -g  //不推荐
本地安装
npm install webpack webpack-cli -D  //-D 开发依赖

执行webpack
npx webpack  //打包

npm install lodash -D

npm install webpack-dev-server -D
npm install html-webpack-plugin -D

//css
npm install style-loader css-loader -D
webpack.config.js
module: { // 所有 非.js 结尾的第三方文件类型，都可以在 module 节点中进行配置
    rules: [ // rules 是匹配规则，如果 webpack 在打包项目的时候，发现，某些 文件的后缀名是 非 .js 结尾的
      //  webpack 默认处理不了，此时，webpack 查找 配置文件中的 module -> rules 规则数组；
      { test: /\.css$/, use: ['style-loader', 'css-loader'] }
    ]
  }
//less
npm install less-loader less -D
{ test: /\.less$/, use: ['style-loader', 'css-loader', 'less-loader'] }

//sass
npm install sass-loader node-sass -D
{ test: /\.scss$/, use: ['style-loader', 'css-loader', 'sass-loader'] }

//加载图片
npm install url-loader file-loader -D
{ test: /\.jpg|png|gif|bmp$/, use: 'url-loader' }

```

### [vue指令](https://blog.csdn.net/wulala_hei/article/details/85000530)

```
npm install webpack webpack-cli -g
npm install -g vue-cli
vue init webpack vue_demo
cd vue_demo
npm install 
npm run dev
```

### vue

```js
beforeCreate      created  初始化后
beforeMounted		mounted  挂载后
ref  获取dom节点
    <p ref="myp">{{msg}}</p>
    this.$refs.myp获取这个div
由于dom的渲染是异步的 $nextTick 如果数据变化后想获取真实dom中内容,需要等待页面刷新后在去获取
所有的dom操作最后用$nextTick中

全局组件
   Vue.component('my-handsom',{
        template:'<div>{{msg}}</div>',
        data(){
          return {msg:'我很英剧'}
        },
    });
局部组件
	components
	三步取: 创建  注册  使用
	     let handsome={template:'<div>{{msg}}</div>',data(){
       			 return  {msg:'张三'}
        }};
		components:{
            handsome,
            methods:{
                
            }
        }
        在页面上使用这个标签
        
子传父
 let vm=new Vue({
        el:'#app',
        data:{
            money:400,
        },
        methods:{
          things(val){
            this.money=val;
          }
        },
        components:{
            child:{
                props:['m'],
                template:'<div>儿子{{m}} <button @click="getMoney">多要钱</button></div>',
                methods:{
                    getMoney(){
                        this.$emit('child-msg', 800);//触发自己的自定义事件,让父亲方法执行
                    }
                }
            }
        }
    })
    //儿子的自定义方法方法执行父亲的方法,
    <div id="app">
    父亲:{{money}}
    <child :m="money" @child-msg="things"></child>
	</div>
简单的理解子组件传递参数给父组件
    子组件
    <button @click.self="$emit('patch')">加一块钱</button>
	$emit()里面的第一个参数是传递给父组件的自定义方法,第二个参数是一个对象,可以是需要传递给父组件的对象
	父组件
    <User @patch="ttt"/>
        //methods 执行这个方法
        ttt() {
                this.money++
            }
slot

<div id="app">
    <modal>
        <a href='http://www.baidu.com'>去百度</a>
        <p slot="content">是否删除</p>
        <h1 slot="title" @click="fn">是否删除??</h1>
    </modal>
</div>
<!--slot作用 定制模板-->
<!--模板中只能有一个根元素,可以通过元素属性定制模板-->
<!--slot 中可以放置一些默认的内容,如果传递了内容则替换掉-->
<!--如果没有名字的标签默认会放置到default-->
<template id="modal">
    <!-- 这里放的内容属于父级当前模板的,只有属性名是属于组件的-->
    <div>
        <slot name="title">默认标题</slot>
        <slot name="content">这是一个默认标签</slot>
        <slot name="default">这是一个默认标签</slot>
    </div>
</template>
    let vm=new Vue({
        el:"#app",
        data:{

        },
        components:{
            modal
        },
        methods:{
            fn(){
                alert(1)
            }
        }
    })
操作挂载后组件的dom    
    <loading ref="load"></loading>

mounted(){//ref 如果放在组件上,获取的是组建的实例,并不是组件的DOM元素
            // this.$refs.load.hide(); 想操作dom 就加一个$nextTick
            this.$refs.load.$el.style.backgroundColor = 'red';
        },    
        
----------------
<div id="app">
    <input type="radio" v-model="radio" value="home">home
    <input type="radio" v-model="radio" value="list">list
    <!--一般用作缓存:为的是后面路由做准备-->
    <keep-alive>
        <component :is="radio"></component>
    </keep-alive>
</div>
    /* 子组件和父组件同时拥有mounted方法,会先走谁*/
    /*需要等待子组件挂载完成后在触发父组件的挂载*/
    let home = {template:"<div>home</div>"};
    let list = {template:"<div>list</div>"};
    let vm=new Vue({
        el:"#app",
        data:{
            radio:'home'
        },
        components:{
            home,list
        }

向子组件传送数据是通过props实现的
     <foo-component :foo-message="fooMessage"></foo-component>
     /*type  能够指定的类型
        String Number Boolean Function Object Array Symbol
        required 声明这个参数是否必须传入
        default 选项来指定当父组件未传入参数是props变量的默认值
        当type的类型为Array或者Object的时候default必须是一个函数
        自定义函数校对
        * */
      props:{
          fooMessage: {type:[Number,String],required:true}
      },
      template:'<div>{{fooMessage}}</div>'   
      
//props总结      
      props: {
    // fooA只接受数值类型的参数
    fooA: Number,
    // fooB可以接受字符串和数值类型的参数
    fooB: [String, Number],
    // fooC可以接受字符串类型的参数，并且这个参数必须传入
    fooC: {
        type: String,
        required: true
    },
    // fooD接受数值类型的参数，如果不传入的话默认就是100
    fooD: {
        type: Number,
        default: 100
    },
    // fooE接受对象类型的参数
    fooE: {
        type: Object,
        // 当为对象类型设置默认值时必须使用函数返回
        default: function(){
            return { message: 'Hello, world' }
        }
    },
    // fooF使用一个自定义的验证器
    fooF: {
        validator: function(value){
            return value>=0 && value<=100;
        }
    }
}
slot 绑定数据
父组件
因为组件中只能包一个div,所以可以用template包起来
slot-scope是让slot具有私有性
<div slot="wang" slot-scope="item">
            <div v-for="sex in item.data">
                {{sex}}
            </div>
</div>
子组件
<slot name="wang" :data="sexArr"></slot>
 data(){return { sexArr:['男','女']
                    }
                }
父组件与子组件的数据通信
    父组件
     <TodoFooter :class1="class1"/>
     data(){
         return{
             class1:'zhangsan'
         }
     }
     子组件
     props: ['class1']
     
子组件与父组件
$emit
父组件
<button-counter v-on:increment="incrementTotal"></button-counter>	
  methods: {
            incrementTotal () {
                this.total++
            }
        }
子组件
   metheds: {
            incrementCounter () {
                this.$emit('increment')
                this.counter++
            }
        }
        
vue 消息订阅与发布

缓存路由
    <keep-alive>
            <router-view></router-view>
    </keep-alive>
向路由组件传递数据
$route.params.id
注意是route不是router不要写错了

编程式路由导航
this.$router.push(path) :想当于点击路由链接(可以返回到当前路由界面)
this.$router.replace(path):用新路由替换当前路由(不可以返回到当前路由界面)
this.$router.back() 请求(返回)上一个记录路由
this.$router.go(-1) 请求返回上一个记录路由
```

向路由组件传递数据和编程式路由导航

```js
父组件
<template>
<div>
  <!--<p>{{// $router.params.id}}</p>-->
  <ul>
    <li v-for="(message,index) in messages" :key="message.id">
      <router-link :to="`/home/message/detail/${message.id}`">{{message.title}}</router-link>
      <button @click="pushShow(message.id)">push查看</button>
      <button @click="reqplaceShow(message.id)">replace查看</button>
    </li>
  </ul>
  <button @click="$router.back()">回退</button>
  <hr>
  <router-view></router-view>
</div>

</template>

<script>
    export default {
        name: "Message",
      data(){
          return{
            messages:[],
          }
      },
      methods:{
        pushShow(id){
          this.$router.push(`/home/message/detail/${id}`)
        },
        reqplaceShow(id){
          this.$router.replace(`/home/message/detail/${id}`)
        },
      },
      mounted(){
          //模拟ajax请求从后台获取数据
        setTimeout(()=>{
          const messgesd=[
            {
              id:1,
              title:'message001',
              content:'message001 content...'
            },
            {
              id:2,
              title:'message002',
              content:'message002 content...'
            },
            {
              id:4,
              title:'message004',
              content:'message004 content...'

            }
          ];
          this.messages=messgesd;

        })
      }
    }
</script>

<style scoped>

</style>


子组件
    <template>
      <div>
        <p>{{$route.params.id}}</p>
        <ul>
          <li>id:{{messageDetail.id}}</li>
          <li>title:{{messageDetail.title}}</li>
          <li>content:{{messageDetail.content}}</li>
        </ul>
      </div>

    </template>

    <script>

        export default {
            name: "MessageDetail",
          data(){
              return{
                messageDetail:{
                }
              }
          },
          mounted(){
              setTimeout(()=>{
                const allMessageDetails=[
                  {
                    id:1,
                    title:'message001',
                    content:'message001 content...'
                  },
                  {
                    id:2,
                    title:'message002',
                    content:'message002 content...'
                  },
                  {
                    id:4,
                    title:'message004',
                    content:'message004 content...'

                  }
                ];
                this.allMessageDetails=allMessageDetails;
                const id=this.$route.params.id*1;
                this.messageDetail=allMessageDetails.find(detail=>detail.id===id)
              },1000)
          },
          watch:{
              $route:function (value) {
                const ids=value.params.id*1;
                this.messageDetail=this.allMessageDetails.find(detail=>detail.id===ids)
              }
          }
        }
        
vuex 
npm install vuex -D
```

style中的scoped是限定样式的作用范围

# JavaScript 风格指南

# 代码整洁的 JavaScript

# JavaScript 代码简洁之道



### //5-3

//尚硅谷61

//珠峰女 vue14

//珠峰男 vue06

### vue-cli@3

> yarn global add @vue/cli
>
> vue create 项目名
>
> cd 项目名
>
> yarn serve

为什么data是一个函数:每一个实例的data属性都是独立的,不会相互影响的

### .self修饰符

>  self是只执行子级本身的函数 
>
> .stop和.self的区别，前者是防止事件冒泡，后者则是忽略了事件冒泡和事件捕获的影响。只有直接作用在 该元素上的事件才会被调用 

```js
 <div class="mid" @click.self="getTarget($event)">
```

### 去掉webstrom的单词波浪线

>  光标选中该单词，alt+enter，关闭相应选项即可。 

vue编译报错

> 在目录下新建一个`vue-config.js`
>
> ```js
> 
> ```
>
> 