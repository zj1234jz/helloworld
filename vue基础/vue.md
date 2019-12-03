# 插值表达式

* 书写 {{ a }}  两个花括号 花括号之间一定需要等号 
* 原始值 undefined 不会显示在插值表达式中
* 如果要在标签里面输入真正的html 代码，那么使用标签 v-html=""
        注意这里会产生xss 攻击
    
* 数据必须先存在 才能被渲染 


*  通过改变数组的长度和索引是不能引起视图的刷新

*  数据要先存在，才能实现数据绑定

*  数组变异方法有七个
      push shift  unshift pop sort reverse splice 

*  $set 可以修改数据并且刷新视图

    vm.$set(修改的数据，修改数据的属性，修改成什么值);

    vm.$el   vm.$nextTick(()=>{
        这里是页面渲染之后的回调函数
    }) 

*  页面的渲染是异步的，数据的更改是同步的 

*  $mount


# 指令

* v-pre  不编译当前dom 保留原始输出
* v-cloak  在dom 被编译之前保留 可以配合css 进行隐藏 在html效果明显，在vue文件没多大效果
* v-once 当前dom 数据只渲染一次
* v-html="" 当前dom 里面要添加的innerHtml 这里需要注意xss攻击
* v-text="" 当前dom 里面要添加的innerText  跟插值表达式唯一的不同在于会覆盖当前dom 的文本节点

* v-if: 判断当前节点是否存在  一般可以配合<template></template>使用
其中template 没有意义，也不会被渲染进页面

* v-if v-else 

* v-if v-else-if v-else 

* v-show  和v-if 的区别  第一 v-if 是直接不存在  v-show 是使用display：none 第二 v-show 在template上不生效

* v-bind:简写为：，为dom  属性绑定上数据 后面的双引号 "" 相当于{{ }}  

* 绑定class时如果绑定多个class 则需要用数组把他们放在一起  注意绑定class 的时候只能绑定一次，也就是只有第一次绑定生效 注意这里只是帮组你添加
* 或者不添加class,并不是帮你清除class,添加style也是一样，只识别数组和对象语法

* v-on: 《==》@ 给dom 绑定事件 而且在methods中正常 函数的this 是该vue实例，如果是箭头函数this则为window  且名称不能跟data 中相同，不然会有冲突
* 其实在data 中定义函数的话this 指代 window ,从这里可以分析出，vue 数据首先会从data 里面找 ，然后去其他地方找

* 其实在data中定义的函数不传参数时this 指向window 传递参数时this 指向 vue实例 
* 建议学习 vue 使用vue 开发版，因为开发版规范vue 

* v-for指令 遍历对象（key,value）in obj  遍历数组(item,index) in arr 其中一定要加:key 且key 唯一，key的存在主要是增加性能

* v-for 可以遍历数字  v-for="item in 8"  1 2 3 4 5 6 7 8 数字从1 开始 也可以遍历字符串 
* 使用v-for 可以使用template模板，但是key绑定要在真实的元素上
* key 的作用在于是否dom重新渲染，所以在某些情境下可以增加key 然后让dom 重新渲染
* v-model 双向数据绑定，是value 和input的语法糖
* input text  checkbox radio  textarea select 这些都可以实现数据的双向绑定 其中checkbox 可以使用数组绑定
* selected 可以使用disabled禁止选择， 同事也可以实现多选 多选状态下需要按住ctrl 
* $event vue 用来记录当前事件源对象 
* 修饰符   事件可以有修饰符 @keyup.enter   或者@keyup.13  可以给修饰符取别名 Vue.config.keycodes={ 'fly-code':112} //注意这里的可以使用连字符 -

* v-model 修饰符  .number 把数字字符串变成数字  .lazy 绑定value 和 onChange事件 .trim  去除前后空格，中间的不能去除

* vue 自定义指令 
	
	全局指令 
		Vue.directive("slice",(el,bindingd,vnode)=>{//第一个参数为指令 名称 使用时要加v-slice 第二个参数可以为函数，或者对象
			el  :表示当前指令绑定的dom 元素 
			bindings：里面有很多东西 
			{
				args:表示参数      传入方法  v-slice：9.number
				name:
				rawname:
				expression:表示当前绑定的变量
				value：表示当前绑定的值
				modifiers:{number:true}
				def:{bind,update}
			
			}
			vnode : context  记录当前vue实列
			
		
		})
		
		//{}第二个参数是对象的时候
		{
			bind(el,bindings,vnode){
				值绑定的时候会调用
			
			}
			update(){
				//值更新的时候调用
			}
			
			inserted(){
				//插入dom元素的使用调用
			}	
		}
	局部自定义指令
		directives：{
		
			"slice":（）=》{//key 对应指令名字 后面依然可以是函数或者对象
			}
		}

