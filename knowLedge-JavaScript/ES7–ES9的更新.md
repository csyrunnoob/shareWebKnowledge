##ES7--ES9的更新
### Es7
- 1. Object.values()
 includes 是 Array 的一个方法，用于查找数组中是否包含了某个项（与 indexOf 不同的是，它可以包含 NaN）。
![Alt text](./WechatIMG3.jpeg)
- 2 .指数中缀运算符
*加法和减法等数学运算分别有 + 和 - 等中缀运算符。类似的，中缀运算符通常用于指数运算。ECMAScript 2016 引入了，用来替代 Math.pow。*
![Alt text](./WechatIMG4.jpeg)

###Es8
- 1.Object.entries()
*Object.entries() 与 Object.keys 相关，但它不仅返回键，而是以数组的方式返回键和值。这使得在循环中使用对象或将对象转换为 Map 等操作变得非常简单。*
![Alt text](./WechatIMG6.jpeg)
- 2. Object.values()
*Object.values() 是一个与 Object.keys() 类似的新函数，它会返回 Object 所有属性的值，但不包括原型链中的值。*
![Alt text](./WechatIMG5.jpeg)
- 3.字符串填充
*String 新增了两个实例方法——String.prototype.padStart 和 String.prototype.padEnd——允许将空字符串或其他字符串追加或前置到原始字符串的尾部或开头。*
  ```
   'someString'.padStart(numberOfCharcters [,stringForPadding]); 
   '5'.padStart(10) // '          5'
   '5'.padStart(10, '=*') //'=*=*=*=*=5'
   '5'.padEnd(10) // '5         '
   '5'.padEnd(10, '=*') //'5=*=*=*=*='
   ```

