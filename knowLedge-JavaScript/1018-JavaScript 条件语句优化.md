# javaScript条件语句
## 1.使用常见的三元操作符 
````
if (foo) bar(); else baz(); ==> foo?bar():baz(); 
if (!foo) bar(); else baz(); ==> foo?baz():bar(); 
if (foo) return bar(); else return baz(); ==> return foo?bar():baz(); 
````
## 2.使用and(&&)和or(||)运算符
````
if (foo) bar(); ==> foo&&bar(); 
if (!foo) bar(); ==> foo||bar(); 
````
## 3.switch语句
>使用if-else 或者switch 是基于测试条件的数量：条件数量较大，倾向于使用switch 而不是if-else。这通常归结到代码的易读性，如果条件较少时，if-else 容易阅读，而条件较多时switch更容易阅读。
>事实证明，大多数情况下switch 表达式比if-else 更快，但只有当条件体数量很大时才明显更快。两者间的主要性能区别在于：当条件体增加时，if-else 性能负担增加的程度比switch 更多。因此，我们的自然倾向认为条件体较少时应使用if-else 而条件体较多时应使用switch 表达式，如果从性能方面考虑也是正确的。
## 4.javascript的indexOf()方法 
````
var arr_data = [1,2,3]; 
arr_data.indexOf(1); //如果存在返回值的下标，不存在返回-1
````
## 5.使用 Array.includes 来处理多重条件(ES2016)

```js
// 条件语句
function test(fruit) {
  if (fruit == 'apple' || fruit == 'strawberry') {
    console.log('red');
  }
}
```
>如果要匹配更多的红色水果 , 就需要用更多的 `||` 这样写起来代码会变得臃肿,我们可以使用`Array.includes`[(Array.includes)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/includes)重写条件语句.

``` js
function test(fruit) {
  // 把条件提取到数组中
  const redFruits = ['apple', 'strawberry', 'cherry', 'cranberries'];
  if (redFruits.includes(fruit)) {
    console.log('red');
  }
}。
```
>我们把所有的红色水果都提取到一个数组中,这样使我们的代码看上去更整洁.
## 6.for循环和if判断
````
var arr = [1, 5, 10, 15];
//传统for
for(let i=0; i<arr.length; i++) {
    if(arr[i] === 查找值) {
        //则包含该元素
    }
}
// for...of
for(v of arr) {
    if(v === 查找值) {
        //则包含该元素
    }
}
//forEach
arr.forEach(v=>{
    if(v === 查找值) {
        //则包含该元素
    }
})
````
