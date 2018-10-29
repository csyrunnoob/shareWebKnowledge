1.冒泡算法
```
    const arr=[1,2,6,8,9,4,0,11];
    Array.prototype.bubbleSort = function(){
        for(var i=0;i<this.length-1;i++){
            for(var j=i+1;j<this.length;j++){
                if(arr[i]<arr[j]){
                    var t= arr[j];
                    arr[j] = arr[i];
                    arr[i] = t;
                }
            }
        }
        return this;
    }
    console.log(arr.bubbleSort())
```
2.归并排序是一种分治算法。其思想是将原始数组切分成较小的数组，直到每个小数组只有一个位置，接着将小数组归并成较大的数组，直到最后只有一个排序完毕的大数组。
```
    const mergeSortRec = (arr)=>{
        let len = arr.length;
        if(len==1){return arr;};
        let piov = Math.floor(len/2);
        let arrF = arr.slice(0,piov);
        let arrR = arr.slice(piov,len);
        return merge(mergeSortRec(arrF),mergeSortRec(arrR))
    }

    function  merge(left,right){
        console.log(left,right)
        let il = 0;
        let ir = 0;
        let result = [];
        while(il<left.length&&ir<right.length){
            if(left[il]<right[ir]){
                result.push(left[il++]);
            }else{
                result.push(right[ir++]);
            }
        }
        while(il<left.length){
            result.push(left[il++]);
        }

        while(ir<right.length){
            result.push(right[ir++]);
        }
        return result
    }
    console.log(mergeSortRec(arr))
```
3.快速排序也许是最常用的排序算法了。它的复杂度为O(nlogn)，且它的性能通常比其他的复杂度为O(nlogn)的排序算法要好
```
    const arr=[1,2,6,8,9,4,0,11];
    Array.prototype.quickSort = function(){
        function quick(that){
            var len = that.length;
            if(len<=1){
                return that;
            }
            let middleNum = that[0];
            let right = [];
            let left = [];
            for(let i=1;i<len;i++){
                if(middleNum<that[i]){
                    right.push(that[i])
                }else{
                    left.push(that[i]);
                }
            }
            return [].concat(quick(left),[middleNum],quick(right));
        }
        return quick(this);
    }

    console.log(arr.quickSort())
```
4.插人排序每次排一个数组项，以此方式构建最后的排序数组。假定第一项已经排序了，接着， 它和第二项进行比较，第二项是应该待在原位还是插到第一项之前呢？这样，头两项就已正确排 序，接着和第三项比较（它是该插人到第一、第二还是第三的位置呢？），以此类推。
```
    const arr=[1,2,6,8,9,4,0,11];
    Array.prototype.insertionSort = function(){
        for(var i=1;i<this.length;i++){
            let preIndex = i-1;
            let current = this[i];
            while(preIndex>=0&&this[preIndex]>current){
                this[preIndex+1] = this[preIndex];
                preIndex--;
            }
            this[preIndex+1] = current
        }
        return this;
    }
    console.log(arr.insertionSort())
```
5.二分搜索：选择数组的中间值如果选中值是待搜索值，算法执行完毕（值找到了）如果待搜索值比选中值要小，则返回步骤1并在选中值左边的子数组中寻找如果待搜索值比选中值要大，则返回步骤1并在选种值右边的子数组中寻找
```
    const arr = [1,4,5,8,9,1,2,6];

    Array.prototype.quickSort = function(){
        function quick(that){
            var len = that.length;
            if(len<=1){
                return that;
            }
            let middleNum = that[0];
            let right = [];
            let left = [];
            for(let i=1;i<len;i++){
                if(middleNum<that[i]){
                    right.push(that[i])
                }else{
                    left.push(that[i]);
                }
            }
            return [].concat(quick(left),[middleNum],quick(right));
        }
        return quick(this);
    }
    
    Array.prototype.binarySearch = function(item) {
        var ary = this.quickSort()
        let low = 0
        let mid = null
        let element = null
        let high = ary.length - 1
        while (low <= high){
            mid = Math.floor((low + high) / 2)
            element = ary[mid]
            console.log('element',element)
            if (element < item) {
                low = mid + 1
            } else if (element > item) {
                high = mid - 1
            } else {
                return mid
            }
        }
        return -1
    }
    console.log(arr.binarySearch(9))
```
顺序搜索：顺序或线性搜索是最基本的搜索算法。它的机制是，将每一个数据结构中的元素和我们要找的元素做比较。顺序搜索是最低效的一种搜索算法。
```
    const arr = [1,4,5,8,9,1,2,6];
    Array.prototype.sequentialSearch = function(item) {
        for (let i = 0; i < this.length; i++) {
            if (item === this[i]) return i
        }
        return -1
    }
    console.log(arr.sequentialSearch(2))
```
6.选择排序：选择排序算法是一种原址比较排序算法。选择排序算法的思路是：找到数据结构中的最小值并 将其放置在第一位，接着找到第二小的值并将其放在第二位，以此类推。
```
    const arr=[1,2,6,8,9,4,0,11];
    Array.prototype.selectSort = function(){
        let minIndex ;
        for(var i=0;i<this.length-1;i++){
            minIndex = i;
            for(var j=i+1;j<this.length;j++){
                if(this[minIndex]<this[j]){
                    minIndex = j;
                }
            }
            if(i!=minIndex){
                var t = this[i];
                this[i] = this[minIndex];
                this[minIndex] = t;
            }
        }
        return this;
    }
    console.log(arr.selectSort())
```