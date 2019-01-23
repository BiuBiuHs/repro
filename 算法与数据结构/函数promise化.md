### 函数promise化

####  1.单一函数对promise进行封装

```
// 如对fs的异步读取文件函数封装promise
// 返回一个promise 同时针对回调的不同参数返回不同的处理结果，方便之后调用

var promisify = function(fpath, encoding){
    return new Promise(function(resolve, reject){
        fs.readFile(fpath, encoding, function(err, result){
            if(err) return reject(err)
            else return resolve(result)
        })
    })
}
```

####  2.函数一般化
 也就是将一般的函数进行promise化
 
```
var promisify = function (method, ctx) {
    return function () {
        // 获取method调用的需要参数
        var args = Array.prototype.slice.call(arguments, 0);
                
        // use runtime this if ctx not provided
        ctx = ctx || this;

        //返回一个新的Promise对象
        return new Promise(function (resolve, reject) {
            // 除了函数传入的参数以外还需要一个callback函数来供异步方法调用
            var callback = function () {
                return function (err, result) {
                    if (err) {
                        return reject(err);
                    }
                    return resolve(result);
                };
            }
            args.push(callback());
            // 调用method
            method.apply(ctx, args);
        });
    };
};

// 调用
var readFileAsync = promisify(fs.readFile)
readFileAsync('./test.txt', 'utf8').then(function(data){ 
  console.log(data) 
})
```
