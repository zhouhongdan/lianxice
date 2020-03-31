# lianxice
平时练习测试

# 2月20日
去重  new Set()	所有的成员都是唯一，不可重复	可用于去重	new Set([1,2,2,3])	[1,2,3]

      Array.from()	从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例	[...new Set([1,6,2,6,3])]	console.log(Array.from([1,2], x => x + x));	[2,4]
                替换	splice(index,1,'5')		Array.from('foo')	[f,o,o]
遍历	.map()	
        Array.from()		
                var friends = [
                    { name: ‘John’, age: 22 },
                    { name: ‘Peter’, age: 23 },
                    { name: ‘Mark’, age: 24 },
                    { name: ‘Maria’, age: 22 },
                    { name: ‘Monica’, age: 21 },
                    { name: ‘Martha’, age: 19 },
                ]
                Array.from(friends, ({name}) => name);	

清空	length =0	
数组转对象	...		var fruits = [“banana”, “apple”, “orange”, “watermelon”];
var fruitsObj = { …fruits };	returns {0: “banana”, 1: “apple”, 2: “orange”, 3: “watermelon”, 4: “apple”, 5: “orange”, 6: “grape”, 7: “apple”}	
对象转数组	Array.from(obj)	
填充数组	fill		new Array(10).fill(“1”)	returns [“1”, “1”, “1”, “1”, “1”, “1”, “1”, “1”, “1”, “1”, “1”]	
合并数组	concat()		food = […fruits, …meat, …vegetables];	
[...array1,...array2]	
两个数组的交集	includes()		 […new Set(numOne)].filter(item => numTwo.includes(item));	
去除假值		在JS中，假值有：false、0、''、null、NaN、undefined	var mixedArr = [0, 'blue', '', NaN, 9, true, undefined, 'white', false];
var trueArr = mixedArr.filter(Boolean);	
array.filter((item) => {return Boolean(item)})	
随机生产一个值		Math.random()*length	
倒序	reverse()	
排序	sort(fn)	fn(p1,p2):return function(a,b){                        if(a.p2 == b.p2){return a.p2 - b.p2}return a.p1 - b.p1}	
lastIndexOf()	返回 index	
求和	reduce()		nums.reduce((x, y) => x + y);	
2月21日	原型	prototype	这个属性 是一个指针，指向一个对象	这个对象 包含 所有实例共享的属性和方法，即这个原型对象是用来给实例共享属性和方法的。
而每个实例内部都有一个指向原型对象的指针。	
原型链	PersonB.prototype = Object.create(PersonA.prototype)	主要实现原理
PersonB.prototype = Object.create(PersonA.prototype)实现来继承PersonA的原型	通过new关键字实例化的对象身上就有了PersonB自身的属性和方法，也有了PersonA的原型方法
当实例化对象调用某个方法时会先在自身和原型上查找，然后是在_proto_上一层层查找，这种方式就是原型链	
闭包	函数嵌套函数，内部函数引用来外部函数的变量，从而导致来垃圾回收机制没有生效，	变量被保存来下来。
也就是所谓的内存泄漏，然后由于内存泄漏又会导致你项目逐渐变得卡顿等等问题。	因此要避免内存泄漏	
vuex	state：用一个对象就包含了全部的应用层级状态。


$store.state.n	
mutations：更改 Vuex 的 store 中的状态的唯一方法是提交 mutation	methods1(state,n){}		$store.commit('methods1',n)	
actions: action 提交的是 mutation，而不是直接变更状态。action 可以包含任意异步操作。	methods2(state,n){}	 const actions = {
    actionsAddCount(context, n = 0) {
        console.log(context)
        return context.commit('mutationsAddCount', n)
    },
    actionsReduceCount({ commit }, n = 0) {
        return commit('mutationsReduceCount', n)
    }
}	$store.dispatch('methods2',n)	
getters: 相当于Vue中的computed计算属性		getters: {
  list(state) {
   return state.list
  }
 },	 computed: {
    count(){
      return this.$store.getters.getterCount
    }
  }	
