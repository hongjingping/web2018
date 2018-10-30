## 1. 变量
1. 在ES6之前，变量声明关键字是var
    1. var的缺点: 
        1. var可以多次声明同一个变量
        2. var会造成变量名提升
2. ES6变量声明关键字：let变量声明；const常量声明；解决了var前面提到的两个缺点。let和const都是块级作用域。
3. 块级作用域？在一个函数内部，在一个代码块内部
  ```
  for (var a = 0; a < 3; a++>) {
   setTimeout(function () {
    console.log(a);
   }, 1000)
  } 
  // 输出结果为3
  <!-- 如何将结果输出为0，1，2 -->
  <!-- es5 -->
  for(var a = 0; a < 3; a++>){
    (function (a) {
      setTimeout(function () {
        console.log(a)
      }, 1000)
    })(a)
  } // 输出结果为0，1，2
  <!-- es6 -->
  for (let a = 0; a < 3; a ++) {
    setTimeout(function () {
      console.log(a)
    }, 1000)
  } //输出结果为0，1，2
  ```

## 2. 函数(箭头函数)
1. 不需要function关键字来创建函数
```
<!-- ES5 -->
var aa = function () {}
<!-- ES6 -->
var aa = () => {}
```
2. 可以极大地简写函数,简写规则: 当函数所有参数只有1个的时候，可以去掉`()`;当函数体中只返回值，而没有其他操作时候，可以去掉`{}`。
```
<!-- es5 -->
var fn = function (a) {
  return a + 5
}
<!-- es6 -->
var fn = a => a + 5
```
3. 继承上下文的关键字this
```
<!-- ES5 -->
var fn = function () {

}
fn.bind(this)
<!-- ES6 -->
var fn = () => {} 
```
## 3. 数组
1. 新增常用的4个方法
    1. map-映射，一个由原数组中的每个元素调用一个指定方法后的返回值组成的新数组。
    ```
    let arr = [6, 5, 4];
    let result = arr.map(item => {
      if (item >= 6) {
        return '优'
      } else {
        return '良'
      }
    })
    <!-- result:['优', '良', '良'] -->
    ```
    2. reduce-汇总
    ```
    let arr = [1,2,3,4,5,6,7]
    let result = arr.reduce((tmp, item, index) => {
      console.log(tmp, item, index);
      return tmp + item;
    })
    console.log(result)
    ```
    3. filter-过滤，使用指定的函数测试所有元素，并创建一个包含所有通过测试的元素的新数组。
    ```
    let arr = [
      { title: '电脑'， price: 30},
      { title: '手机'， price: 20},
      { title: '键盘'， price: 10},
      { title: '鼠标'， price: 5},
    ]

    let result = arr.filter(json => json.price >= 10)
    conosle.log(result)
    ```
    4. forEach-迭代，为每个元素执行对应的方法
    ```
    let arr = [1,2,3,4,5]
    arr.forEach((item, index) => {
      console.log(index+':'+item)
    })
    ```
    5. every()-测试数组中的所有元素是否都通过了指定函数的测试
    ```
    var a = [1,2,3,4,5,6,7,8]
    var b = a.every(item => {
      return item > 4
    })
    var c = a.every(item => {
      return item > 0
    })
    console.log(b); // false
    console.log(c); // true
    ```
    6. 展开运算符-允许一个表达式在某处展开，常用的场景包括:函数参数，数组元素，解构赋值。
        1. 解构赋值语法是一个js表达式，它使得从数组或对象中提取数据赋值给不同的变量变为可能。
        ```
        var a = [1,2,3,4,5]
        var [b, c] = a;
        console.log(b); // 1
        console.log(c); // 2

        function fun(...a) {
          console.log(a); // [1,2,3]
        }
        fun(1,2,3); // 传入1,2,3参数,...a为数组[1,2,3]

        function gun({a, b}) {
          return a+b
        }
        console.log(gun({a:2, b:1})); // 3
        ```

## 4. 函数的参数
1. 收集参数
```
function show(a, b, ...args) {
  console.log(args);
}
show(1,2,3,4,5,6,7,8)
```
2. 展开数组
```
const arr1 = [1,2,3]
const arr2 = [4,5,6]
console.log([...arr1, ...arr2]); // [1,2,3,4,5,6]
console.log(...arr1); // 1,2,3
```
3. 默认值
```
const show = (a=666, b=999) => {
  console.log(a); // 666
  console.log(b); // 999
}
show()
```
## 5. 解构赋值
1. 左右两边结构必须一样;
2. 右边必须是合法的值;
3. 声明和赋值不能分开(必须在一句话里面完成);
```
let [a,b,c] = [1,2,999];
let {e, d, g} = {e:4, d:5, g:8};
console.log(a,b,c,e,d,g)
```
## 6. 字符串
1. 多了两个新方法: startWith,endsWith
```
<!-- startsWith -->
let str='https//http://mp.blog.csdn.net/postedit/79478118';

if(str.startsWith('http://')){
  alert('普通网址');
}else if(str.startsWith('https://')){
  alert('加密网址');
}else if(str.startsWith('git://')){
  alert('git地址');
}else if(str.startsWith('svn://')){
  alert('svn地址');
}else{
  alert('其他');
}
<!-- endsWith -->
let str='12121.png';
 
if(str.endsWith('.txt')){
  alert('文本文件');
}else if(str.endsWith('.jpg')){
  alert('JPG图片');
}else{
  alert('其他');
}
```
2. 字符串模板，方便字符串拼接，可以折行
```
let title='标题';
let content='内容';
let str='<div>\
  <h1>'+title+'</h1>\
  <p>'+content+'</p>\
</div>';
 
let str2=`<div>
  <h1>${title}</h1>
  <p>${content}</p>
