- [写一个 `execTime` 函数，要求如下](#Sleep)


### Sleep
1. 写一个 `execTime` 函数，要求如下
+ 参数：时间毫秒数
+ 作用：什么都不做，但函数执行消耗的时间为参数传递的毫秒数
```
function execTime(t) {
  // 补全代码
}
console.log(1) // print 1
execTime(3000) // execute cost 3s
console.log(2) // print 2
```
### 解：
```
function execTime(t){
  var now = new Date()
  while(new Date() - now < t){}
}
```  
### 2. 写一个 execTime 函数，要求
+ 参数 t：时间毫秒数
+ 参数 callback：回调函数
```
function execTime(t, callback) {
  // some code
}
console.log(1)
execTime(3000, function(){
  console.log(3)
})
console.log(2)
```
执行结果为：立即输出1和2，3秒后输出3 
### 解：
```
function execTime(t, fn){
  setTimeout(fn, t)
}
```
