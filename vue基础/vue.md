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





































