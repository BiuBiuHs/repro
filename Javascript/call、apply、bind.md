### bind 返回一个新的函数，不立即执行。
例如：react中，改变函数指向

### apply, call。立即执行
```javascript
fn.call(isThis, arg1, arg2, ....)

fn.apply(isThis, [arg1, arg2, ....])

apply 接收一个数组参数，call 直接接收参数
apply 的性能会比call差，因为要对数组参数进行判断和解构
```

### 实现bind

```
Function.prototype.bind=function(obj){
  let self= this;
   // 获取bind函数从第二个参数到最后一个参数
    var args = Array.prototype.slice.call(arguments, 1);
    
  //bind最终返回一个可执行函数 因此 此处返回 一个function
  return function(){
  
  // 这个时候的arguments是指bind返回的函数传入的参数
   var bindArgs = Array.prototype.slice.call(arguments);
  
      //self就指向 bind 的那个函数 func.bind  self=> func
      let args=Array.prototype.slice.call(argument,1)
               self.apply(obj,args.concat(bindArgs))
  }
}
```
