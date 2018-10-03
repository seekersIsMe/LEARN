## set
* set构造函数创造类似数组的数据，set数据结构的数据没有重复的值
```
let ary = [1,2,3,4,4,4,4];
let setData = new Set();
ary.forEach((p) => {
setData.add(p)
})
console.log(setData) // [1,2,3,4]
```
* set函数接受一个数组（或者是具有iterable接口的数据类型）作为参数，用来初始化
```
let setData = new Set([1,2,3,4,4,4,4]);  //  [1,2,3,4]
let setDiv = new Set(document.getElementsByTagName('div'))
```

* Set 加入值的时候，不会发生类型转换,例如5和‘5’是不同的值，NaN和NaN相等的，见代码
```
let ary = [NaN,NaN,NaN,5,'5',{},{}]
let setData = new Set(ary);// [NaN,5,'5',{},{}]
``` 
# set实例的属性和方法
* 属性
    * Set.prototype.constructor：构造函数，默认就是Set函数。
    * Set.prototype.size：返回Set实例的成员总数。
* 方法
    * add(),向该set数据中加目标值，返回该set
    * has(),判断该set是否包含目标值，返回布尔值，表示是否包含
    * delete(),删除该set的目标值，返回boolean值，表示是否删除成功
    * clear(),清除该set的所有的项，没有返回值
    * Array.from方法可以将set数据转化成数组
```
// 数组去重
let ary = [1,2,3,3,3,3];
let setData = new Set(ary);
ary =Array.from(setData);

// 结合扩展运算符
let arr = [1,2,3,3,3,3];
let unique = [...new Set(arr)];
```
* 遍历操作
    * keys()：返回键名的遍历器
    * values()：返回键值的遍历器
    * entries()：返回键值对的遍历器
    * forEach()：使用回调函数遍历每个成员
    * **Set 结构没有键名，只有键值（或者说键名和键值是同一个值），所以keys方法和values方法的行为完全一致**
* 扩展运算符（...）内部使用for...of循环，所以set数据也可以使用扩展运算符
    * 数组的map和filter也可以间接用于set数据，先将set数据转化成数组，在使用map等数组方法

    * 所以set很容易实现交并差集
```
let a = new Set([1, 2, 3]);
let b = new Set([4, 3, 2]);

// 并集
let union = new Set([...a, ...b]);
// Set {1, 2, 3, 4}

// 交集
let intersect = new Set([...a].filter(x => b.has(x)));
// set {2, 3}

// 差集
let difference = new Set([...a].filter(x => !b.has(x)));
// Set {1}
```
----
## weakSet数据结构
* 特性
    * weakSet数据和set数据类似，但是weakSet的成员只能是对象
    * weakSet的成员对象是弱引用，即垃圾回收机制不考虑 WeakSet 对该对象的引用，也就是说，如果其他对象都不再引用该对象，
    那么垃圾回收机制会自动回收该对象所占用的内存，不考虑该对象还存在于 WeakSet 之中
    * 不可遍历，forEach，size都没有
* 方法
    * WeakSet.prototype.add(value)：向 WeakSet 实例添加一个新成员。
    * WeakSet.prototype.delete(value)：清除 WeakSet 实例的指定成员。
    * WeakSet.prototype.has(value)：返回一个布尔值，表示某个值是否在 
    
-----
## map数据类型
* 特性：
    * Object对象的数据结构是键值对的形式，键是字符串，而map结构的数据可以是‘值-值’的形式，对象也可以做键
    * 参数：
        * 任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构都可以当作Map构造函数的参数，见例子：
        ```
        let mapData = new Map([
        ['name','zhan']  //双元素
        ]);
        mapData.get('name') // 'zhan'
        ```
    * 针对同一个键进行赋值，后面的赋值操作会覆盖前面的值
    ```
     let mapData = new Map();
     mapData.set('name', 'zhan').set('name', 'hui');
     mapData.get('name'); //'hui'
    ```
    * 获取没有设置的键值，返回undefined
    ```
    let mapData = new Map().get('name'); // undefined
    ```
    * **注意**
        * 只用引用类型的数据作为键时，因为不同的对象对应的内存地址不一样，
    所以对应的值也就不同，其实Map数据的键是和内存地址做绑定的，这一点需要格外注意
        ```
        //下面两个对象对应的内存地址不同，
        let mapData = new Map();
        mapData.set({},'zhan');
        mapData.get({}); //undefined 
        ```
        * Map 的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map 将其视为一个键，比如0和-0就是一个键，
        布尔值true和字符串true则是两个不同的键。另外，undefined和null也是两个不同的键。虽然NaN不严格相等于自身，但 Map 将其视为同一个键。
        ```
        let map = new Map();
        
        map.set(-0, 123);
        map.get(+0) // 123
        
        map.set(true, 1);
        map.set('true', 2);
        map.get(true) // 1
        
        map.set(undefined, 3);
        map.set(null, 4);
        map.get(undefined) // 3
        
        map.set(NaN, 123);
        map.get(NaN) // 123
        ```
* Map实例的属性和操作方法
    * size，返回map数据的成员个数
    * set()
    * get()
    * has()，has方法返回一个布尔值，表示某个键是否在当前 Map 对象之中
    * delete(),delete方法删除某个键，返回true。如果删除失败，返回false
    * clear(),clear方法清除所有成员，没有返回值
* 遍历方法（遍历顺序是插入顺序谁先插入谁先遍历到）
    * keys()：返回键名的遍历器。
    * values()：返回键值的遍历器。
    * entries()：返回所有成员的遍历器。
    * forEach()：遍历 Map 的所有成员
    * 将map数据转换成数组，最快的就是扩展运算符
    ```
     let mapData = new Map([
     ['name', 'zhan'],
     ['age', 25],
     ['sex', 'boy']
     ]);
     let ary = [...mapData.keys()]; // ['name','age','sex'];
     let ary_ =[...mapData.entries()]; // [['name', 'zhan'],['age', 25],['sex', 'boy']]
     let ary__ =[...mapData]; // [['name', 'zhan'],['age', 25],['sex', 'boy']]
    ```
    * Map数据没有map和filter方法，不过借助数组，可以间接实现
    ```
    const map0 = new Map()
      .set(1, 'a')
      .set(2, 'b')
      .set(3, 'c');
    
    const map1 = new Map(
      [...map0].filter(([k, v]) => k < 3)
    );
    ```
## weakMap
* 特性
    * 类似于Map结构，不同的有以下几点
        * 只用对象作为键
        * WeakMap的键名所指向的对象，不计入垃圾回收机制
        * 没有遍历操作
* 方法和属性
    * get()
    * set()
    * has()
    * delete()
    * 没有size属性，因为没有办法列出所有键名，某个键名是否存在完全不可预测，跟垃圾回收机制是否运行相关，
    为了防止出现不确定性，就统一规定不能取到键名。二是无法清空，即不支持clear方法
* 应用
    * WeakMap 应用的典型场合就是 DOM 节点作为键名，将dom作为键
    * 由于WeakMap的键名所指向的对象，不计入垃圾回收机制，一旦这个 DOM 节点删除，该状态就会自动消失，不存在内存泄漏风险。
    ```
    let myElement = document.getElementById('logo');
    let myWeakmap = new WeakMap();
    
    myWeakmap.set(myElement, {timesClicked: 0});
    
    myElement.addEventListener('click', function() {
      let logoData = myWeakmap.get(myElement);
      logoData.timesClicked++;
    }, false);
    ```