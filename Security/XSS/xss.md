## 为什么叫XSS
- Cross Site Script，但是CSS已经被使用了
- 指运行了外部的注入的脚本

## 防御方法： 防御html内容注入，转义html实体
```js
var escapeHtml = function(str) {
    if(!str) return '';
    str = str.replace(/</g,'&lt;'); // 替换左尖括号 
    str = str.replace(/>/g,'&gt;'); // 替换右尖括号
    return str;
}
```

## 防御方法： 防御html属性注入，转义html实体
```js
var escapeHtmlProperty = function(str) {
    if(!str) return '';
    str = str.replace(/"/g,'&quto;'); // 替换双引号
    str = str.replace(/'/g,'&#39;'); // 替换单引号
    str = str.replace(/ /g,'&#32;'); // 替换空格
    return str;
}
```
上面2个函数可以合并为一个
