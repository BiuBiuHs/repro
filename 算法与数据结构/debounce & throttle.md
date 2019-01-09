### 函数节流 throttle

用于scroll，resize节流，页面滚动频繁触发会导致性能问题

```javascript
var throttle = function(func, wait) {
    var timeout;
    
    return function() {
       
        if(!timeout) {   //存在timer不执行
            timeout = setTimeout(function() {
                timeout = null;
                func();
            }, wait);
        }
    }
}
```

### 函数防抖 debounce

用于输入框，一段时间不输入后进行搜索

```javascript
var debounce = function(func, wait) {
    var timeout;

    return function() {
        clearTimeout(timeout);
        timeout = setTimeout(function() {
            func();
        }, wait);
    }
}
```
