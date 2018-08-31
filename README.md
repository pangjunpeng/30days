+ [sleep函数](#sleep)
+ [异步与定时器](#exectime)
+ [obj.obj === obj](#obj)
+ [fn() === fn;fn.fn===fn](#function1)
+ [fn() // 'a'; fn()() // 'b'](#function2)
+ [fn()==='a'; fn()()==='b'](#function3)
## Sleep
**1. 写一个 `execTime` 函数，要求如下**
+ 参数：时间毫秒数
+ 作用：什么都不做，但函数执行消耗的时间为参数传递的毫秒数
```javascript
function execTime(t) {
  // 补全代码
}
console.log(1) // print 1
execTime(3000) // execute cost 3s
console.log(2) // print 2
```
### 解：
```javascript
function execTime(t){
  var now = new Date()
  while(new Date() - now < t){}
}
```  
## execTime
**2. 写一个 execTime 函数，要求**
+ 参数 t：时间毫秒数
+ 参数 callback：回调函数
```javascript
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
```javascript
function execTime(t, fn){
  setTimeout(fn, t)
}
```
## obj
**3. 创建一个对象 obj，使得 obj.obj.obj.obj.obj === obj，即，不管出现多少次 .obj，都得到 obj**
### 解
```javascript
obj = {}
obj.obj = obj
```
或
```javascript
obj = {
  get obj(){
    return this
  }
}
```
## function1
**4. 写出一个函数 fn，使得 fn 满足以下条件：**
+ fn() === fn
+ fn.fn === fn
### 解
```javascript
function fn(){
  return fn
}
fn.fn = fn //函数本身也是对象，也可以设置属性
```
## function2
**5. 写一个函数 fn，使得 fn 满足一下条件：**
+ fn() 打印出 'a'
+ fn()() 打印出 'b'
+ fn()()() 打印出 'c'
### 解
```javascript
function fn(){
  var timer = setTimeout(() => {
    console.log('a')
  })
  return function (){
    clearTimeout(timer)
    timer = setTimeout(() => {
      console.log('b')
    })
    return function (){
      clearTimeout(timer)
      timer = setTimeout(() => {
        console.log('c')
      })
    }
  }
}
```
完美版
```javascript
function fn(){
  var str = 'a'
  setTimeout(() => {
    console.log(str)
  })
  return function (){
    str = 'b'
    return function (){
      str = 'c'
    }
  }
}
```
## function3
**4. 写出一个函数 fn，使得 fn 满足以下条件：**
+ fn() == 'a'
+ fn()() == 'b'
+ fn()()() == 'c'
### 解
```javascript
function fn(){
  return a
}
function a(){
  return b
}
a.toString = function(){
  return 'a'
}
function b(){
  return 'c'
}
b.toString = function(){
  return 'b'
}
```