* 过滤器 (不改变数据本身，改变数组展示)
	
	全局过滤器 
	Vue.filter("name",()=>{
		return newvalue;
	})
	使用 {{money | name}}
	
	局部过滤器
	
	filters:{
		function(){
		}
	}
# vue的渲染过程以及jsx语法

* $el  > $mount -->template--> 拿到模板  ---> AST(抽象语法树)-->render-->Vnode(虚拟dom)-->真实Dom 

* jsx语法 
    >代码如下
   ```
   render(h){
                return h("h4",{
                    class:"red",
                    style:{
                        color:"red",
                        fontSize:"25px"
                    },
                    domProps:{
                        innerHTML:"我不是h4标题"//会直接覆盖innerHTML
                    }
                },[
                    "我是一级标题",//这里可以写成多个dom 元素
                    h()
                ])

            }
    ```
    >于是有了jsx语法 js 写在{}里 dom 写在<>里 这里注意要在HTML里面显示需要其他解析工具,这里标签也可以是变量
    ```
    render(){
        return (
            <h1 style={{
                color:"red",
                fontSize:"25px"
            }}
            on-click={console.log(a)}//这里on-click必须要加-
            >

            </h1>
        )
    }

    ```

# vue生命周期

* markdown在线编辑器 [在线编辑](https://www.mdeditor.com/)
    ![生命周期](https://cn.vuejs.org/images/lifecycle.png)
    



# 组件之间的通讯1

>使用属性绑定  props
* 没绑定的属性会被存在 vm.$attrs 里面 ，直接绑定这个对象，语法为 v-bind="$attrs" 这样没被绑定的属性会出现在html 结构中。这时可以使用
inheritAttrs = false 这样就不会出现没绑定的自定义属性，但是原有特性任然会出现，比如说class

>使用$parent 和$children 

>使用provide 和 inject 
 
```
provide:{
	title:"title"，
	name:"zj",
}
inject:["title"]

```
![ui 图](file:///C:/Users/dell/Desktop/%E5%88%86%E5%B1%8F/ui/ui1.png)

# 子组件如何向父组件传递数据
>使用 \$children 一般来说\$parent 只有一个，但是$children 是一个数组，因为可以有多个 


>使用\$refs 这里需要注意两点 第一是如果把ref="same" 作用于多个dom 那么只会识别最后一个dom 如果是使用v-for 循环，那么会被变成数组

>技巧传值，只用过函数传值，这个不常用，或者说属于基础知识

>监听组件点击 默认情况下组件是无法响应事件的，需要添加修饰符.native 才可以向原生dom那样实现点击

>关于$attrs 和 props 和 $listener 三者之间的关系 非事件对象可以用$attrs 和 props 这两者的区别在于子组件是否有注册使用，而$listenner则保存该组件的事件属性

>使用$emit() 方式触发组件事件，既然组件自己本身不知道自己被点击了，那么就内部提醒一下 使用 $emit("click","params")

>$listenner 如何绑定 使用v-on 可以把该组件所有事件直接绑定在在组件dom上 


# 组件之间传递数据值eventbus

>综述：就是利用vue 原型上的一个vue实列，然后通过对该实列的发布$emit()事件和订阅 $on("click",()=>{}) 实现数据通信、

# 关于vue实列的this 
>在跟实列中data中的this指向window 在组件中data 中的this指向其vue实列

>vue 中的单向数据流概念

* 父子组件的双向数据传递 
  
>第一使用：value + @input  ==>v-model

>第二使用：:value + @update:value ==>:value.sync 的语法糖

# 关于slot (插槽)

>何时需要  在一个组件里还想插入HTML 或者其他dom 默认是不支持的，但是可以使用插槽

```
<my-component>
	这是一个按钮
	<tempalte v-slot:name值>这是一个sb </template>
</my-component>
js
	components:{
		myComponent:{
			template:<div><slot name="default"></slot></div>
		}
	}

```
>注意点
* 第一是 v-slot: 的简写为#
* 第二是 组件内部没有slot 的情况下是不会渲染组件标签里的东西
* 第三是 组件里面有没写名字的slot 标签，默认外部组件标签里的东西会被插入到该slot 里
* 第四是如果外部使用标签 并且指明名字的插入 会插入到内部对应名字哪里

# 安装脚手架

	* npm install -g @vue/cli 用于快速创建项目
	* npm install -g @vue/cli-service-global 用于原形开发，编译.vue 文件	
	* npm uninstall vue-cli -g 用于卸载之前的旧版本
	* npm  install -g@vue/cli-init 安装桥接工作 可以使用旧版本的init
	* 插件文明 Vetur 

# 递归组件 如何在组件内使用自身 

	给组件命名{
		name:""
	}
	再使用

	还有如何利用v-if  和v-show 的配合 

































