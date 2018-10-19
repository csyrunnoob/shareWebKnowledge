# 如何优雅的使用for循环
>日常编码过程中 , 对于一些数据的迭代以及遍历 , 首先想到的就是`for`循环。
````
//获取年龄超过18岁人的名称
let data = [
  {name: 'zhangSan', age: 16},
 {name: 'liSi', age: 20},
]
let nameArr = []
for(let i=0;i<data.length;i++){
  if(data[i].age>18){
    nameArr.push(data[i].name)
  }
}
console.log(nameArr)//['liSi']
````
>这样写起来可以实现, 但是不优雅,代码繁琐.
## forEach - (es6)
````
//获取年龄超过18岁人的名称
let data = [
  {name: 'zhangSan', age: 16},
 {name: 'liSi', age: 20},
]
let nameArr = []
data.forEach(item=>{
  if(item.age>18){
    nameArr .push(item.name)
  }
})
console.log(nameArr)//['liSi']
````
>这种方式，看起来优雅了许多，省去了不少代码, 简单易懂.

>**是不是说forEach是不是就是最好的优雅方案？有没有存在问题？如果我们遇到一种情况，就是对列表遍历处理后，需要返回一个处理后的数组，那我们继续使用forEach是否能够达到我们的目的呢？**

````
//方式一
let one = [1,2,3]
let oneArr = one.forEach(item=>item+1)
console.log(oneArr)      //undefined
//方式二
let two = [1,2,3]
let twoArr = []
two.forEach((item,index,arr)=>{
  twoArr[index] = item+1
})
console.log(twoArr )
````
>可以看到，第一种处理是希望处理完后直接赋值给一个变量，然而forEach循环返回的是undefined，第二种处理虽然最终的确能够达到我们目标，拿到处理完的数据，但是还需要在外部定义一个变量进项一系列处理,也不是很优雅.

## Map() - (es6)
>`Map`方法会对原始数组中的每个元素进行遍历一次，并调用callback，最终返回一个新的数组而不会影响到原始数组。
````
let three = [1,2,3]
let threeArr = []
threeArr = three.map(item=>item+1)
console.log(threeArr)    //[2,3,4]
````
>曾经的多行循环代码只需要一行就可以完成，看着也优雅了好多，而且返回一个新的处理后的素组以及不会对原有的数组产生污染
## Filter() - (es6)
>`filter`方法，简单滴说就是对数组进行筛选或过滤，然后返回一个新的数组，并不会对原始数组产生任何的影响

>我们又要回到for循环那个栗子,如何用`filter`让代码更优雅
````
let data = [
  {name: 'zhangSan', age: 16},
 {name: 'liSi', age: 20},
]
let nameArr = []
nameArr = data.filter(item=>item.age>18)
console.log(nameArr)     //[{name:'liSi',age:20}]
````
>使用`Filter`方法只能达到了第一步目标就是优雅了for循环里的条件语句,如何直接返回我们想要的内容呢,这里我们可以使用`map`方法,两者结合起来
````
let data = [
  {name: 'zhangSan', age: 16},
 {name: 'liSi', age: 20},
]
let nameArr = []
nameArr = data.filter(item=>item.age>18).map(item=>item.name)
console.log(nameArr)     //['liSi']
````
>这样会觉得看起来舒服好多，而且也通俗易懂，而这也是最终优雅方案

**forEach比较适用于不改变原始数组数据，仅仅拿数组数据进行做一些事情，而map则适用于改变数据值并且返回一个新数组**

>除了上述提到的常用情景外，我们还会遇到很多其他地方可以继续优雅for循环,`some`方法和`every`方法
## Every()和Some() - (es6)
#### some：遍历数组元素，只要遇到条件为true则直接返回true，否则直到遍历最后并返回false
#### every：遍历数组元素，只要遇到条件为false则直接返回false，否则直到遍历最后并返回true

>现在有一种情景，就是要根据后端返回的一个列表里有费用低于0时就展示提示语。
````
let res = [
  {name:'zhangSan',fee:100},
  {name:'liSi',fee:-29},
  {name:'wangWu',fee:45}
]
let showTips = false
showTips = res.some(item=>item.fee<0)
console.log(showTips )    //true
showTips = !res.every(item=>item.fee>0)
console.log(showTips )    //true
````
## reduce()
>`reduce()` 方法接收一个函数作为累加器（accumulator），数组中的每个值（从左到右）开始缩减，最终为一个值

>上面为官方的说法，简单地理解，就是对一个列表进行遍历，第一次取两个元素进行处理得到一个新值，然后到下一次循环时就拿该新值与第三个元素进行处理，以此类推，最终得到一个值并返回。以下为图解
![avatar](https://user-gold-cdn.xitu.io/2018/10/17/166818ac12643341?imageView2/0/w/1280/h/960/format/webp/ignore-error/1)
>需求:后端返回一个对象，而我们需要对这个对象进行处理只需要得到指定属性值，多余的属性就过滤掉。
````
let res = {
  a:1,
  b:2,
  c:3,
  d:4
}
let arr = ['a','d']
let obj= {}
obj = arr.reduce((p,n)=>n in res&&(p[n]=res[n])&&p,{})
console.log(obj)    //{a: 1, d: 4}
````