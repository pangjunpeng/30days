+ [1. sleep函数](#sleep)
+ [2. 异步与定时器](#exectime)
+ [3. obj.obj === obj](#obj)
+ [4. fn() === fn;fn.fn===fn](#function1)
+ [5. fn() // 'a'; fn()() // 'b'](#function2)
+ [6. fn()==='a'; fn()()==='b'](#function3)
+ [7. promise](#promise)
+ [8. 数组排序byField](#byfield)
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
### promise
**小明成绩不好，每次考试都靠瞎。小明的老师对他说：“小明，如果考不到60分你继续考，直到考到60分，我实现你的愿望让你和凯丽坐到一起”**
```
function exam() {
  var score = Math.floor(Math.random() * 101)
  if (score >= 60) {
    console.log('及格，和凯丽坐到一起')
  } else {
    console.log('不及格，继续考试')
    setTimeout(exam, 1000)
  }
}
exam()
```
对上述代码使用 Promise 改写，能用以下方式调用
```
exam().then(score => {
  console.log('及格，和凯丽坐到一起', score)
})
```
### 解
1. 没有用到延时1秒，pass
```
function exam(){
	return new Promise((resolve, reject) => {
    var score = Math.floor(Math.random() * 101)
    while(score < 60){
      console.log('不及格，继续考试')
      score = Math.floor(Math.random() * 101)
    }
    resolve(score)
	})
}
```
2. 
```
function exam(){
	return new Promise((resolve, reject) => {
		function _exam(){
      var score = Math.floor(Math.random() * 101)
      if (score >= 60) {
          resolve(score)
      } else {
          console.log('不及格，继续考试')
          setTimeout(_exam, 1000)
      }
		}
		_exam()
	})
}
```
3. 
```
function exam(){
	return new Promise((resolve, reject) => {
    var score = Math.floor(Math.random() * 101)
    if (score >= 60) {
      resolve(score)
    } else {
      console.log('不及格，继续考试')
      setTimeout(() => { resolve(exam()) }, 1000)
    }
	})
}
```
### byField
**写一个 byField 函数，实现数组按姓名、年纪任意字段排序**
```
var users = [
  { name: 'John', age: 20, company: 'Baidu' },
  { name: 'Pete', age: 18, company: 'Alibaba' },
  { name: 'Ann', age: 19, company: 'Tencent' }
];

users.sort(byField('company'))
// 输出
/*
[
  { name: 'Pete', age: 18, company: 'Alibaba' },
  { name: 'John', age: 20, company: 'Baidu' },
  { name: 'Ann', age: 19, company: 'Tencent' }
];
*/
users.sort(byField('name'))
// 输出
/*
[
  { name: 'Ann', age: 19, company: 'Tencent' },
  { name: 'John', age: 20, company: 'Baidu' },
  { name: 'Pete', age: 18, company: 'Alibaba' },
];
*/
```
### 解
待续
