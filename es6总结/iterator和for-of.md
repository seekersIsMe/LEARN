# iterator接口
* 简介：
    * Iterator 接口的目的，就是为所有数据结构，提供了一种统一的访问机制，即for...of循环（详见下文）。当使用for...of循环遍历某种数据结构时，该循环会自动去寻找 Iterator 接口。
* iterator接口遍历过程
   1. 创建一个指针对象，指向当前数据结构的起始位置。也就是说，遍历器对象本质上，就是一个指针对象。
   2. 第一次调用指针对象的next方法，可以将指针指向数据结构的第一个成员。
   3. 第二次调用指针对象的next方法，指针就指向数据结构的第二个成员。
   4. 不断调用指针对象的next方法，直到它指向数据结构的结束位置。 
* 凡是具有Symbol.iterator属性的数据就具备for-of遍历的功能
    * Symbol.iterator本身是一个函数，该函数返回一个具有next方法的对象(简称遍历对象)，next方法则是返回一个获取下一个成员的信息
    * 遍历对象除了有next方法，还可以部署return和throw方法
       * return方法的使用场合是，如果for...of循环提前退出（通常是因为出错，或者有break语句），就会调用return方法。如果一个对象在完成遍历前，需要清理或释放资源，就可以部署return方法。
       * throw方法主要是配合 Generator 函数使用，一般的遍历器对象用不到这个方法
       * **下面见例子**
           * 例子一：
            ```
            next:()=>({
            value:value,//返回下一个成员的值
            done:false // 判断是否遍历到结尾了
            })
            ```   
            * 例子二：
            ```
            var it = makeIterator(['a', 'b']);
            
            it.next() // { value: "a", done: false }
            it.next() // { value: "b", done: false }
            it.next() // { value: undefined, done: true }
            
            function makeIterator(array) {
              var nextIndex = 0;
              return {
                next: function() {
                  return nextIndex < array.length ?
                    {value: array[nextIndex++], done: false} :
                    {value: undefined, done: true};
                }
              };
            }
            ```
           * 例子三：
           ```
            let arr = ['a', 'b', 'c'];
            let iter = arr[Symbol.iterator]();
            
            iter.next() // { value: 'a', done: false }
            iter.next() // { value: 'b', done: false }
            iter.next() // { value: 'c', done: false }
            iter.next() // { value: undefined, done: true }
            ```
* 原生具备Iterator接口的数据类型有：
  * Array
  * Map
  * Set
  * String
  * TypedArray
  * 函数的 arguments 对象
  * NodeList 对象

----

# for-of
* 一个数据结构只要部署了Symbol.iterator属性，就被视为具有 iterator 接口，就可以用for...of循环遍历它的成员。
也就是说，for...of循环内部调用的是数据结构的Symbol.iterator方法。
* forEach遍历无法通过break命令或return命令跳出循环，除非抛出错误
* for-of可以和break、continue和return配合使用，且简洁
    