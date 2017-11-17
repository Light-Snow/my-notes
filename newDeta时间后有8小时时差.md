#### new Date() 中传入的参数的参数中不能识别‘-’，‘T’,所以需要转化一下，兼容性函数如下：
```
function fixDate(strTime) {
    if (!strTime) {
      return '';
    }
    var tempDate = new Date(strTime+'+0800');
    if(tempDate=='Invalid Date'){
        strTime = strTime.replace(/T/g,' ');
        strTime = strTime.replace(/-/g,'/');
        tempDate=new Date(strTime+'+0800');
    }
    tempDate.toLocaleDateString();
    return tempDate;
  }
```