https://blog.csdn.net/qq_41614928/article/details/100051104、https://blog.csdn.net/qq_36503569/article/details/102402831	
Vue Router	<router-link>和<router-view>和<keep-alive>	
深拷贝	通过利用JSON.parse(JSON.stringify(Object))来达到深拷贝的目的	JSON.parse(JSON.stringify(Object)		但是JSON深拷贝的缺点是undefined和function还有symbol类型是无法进行深拷贝的	
浅拷贝：	1.ES6新特性Object.assign()     2.与扩展运算符来达到浅拷贝的目的	
生产环境和开发环境	
Vue通信	第一种：props和$emit


第二种：中央事件总线 EventBus(基本不用)	
第三种：vuex（状态管理器）	
第四种：$parent 和 $children
当然还有其他办法，但是基本不常用	$.refs.p  	通过$parent和$children就可以访问组件的实例,可以访问此组件的一切方法和data	要注意边界情况，如在#app上拿$parent得到的是new Vue()的实例，在这实例上再拿$parent得到的是undefined，而在最底层的子组件拿$children是个空数组。也要注意得到$parent和$children的值不一样，$children 的值是数组，而$parent是个对象	
Vue项目中	
1.new 实例化一个Class  想调用里面的函数，无效， 因为 没有正确对象--已实例化对象 上调用	
2.keep-alive  路由走 缓存--跳转scrolltop	
3.scrollTop(0,0)	
4.import 地址引错 提示install	
Vue项目中遇到视图不更新，方法不执行，埋点不触发等问题	
vue中数据改变，强制视图更新，视图不更新的原因和解决办法	obj	对象改变：oldObj = Object.assign({},newObj);	原理：对象是引用类型，vue不一定能监控到 所以当我们新建一个对象并赋值给oldObj字段的话，直接改变了它的指向地址	
vue.set	对象和数组都能用的	
this.$set(this,'oldArray',newArray);	
this.$set(this,'oldObj',newObj);	
this.$set(this.some.name,‘b’,2)	
array	push()，pop()，shift()，unshift()，splice()，sort()，reverse()可被vue检测到 ，filter(), concat(), slice() 。这些不会改变原始数组，但总是返回一个新数组。当使用非变异方法时，可以用新数组替换旧数组。
vue不能检测以下变动的数组：

① 当你利用索引直接设置一个项时，vm.items[indexOfItem] = newValue

② 当你修改数组的长度时，例如： vm.items.length = newLength
使用update	this.$forceUpdate()，强制视图更新 	vue多层循环，动态改变数据后渲染的很慢或者不渲染。	
异步更新队列	解决办法：可在数据变化之后立即使用 Vue.nextTick(callback) 。这样回调函数在 DOM 更新完成后就会调用。	
讲项目 要有关键字  从关键字上知道 你擅长什么	
技术笔试和技术面试时，重复率非常高，所以每次面试之后，一定要把问题记录和整理下来，一定	https://www.cnblogs.com/qianguyihao/p/8776837.html	https://github.com/qianguyihao/web	
续触发事件时	防抖动（Debouncing）	如果事件处理函数调用的频率无限制，会加重浏览器的负担	// 防抖
  var timer = null;

  function fandou(fucntion(){},time){
    if(timer){
       clearInterval(timer)
    }
    timer = setTimeout(fn,time)
  }
当持续触发事件时，一定时间段内没有再触发事件，事件处理函数才会执行一次，。	触发时候 有定时器 就清定时器 重新触发一个定时器	
节流阀（Throtting		function jieliu(fn,time){
    if(timer){
      return
    }
    timer = setTimeout(function(){
      clearInterval(timer)
      fn()
    },time) 
  }
保证一定时间段内只调用一次事件处理函数。	触发时候 有定时器 就返回	
如果 js 熟练，说明你是有技术深度的前端；如果 css 熟练，说明你是有经验的前端。	
https://github.com/qianguyihao/web	
https://www.cnblogs.com/qianguyihao/p/8776837.html	牛人	
浏览器输入url 到底干了什么	https://zhuanlan.zhihu.com/p/43369093	
DOMContentLoaded 	DOMContentLoaded 事件表示 DOM 树构建完毕，可以安全地访问 DOM 树所有 Node 节点、绑定事件等等	
load	load 事件表示所有资源都加载完毕，图片、背景、内容都已经完成渲染，页面处于可交互状态。	
react面试题	https://mp.weixin.qq.com/s/HoYBc9NxuBl2b3zaEjmKsQ	
Vue跨域	proxyTable: {
      '/api/a': {
        target: 'https://api.apiopen.top/', // 接口的域名
        secure: false,  // 如果是https接口，需要配置这个参数
        changeOrigin: true, // 如果接口跨域，需要进行这个参数配置
        pathRewrite: {
          '^/api/a': '/'
        }
      }
    },	
拦截器的使用	// http request 请求拦截器，有token值则配置上token值
axios.interceptors.request.use(
    config => {
        if (token) {  // 每次发送请求之前判断是否存在token，如果存在，则统一在http请求的header都加上token，不用每次请求都手动添加了
            config.headers.Authorization = token;
        }
        return config;
    },
    err => {
        return Promise.reject(err);
    });	
// http response 服务器响应拦截器，这里拦截401错误，并重新跳入登页重新获取token
axios.interceptors.response.use(
    response => {
        return response;
    },
    error => {
        if (error.response) {
            switch (error.response.status) {
                case 401:
                    // 这里写清除token的代码
                    router.replace({
                        path: 'login',
                        query: {redirect: router.currentRoute.fullPath}   //登录成功后跳入浏览的当前页面
                    })
            }
        }
        return Promise.reject(error.response.data)
    });	
react入门 	https://zh-hans.reactjs.org/tutorial/tutorial.html	
自动刷新	window.location.reload(true)	
axios参数传递	get:params:{}	
post:{}	
表达式	语句	https://www.cnblogs.com/qlqwjy/p/7660590.html	
正则表达式	https://www.jb51.net/tools/zhengze.html	
test 在字符串中检测模式匹配，返回true或false	
exec 该方法是专门为捕获组而设计的
功能：正则捕获的数据，一个数组；
参数：要应用模式匹配的字符串
特性：
使用全局标记g；持续查找所有匹配项并返回
不使用全局标记g；始终返回第一个匹配项信息
执行的过程
检测字符串参数，获取正则表达式匹配文本
找到匹配文本则返回一个数组
第0个元素：与整个模式匹配的字符串
其他元素：与捕获组匹配的字符串
否则返回null
派生属性
index 匹配项在字符串中的位置
input 应用正则表达式的字符串
length 返回数组元素的个数	字符串方法
match 找到一个或者多个正则表达式的匹配
replace 替换与正则表达式匹配的子串
search 检索与正则表达式匹配的值
split 把字符串分割为字符串数组	
hi	reg = /\bhi\b/	\b并不匹配这些单词分隔字符中的任何一个，它只匹配一个位置。	
hi后面不远处跟着一个Lucy	reg = /\bhi\b.*\bLuck\b/	.是另一个元字符，匹配除了换行符(\n)以外的任意字符	
先是一个单词hi,然后是任意个任意字符(但不能是换行)，最后是Lucy这个单词。	*(数量)——任意数量的不包含换行(\n)的字符	
https://www.jb51.net/tools/zhengze.html 待续	
. 匹配除换行符以外的任意字符
\w 匹配字母或数字或下划线或汉字
\s 匹配任意的空白符
\d 匹配数字
\b 匹配单词的开始或结束
^ 匹配字符串的开始
$ 匹配字符串的结束		\s匹配任意的空白符，包括空格，制表符(Tab)，换行符，中文全角空格等	\s：空白字符（包含：空格符，制表符，回车符，换行符，垂直换行符，换页符）
\S:非空白字符
\n：换行符
\r：回车符
\b:单词边界
\B:非单词边界
\t：制表符
 . ：表示除了\r\n外的所有字符
量词（以下n为代表数量的词）
n+：可以出现1到无数次	
你应该使用\.和\*。当然，要查找\本身，你也得用\\	\[a-z]{1,}\\\.[a-z]{2,3}\	
字符转义 \	
* 重复零次或更多次
+ 重复一次或更多次
? 重复零次或一次
{n} 重复n次
{n,} 重复n次或更多次
{n,m} 重复n到m次		只不过{2}匹配只能刚好重复2次，{5,12}则是重复的次数不能少于5次，不能多于12次，否则都不匹配。	
在方括号[]里列出它们就行		[aeiou]就匹配任何一个英文元音字母，[.?!]匹配标点符号(.或?或!)	
\(?0\d{2}[) -]?\d{8}	
匹配 (010)88886666，或022-22334455，或02912345678等	
反义	\W 匹配任意不是字母，数字，下划线，汉字的字符
\S 匹配任意不是空白符的字符
\D 匹配任意非数字的字符
\B 匹配不是单词开头或结束的位置
[^x] 匹配除了x以外的任意字符
[^aeiou] 匹配除了aeiou这几个字母以外的任意字符	\S+匹配不包含空白符的字符串。

<a[^>]+>匹配用尖括号括起来的以a开头的字符串。	/a[^>]+/g.exec('<askokos>k>')               ["askokos", index: 1, input: "<askokos>k>", groups: undefined]	
分枝条件	用|把不同的规则分隔开	var reg4 = /\d{5}-\d{4}|\d{5}/
console.log(reg4.exec('12123-565'))	((2[0-4]\d|25[0-5]|[01]?\d\d?)\.){3}(2[0-4]\d|25[0-5]|[01]?\d\d?)。	
将会从左到右地测试每个条件，如果满足了某个分枝的话，就不会去再管其它的条件了。	var reg5 = /\d{5}| \d{5}-\d{4}/
console.log(reg5.exec('12123-565'))	
分组	用小括号来指定子表达式，可以指定这个子表达式的重复次数	(\d{1,3}\.){3}\d{1,3}是一个简单的IP地址匹配表达式。要理解这个表达式，请按下列顺序分析它：\d{1,3}匹配1到3位的数字，(\d{1,3}\.){3}匹配三位数字加上一个英文句号(这个整体也就是这个分组)重复3次，最后再加上一个一到三位的数字(\d{1,3})。	
后向引用	一个更复杂的例子：(?<=<(\w+)>).*(?=<\/\1>)	匹配不包含属性的简单HTML标签内里的内容。(?<=<(\w+)>)指定了这样的前缀：被尖括号括起来的单词(比如可能是<b>)，然后是.*(任意的字符串),最后是一个后缀(?=<\/\1>)。注意后缀里的\/，它用到了前面提过的字符转义；\1则是一个反向引用，引用的正是捕获的第一组，前面的(\w+)匹配的内容，这样如果前缀实际上是<b>的话，后缀就是</b>了。整个表达式匹配的是<b>和</b>之间的内容(再次提醒，不包括前缀和后缀本身)。		参悟  https://blog.csdn.net/bombas/article/details/80790274
零宽断言	查找在某些内容(但并不包括这些内容)之前或之后的东西，也就是说它们像\b,^,$那样用于指定一个位置，这个位置应该满足一定的条件(即断言)	(?=exp)	\b\w+(?=ing\b)，匹配以ing结尾的单词的前面部分(除了ing以外的部分)，如查找I'm singing while you're dancing.时，它会匹配sing和danc。	
(?<=\s)\d+(?=\s)匹配以空白符间隔的数字(再次强调，不包括这些空白符)。	(?<=exp)	(?<=\bre)\w+\b会匹配以re开头的单词的后半部分(除了re以外的部分)，例如在查找reading a book时，它匹配ading。	
((?<=\d)\d{3})+\b，用它对1234567890进行查找时结果是234567890。	
(?!exp)	\d{3}(?!\d)匹配三位数字，而且这三位数字的后面不能是数字；\b((?!abc)\w)+\b匹配不包含连续字符串abc的单词。	
(?<!exp)	(?<![a-z])\d{7}匹配前面不是小写字母的七位数字。	
(?#comment)	2[0-4]\d(?#200-249)|25[0-5](?#250-255)|[01]?\d\d?(?#0-199)。	
注释	
贪婪与懒惰	*? 重复任意次，但尽可能少重复
+? 重复1次或更多次，但尽可能少重复
?? 重复0次或1次，但尽可能少重复
{n,m}? 重复n到m次，但尽可能少重复
{n,}? 重复n次以上，但尽可能少重复	
width	content	
offsetWidth	width+padding+border	
clientWidth	width+padding	
offsetLeft	
 	
https://www.ruanyifeng.com/blog/2018/07/json_web_token-tutorial.html	
http://www.jq22.com/demo/jquery-guaguaka-150106220841/	
一、clientX、clientY
点击位置距离当前body可视区域的x，y坐标

二、pageX、pageY
对于整个页面来说，包括了被卷去的body部分的长度

三、screenX、screenY
点击位置距离当前电脑屏幕的x，y坐标

四、offsetX、offsetY
相对于带有定位的父盒子的x，y坐标

五、x、y
和screenX、screenY一样
https://www.w3school.com.cn/tags/canvas_globalcomposit	context.globalCompositeOperation="source-in";	source-over 默认。在目标图像上显示源图像。
<script>

var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");


ctx.fillStyle="green"; (目标图像 destination)
ctx.fillRect(150,20,75,50);

ctx.fillStyle="#ccc"; (源图像 source)
ctx.globalCompositeOperation="xor";
ctx.fillRect(180,50,75,50);

</script>	source-atop 在目标图像顶部显示源图像。源图像位于目标图像之外的部分是不可见的。	
source-in 在目标图像中显示源图像。只有目标图像内的源图像部分会显示，目标图像是透明的。	
source-out 在目标图像之外显示源图像。只会显示目标图像之外源图像部分，目标图像是透明的。	
destination-over 在源图像上方显示目标图像	
destination-atop 在源图像顶部显示目标图像。源图像之外的目标图像部分不会被显示。	
destination-in 在源图像中显示目标图像。只有源图像内的目标图像部分会被显示，源图像是透明的	
destination-out 在源图像外显示目标图像。只有源图像外的目标图像部分会被显示，源图像是透明的	
lighter 显示源图像 + 目标图像	
copy 显示源图像。忽略目标图像	
xor 使用异或操作对源图像与目标图像进行组合	
https://github.com/XmanLin/MyUtils/blob/master/util/util.js	
https://juejin.im/post/5e6ed2fff265da57671bdbd2?utm_source=gold_browser_extension	
nuxt.js	
https://www.cnblogs.com/zr123/p/10660296.html	
https://segmentfault.com/a/1190000020149370	
https://webpack.js.org/concepts/	
https://www.iconfont.cn/	
https://www.cnblogs.com/iamlhr/p/11459653.html	array1.sort();array1.sort(sort1)	
数组排序	function sort1(a,b){return a-b}	
function sort2(prop1){                                           return function(a,b){                            return a.prop1 - b.prop1}                                }	
function sort3(file1,file2){  return function(){  if(a.file1 == b.file1){return a.file2 - b.file2} return a.file1 -b.file1                 }}	
主攻+其他技	
相关书	代码大全、程序员修炼之道、编程珠玑、代码整洁之道	
editor	熟悉ide每个细节 快捷键 特性	
Git	PRO GIT	
精通框架重构	重构：改善既有代码的设计	
TDD测试	
命令行	shell 命令行 conquering the command line	
Github 分享	每周一次	
Unicode 字符串的编码和解码	escape	var s = "JavaScript 中国";
s = escape(s);  //Unicode编码
console.log(s);  //返回字符串“JavaScript%u4E2D%u56FD”
s = unescape(s);  //Unicode解码
console.log(s);  //返回字符串“JavaScript 中国”	
unescape	
encodeURI	var s = "c.biancheng.net/navi/search.asp?keyword=URI";
a = encodeURI(s);
console.log(a);
b = encodeURICompoent(s);
console.log(b);	
encodeURICompoent	
输出显示为：
c.biancheng.net/navi/search.asp?keyword=URI
c.biancheng.net%2Fnavi%2Fsearch.asp%3Fkeyword%3DURI	
iframe找元素	// 在标签上添加onload事件
<iframe id="ifra" onload="getIframe()"  name="myifra" src="iframe2.html" width="400" height="400"></iframe>

// 原生js获取
function getIframe() {
 var ifra = document.getElementById("ifra");
 console.log(ifra.contentWindow.document.getElementById("btn"));
}

// jquery获取

function getIframe() {
 console.log($('#ifra').contents().find("#btn")[0]);
}	
子页面调用父页面方法	// 先通过window.parent获取到父元素，在调用该对象上的方法

window.parent.sayHello();

// 或者jquery

$(window.parent)[0].sayHello();	
父页面调用子页面方法	// 先获取到子页面的window对象，然后在调用
window.onload = function() {
 var ifra = document.getElementById("ifra");
 ifra.contentWindow.sayName();
}	
