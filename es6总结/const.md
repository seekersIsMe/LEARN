# 用法
* 声明一个只读的常量
* 暂时性死区特性，要先声明后使用
* 只在声明的作用域块内有效
* 统一作用域块内不可以重复声明同一常量

# 本质：
* const本质上只是保证该常量名指向的内存地址是不变的，类似c语言中指针的概念
所以如果使用const声明一个对象，只要不改变该常量名指向对象在栈内存的地址就不会报错，对象的属性是可以操作的，数据结构是可变的
* 如果要完全冻结对象，可以使用Object.freeze();见下列代码：
```
function freeze(obj) {
    if(!isObject(obj)) return;
    Object.freeze(obj);
    for(let i in obj) {
    freeze(i);
    }
}
function isObject(obj) {
return Object.prototype.toString.call(obj).slice(8,-1).toLowerCase()==='object';
}
```