# symbol一个独一无二的值
```
let s = Symbol('foo')
let ss = Symbol('foo')
s === ss  // false
```
 * 将symbo作为属性名或在函数名，需要用[]
 ```
 let name = Symbol('name');
 let fun = Symbol('fun');
 let obj =  {
        [name]:zhan
        [fun](){
        // doSomething
                }
            }
```
* Object.getOwnPropertySymbols获取该Symbol属性

* 消除魔术字符创
```angular2html
const shapeType = {
  triangle: Symbol('triangle'),
  other: Symbol('other')
};

function getArea(shape, options) {
  let area = 0;
  switch (shape) {
    case shapeType.triangle:
      area = .5 * options.width * options.height;
      break;
      case shapeType.other:
      // do something
      break;
  }
  return area;
}

getArea(shapeType.triangle, { width: 100, height: 100 })
```

# Symbol.for()、 Symbol.keyFor()
* Symbol.for()与Symbol()这两种写法，都会生成新的 Symbol。它们的区别是，
前者会被登记在全局环境中供搜索，后者不会。Symbol.for()不会每次调用就返回一个新的 Symbol 类型的值，
而是会先检查给定的key是否已经存在，如果不存在才会新建一个值。比如，如果你调用Symbol.for("cat")30 次，
每次都会返回同一个 Symbol 值，但是调用Symbol("cat")30 次，会返回 30 个不同的 Symbol 值。
````
let s1 = Symbol.for('foo');
let s2 = Symbol.for('foo');

s1 === s2
````

* Symbol.keyFor方法返回一个已登记的 Symbol 类型值的key。
````
let s1 = Symbol.for("foo");
Symbol.keyFor(s1) // "foo"

let s2 = Symbol("foo");
Symbol.keyFor(s2) // undefine   变量s2属于未登记的 Symbol 值，所以返回undefined
````