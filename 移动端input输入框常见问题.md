### 获得焦点时，光标消失或错位：

-webkit-user-select:none 导致 input 框在 iOS 中无法输入，光标不出现，设置如下
```
user-select: text;
-webkit-user-select: text;
```
利用scrollIntoView 使当前元素出现到指定位置，避免光标错位，设置如下：
```
e.target.scrollIntoView(true);  
e.target.scrollIntoViewIfNeeded();
```

### 输入框获得焦点可弹出软键盘，却没有光标闪烁，也无法正常输入。

-webkit-user-select:none 导致的，可以这样解决
```
*:not(input,textarea) {
   -webkit-touch-callout: none;
   -webkit-user-select: none;
}
```
### input 自定义样式

```
// 使用伪类
input::-webkit-input-placeholder,
input::-moz-placeholder,
input::-ms-input-placeholder {
 ...style
 text-align: center;
}
```

### ios的wkWebview下 输入框获取焦点后，页面正题网上顶（这没毛病）， 尴尬的是失去焦点后页面不回弹了，顶部上移了，底部留有一截灰色区域，需要手动随意触摸一个地方。才会回弹。

解决方法：监听软键盘弹起、关闭事件，在进行对应的操作
```
mounted () {// 软键盘关闭事件   可在全局的地方  vue的话比如App.vue 文件里添加以下代码
    document.body.addEventListener('focusout', () => {
      // 回到原点  若觉得一瞬间回到底部不够炫酷，那自己可以自定义缓慢回弹效果， 可用css 、贝塞尔曲线、js的 requestAnimationFrame  等等 方法 实现体验性更好的回弹效果
      window.scrollTo({ top: 0, left: 0, behavior: 'smooth' })
    })
}
```