</div>`;
```
## 7. 面向对象
<!-- ES5类以及类的继承 -->
```
// 父类
function User(name, age) {
  this.name = name;
  this.age = age;
}

User.prototype.printUserInfo = function () {
  console.log(`${this.name}:${this.age}`)
}

// 子类
function VipUser (name, age, level) {
  User.call(this, name, age)
  this.level = level;
}
VipUser.prototype = new User();
VipUser.prototype.constructor = VipUser;

VipUser.prototype.printLevel = function () {
  console.log(`${this.level}`)
}

const class1 = new VipUser('barret', 25, 999)
class1.printUserInfo()
class1.printLevel()
```
<!-- ES6类以及类的继承 -->
```
// 父类
class User {
  constructor (name, age) {
    this.name = name;
    this.age = age;
  }
  printUserInfo () {
    console.log(`${this.name}:${this.age}`)
  }
}

// 子类
class VipUser extends User {
  constructor (name, age, level) {
    super(name, age)

    this.level = level
  }

  printLevel () {
    console.log(`${this.level}`)
  }
}

const class1 = new VipUser('barret', 25, 999);
class1.printUserInfo();
class1.printLevel();
```
2. ES6较ES5的优点: 区别于函数，更加专业化；写法更简单，更容易实现类的继承
## 8. promise
1. ajax与promise并联请求比较
```
// ajax 各个请求并联请求
const ajaxData = () => {
  $.ajax({
    url: './user.json',
    dataType: 'json',
    success: (res) => {
      console.log(res)
    }
  })

  $.ajax({
    url: './user1.json',
    success: (res) => {
      console.log(res)
    }
  })
}
ajaxData();

// promise 各个请求并联请求，相比较于ajax，，更加便于数据统一管理
const promiseData = function () {
  const p1 = new Promise((resolve, reject) => {
    $.ajax({
      url: './user.json',
      dataType: 'json',
      success (res) {
        console.log(res)
      },
      err (err) {
        console.log(err)
      }
    })
  })

  const p2 = new Promise(function (resolve, reject) {
    $.ajax({
      url: './user1.json',
      success(res) {
        resolve()
      },
      err(err) {
        reject(err)
      }
    })
  })

  Promise.all([p1, p2]).then((arr) => {
    console.log(arr)
  }, (errArr) => {
    console.log(errArr)
  })
}
promiseData()
```
2. ajax与promise串联请求比较
```
// ajax 串联请求，下一次请求依赖于上一次请求，如果依赖性比较多嵌入会很多，维护起来会很复杂
const ajaxData = function () {
  $.ajax({
    url: './user.json',
    dataType: 'json',
    success: (res) => {
      console.log(res)
      if (res.name === 'wikiHong') {
        $.ajax({
          url: './user1.json',
          success: (res2) => {
            console.log(res2)
          }
        })
      }
    }
  })
}
ajaxData();

// promise 串联的时候，下一个请求依赖于上一个请求也会嵌套，维护起来比较复杂
const promiseData = function () {
  const p1 = new Promise (function (resolve, reject) {
    $.ajax({
      url: './user.json',
      success(res) {
        resolve(res)
      },
      error(err) {
        reject(err)
      }
    })
  })

  const p2 = function (input) {
    return new Promise(function (resolve, reject) {
      $.ajax({
        url: './user1.json',
        success(res) {
          resolve({
            ...res,
            ...input
          })
        },
        error(err) {
          reject(err)
        }
      })
    })
  }
  p1.then(p2).then((res) => {
    console.log(res);
  })
}
```
## 9. generator
1. generator看上去像是一个函数，实际上可以返回多次。
2. 与函数不同的是，
    1. generator用function*定义，
    2. generator用yeild返回多次，
    3. function一步到底，generator中间可以停顿
3. 基本使用
```
function* show() {
  console.log('a');
  yeild;
  console.log('b');
}
const genObj = show();
genObj.next()
genObj.next()
genObj.next()
```
4. yeild可以传参
```
function* show(num1, num2) {
    console.log(num1 + ' ' + num2);
    const a = yield;
    console.log(a)
}
const genObj = show(66, 99);
genObj.next(12); //输出 "66 99" 没法给yield传参（原因：generator在执行yield前半部分，没走到赋值操作）
genObj.next(55); //输出55
genObj.next(67); //输出{value: undefined, done: true}
```
5. yield可以返回（相当于return）
```
function* show() {
    const a = yield 99;
    yield a;
    return 66;
}
 
const genObj = show();
 
const a1 = genObj.next(12);
console.log(a1); //输出{value: 99, done: false}
 
const a2 = genObj.next(55);
console.log(a2); //输出{value: 55, done: false}
 
const a3 = genObj.next(99);
console.log(a3); //输出{value: 66, done: true}
```

