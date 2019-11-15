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