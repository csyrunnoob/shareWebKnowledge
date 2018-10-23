##ES7--ES9的更新
### Es7
- 1 . Object.values()
 includes 是 Array 的一个方法，用于查找数组中是否包含了某个项（与 indexOf 不同的是，它可以包含 NaN）。
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG3.jpeg)
- 2 .指数中缀运算符
*加法和减法等数学运算分别有 + 和 - 等中缀运算符。类似的，中缀运算符通常用于指数运算。ECMAScript 2016 引入了，用来替代 Math.pow。*
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG4.jpeg)

###Es8
- 1.Object.entries()
*Object.entries() 与 Object.keys 相关，但它不仅返回键，而是以数组的方式返回键和值。这使得在循环中使用对象或将对象转换为 Map 等操作变得非常简单。*
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG6.jpeg)
- 2 . Object.values()
*Object.values() 是一个与 Object.keys() 类似的新函数，它会返回 Object 所有属性的值，但不包括原型链中的值。*
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG5.jpeg)
- 3.字符串填充
*String 新增了两个实例方法——String.prototype.padStart 和 String.prototype.padEnd——允许将空字符串或其他字符串追加或前置到原始字符串的尾部或开头。*
  ```
   'someString'.padStart(numberOfCharcters [,stringForPadding]); 
   '5'.padStart(10) // '          5'
   '5'.padStart(10, '=*') //'=*=*=*=*=5'
   '5'.padEnd(10) // '5         '
   '5'.padEnd(10, '=*') //'5=*=*=*=*='
   ```
- 4.**async/await**
*到目前为止，这是最重要和最有用的一个特性。异步函数可以避免回调地狱，并让整个代码看起来更简单。
async 关键字告诉 JavaScript 编译器要以不同的方式处理这个函数。在遇到函数中的 await 关键字时，编译器就会暂停。它假定 await 之后的表达式会返回一个 promise 并等待，直到 promise 完成或被拒绝。
在下面的示例中，getAmount 函数调用两个异步函数 getUser 和 getBankBalance。我们可以使用 promise，但使用 async await 更加优雅和简单。*
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG7.jpeg)

- 4.1 **返回 promise 的异步函数**
*如果你想获得异步函数返回的结果，需要使用 Promise 的 then 语法来捕获结果。
在下面的示例中，我们希望使用 console.log 来记录结果（但不在 doubleAndAdd 中）。所以，我们需要等待，并使用 then 语法将结果传给 console.log。*
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG8.jpeg)

- 4.2 **并行调用 async/await**
*在前面的例子中，我们调用 await 两次，每次等待一秒钟（总共 2 秒）。其实我们可以并行调用 await，因为 a 和 b 没有相互依赖。*
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG9.jpeg)

- 4.3 **async/await 函数的错误处理**
*使用 async/await 时，有多种方法可以处理错误。
选项 1——在函数中使用 try catch*
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG10.jpeg)

选项 2——捕获每个 await 表达式
由于每个 await 表达式都返回一个 Promise，因此可以像下面这样捕获每行的错误。
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG11.jpeg)

选项 3——捕获整个 async-await 函数
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG12.jpeg)
### ES9
- 1**对象的剩余属性**
剩余运算符...（三个点）允许我们提取尚未提取的 Object 属性。
*1.1你可以使用剩余操作符来提取你所需要的属性*
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG13.jpeg)

*1.2你还可以移除不需要的项！*
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG14.jpeg)

- 2**对象的延展性**
- ![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG15.jpeg)

- 3**异步迭代**
**这是一个非常有用的特性。基本上，它让我们可以更轻松地创建异步代码循环！
这个特性添加了一个新的“for-await-of”循环，允许我们在循环中调用返回 promise（或 promise 数组）的异步函数。循环在执行下一步之前会等待每个 Promise 完成。**
![Alt text](https://github.com/csyrunnoob/shareWebKnowledge/blob/csy/img/WechatIMG16.jpeg)


