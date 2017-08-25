Vue移动端项目总结

使用Vue项目写了一个移动端项目，然后又把项目硬生生的抽离了组件，一直忙着写RN项目没有时间总结心得，今天上午终于下定决心，写点总结。

1、position:absolute： 定位的时候不同手机的浏览器版本不一样，存在兼容性问题，所以要修改为fixed,然后使用left: calc(50% - 1rem )进行定位；

2、event.touches[0].pageY：移动端事件touchstart,touchmove,touchend,在vue中的手指滑动的对象是要传入$event才可以使用event.touches[0].pageY等值；

3、返回顶部：根据touchend事件判断document.body.scrollTop的值是否大于1000来控制返回顶部按钮的显示和隐藏；

4、弹窗定位: postion: absolute; left: 50%; top: 50%; margin-top: -height/2; margin-left: -width/2；

5、localstorage：存储对象的时候存储的是字符串JSON.stringify()，取的时候是对象( JSON.parse() )；

6、@input： 实时监听input中的值的时候，focus和blur都不能满足需求的时候可以使用input事件；

7、分享组件: (1)<a href="http://service.weibo.com/share/share.php?appkey=&title=&url=&searchPic=false&style=simple" target="_blank"><img src="/static/weibo.png" alt="wechat">分享到微博</a>；

8、左右滑动效果：的时候可以使用overflow-x:auto,但是在苹果手机上会有问题，解决兼容的方法是:-webkit-overflow-scrolling: touch；

9、移动端使用百度分享的时候: 

created(){

window._bd_share_main && window._bd_share_main.init()
},
mounted(){
window._bd_share_main && window._bd_share_main.init()
},

否则百度分享会出现点击两次才出现分享按钮，同时在index.html做出相应的配置；

10、异步渲染： 在vue项目中的有时候由于异步的原因导致dom渲染问题，获取不到对应的节点，在使用this.$nextTick无效的情况，可以使用 setTimeout等待dom加载完成之后执行函数，不过不推荐，会有性能问题；

11、移动端H5实现上传图片:  http://javascript.ruanyifeng.com/htmlapi/file.html#toc0，推荐看一下这个，使用H5 API中的readAsDataURL，获取图片返回的base64编码data-uri对象。，然后去请求后台的返回图片路径，在处理图片显示的时候，会有两种选择: (1)不请求后台，直接渲染图片(2)base64请求后台，渲染图片，还有就是删除的时候要保持和数据库同步；

12、移动端不支持select，自己div模拟select下拉效果；

13、请求传参： 传递参数的时候是包含#的url的时候，后台可能不识别#，需要编码的可以使用encodeURI(),encodeURIComponent()；

14、Hybrid: 和原生交互的时候，给IOS传递参数的时候，使用 window.location.href = "next://";那么IOS就可以接受到next这个参数；

15、导航钩子：判断离开一个路由的时候执行一个方法route1.beforeEach((to, from, next) => {

if( from.path == '/theme_detail' ){
console.log( 88888 )
}
next()
})；

 export default route1

16、iphone5s不兼容display:flex：处理方法: display:-webkit-flex;-webkit-box; flex:1; -webkit-flex: 1;-webkit-box-flex:1;

17、原生和IOS交互的时候，IOS使用第三方库WebViewJavascriptBridge，原生调用js方法，在js中的时候使用方法: 一个js文件全局配置const BridgeMixin = {

methods: {
setupWebViewJavascriptBridge(callback) {
if (window.WebViewJavascriptBridge) { return callback(WebViewJavascriptBridge); }
if (window.WVJBCallbacks) { return window.WVJBCallbacks.push(callback); }
window.WVJBCallbacks = [callback];
var WVJBIframe = document.createElement('iframe');
WVJBIframe.style.display = 'none';
WVJBIframe.src = 'https://__bridge_loaded__';
document.documentElement.appendChild(WVJBIframe);
setTimeout(function() { document.documentElement.removeChild(WVJBIframe) }, 0)
}
}
}
export {
BridgeMixin
}，然后在调用的页面， this.setupWebViewJavascriptBridge(function(bridge){
bridge.registerHandler('testJavascriptHandler', function(data, responseCallback) {
var responseData = { 'Javascript Says':'Right back atcha!' }
alert( data )
responseCallback(responseData)
}；

18、当数据多的时候可以使用路由外面裹一层keep-alive，要加载router-view中，这样再次进入这个路由的时候就不会重新加载了，比如进入页面看到14行了，然后点击进入下一个页面，返回的时候直接定位是14行；

19、原生js实现滚动到顶部 

//document.body.scrollTop获取chrome等浏览器的scrollTop，document.documentElement.scrollTop获取IE浏览器的scrollTop
let x = document.body.scrollTop || document.documentElement.scrollTop;
let timer = setInterval(function(){
x = x - 10;
if( x < 100 )
{
x = 0;
window.scrollTo(x,x);
clearInterval(timer);
}
window.scrollTo( x, x );
},"10");

20、如何把build的项目在本地跑起来，把config下面的index.js中的assetsPublicPath的都改为./

21、地址栏添加icon的时候因为是用的是webpack打包的所以这个icon要放在static文件下；

22、如何给网站添加站标： 在线生成ico站标，一般是16*16，将制作好的站标命名为favicon.ico，放在项目根目录，然后在首页的<head></head>标签内添加

<link rel="shortcut icon" href="/favicon.ico" />

<link rel="bookmark"href="/favicon.ico" />

23、在自定义组件中使用这些受限制的元素时会导致一些问题，例如：

<table>
<my-row>...</my-row>
</table>
自定义组件 <my-row> 被认为是无效的内容，因此在渲染的时候会导致错误。 变通的方案是使用特殊的 is 属性：
<table>
<tr is="my-row"></tr>
</table>

24、vue设置请求头的时候：

Vue.http.interceptors.push((request, next) =>{
request.headers.set('loginCode', this.loginCode);
next((response) => {
return response
});
});

25、插件开发: 声明插件-> 写插件-> 注册插件 —> 使用插件

26、Vue.mixin({//这里的代码会在每个组件（包括根组件）的created执行之前 执行

created: function () {
console.log("组件开始加载")
}
}),也就是这个的代码的执行循序是在created方法之前的；

27、假如是写给例如methods属性的某个方法,组件里若本身有test方法,并不会先执行插件的test方法,再执行组件的test方法,而是只执行其中一个,并且优先执行组件本身的同名方法.这点需要注意

28、想获取子组件的值是通过自定义事件获取的，子组件this.$emit(eventName, params),父组件监听事件获取参数v-on:eventName=eventName,eventName(params){console.log(params)}，

附：

vue2.0相关文档
http://vuefe.cn/ 中文文档

http://vuejs.org/guide/ 官网原文文档

http://router.vuejs.org/zh-cn/index.html vue-router2.0中文文档

http://vuex.vuejs.org/en/index.html vuex2.0 英文文档

https://github.com/bhnddowinf/vuejs2-learn v2学习项目

