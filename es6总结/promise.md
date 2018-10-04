# promise简介
* Promise是异步编程的一种解决方案
* 异步编程有以下四种：
    * Promise
    * 回调函数
    * 事件
    * 订阅发布模式
* 特点
    * Promise对象的状态不受外界的影响，只有异步操作的结果可以影响其状态，其状态有：
        * pending（进行中）
        * fulfilled(已成功)
        * rejected (失败)
    * 一旦状态确定，就不会变化
        * Promise对象的状态改变，只有两种可能：从pending变为fulfilled和从pending变为rejected。只要这两种情况发生，
        状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）
       
* 缺点：
    * 一旦新建，Promise就会执行，并且无法中途取消
    * 若没有设置回调函数，Promise内部抛出的错误无法反应到外部
    * pending状态时，无法得知是刚开始还是快结束了

# 基本用法
 * Promise对象是一个构造函数，其接受一个函数为参数，该函数有两个参数，分别是resolve和reject。它们是两个函数，由 JavaScript 引擎提供，不用自己部署。
    ```
    let myPromise = new Promise(function (resolve,reject) {
        console.log('立即执行')
        if (异步操作成功) { 
            resolve(value)
        }else {
        reject(error)
        }
    })
    ```
    * resolve函数将Promise对象的状态从pending变成fulfilled,并将异步操作成功的结果作为参数传递出去
    * reject函数将Promise对象的状态从pending变成rejected,并将异步操作失败的结果作为参数传递出去
 * Promise实例生成之后，通过then可以指定resolved（fulfilled）状态和rejected状态的回调函数。
   ```
   // 下面举一个简单的ajax请求的例子
    let myPromise = new Promise(function (resolve,reject) {
           $.ajax({
           succeed:function () {
            resolve(value)
           }，
           error: function () {
           reject(error)
           }
           })
        })
        myPromise.then(function (value) {
        //请求成功后续的操作，这里也可以做后续的异步操作
        },function (error) {
        //请求失败后续的操作，该函数可选
        })
   ```
 * Promise一旦新建，其参数函数就会立即执行
    ```
    let promise = new Promise(function(resolve, reject) {
      console.log('Promise');
      resolve();
    });
    
    promise.then(function() {
      console.log('resolved.');//这里是异步操作，所以是最后输出
    });
    
    console.log('Hi!');
  
    // Promise
    // Hi!
    // resolved
    ```
  ----
# Promise.prototype.then() 
* then接受两个参数，这两个参数是函数，第一个参数函数为resolved状态下的回调函数，第二个参数函数为rejected状态下的回调函数，且可选
* then执行完后会返回新的Promise对象,所以支持链式调用，可以有多个then，前面then的回调函数返回的结果会作为参数传给后面then的回调函数
  ```
    getJSON("/posts.json").then(function(json) {
      return json.post;//将json.post传给后面的then回调函数
    }).then(function(post) {
      // ...
    });
  ```
* 见下面例子：
  ```
  const getJSON = function(url) {
    const promise = new Promise(function(resolve, reject){
      const handler = function() {
        if (this.readyState !== 4) {
          return;
        }
        if (this.status === 200) {
          resolve(this.response);
        } else {
          reject(new Error(this.statusText));
        }
      };
      const client = new XMLHttpRequest();
      client.open("GET", url);
      client.onreadystatechange = handler;
      client.responseType = "json";
      client.setRequestHeader("Accept", "application/json");
      client.send();
  
    });
  
    return promise;
  };
    getJSON("/post/1.json").then(function(post) {
      return getJSON(post.commentURL); //这里手动返回一个Promise对象，后面then的回调函数funcA和funcB执行哪一个，取决该返回的Promise的状态
    }).then(function funcA(comments) {
      console.log("resolved: ", comments);
    }, function funcB(err){
      console.log("rejected: ", err);
    });
    //用箭头函数写则简明很多：
    getJSON("/post/1.json").then(
      post => getJSON(post.commentURL)
    ).then(
      comments => console.log("resolved: ", comments),
      err => console.log("rejected: ", err)
    );
  ``` 
# Promise.prototype.catch() 
* 返回Promise对象
* Promise.prototype.catch方法是.then(null, rejection)的别名，用于指定异步操作发生错误时的回调函数。
    * 例子一：
  ```
    const promise = new Promise(function(resolve, reject) {
      throw new Error('err');//如果抛出错误是在resolve之后，catch就不会捕捉到错误，因为Promise 状态已经变成resolved，再抛出错误是无效的
      resolve('test')
    }).then((value)=>{
        console.log(value)
    },(err)=>{
    console.log(err)
    });
    promise.catch(function(error) {
      console.log(error);
    });
  ```
  * 例子二：
  ```
    function timeout(ms) {
      return new Promise((resolve, reject) => {
        setTimeout(resolve, ms, 'done');
      });
    }
    
    timeout(2000).then((value) => {
      throw new Error('test1');
      console.log(value);
    },
    (value) => {
    throw new Error('test2');
      console.log(value+1);//不会执行
    }
    ).catch((err)=>{
    console.log(err+2); //test12
    });
  ```
  * 不要在then方法里面定义 Reject 状态的回调函数（即then的第二个参数），建议使用catch方法。
  ```
    // 不好的做法
    promise
      .then(function(data) {
        // success
      }, function(err) {
        // error
      });
    
    // 好的做法，这样可以捕捉前面的then内部抛出的错误
    promise
      .then(function(data) { //cb
        // success
      })
      .catch(function(err) {
        // error
      });
  ```
----

# Promise.prototype.finally()
* 不管promise最后的状态，在执行完then或catch指定的回调函数以后，都会执行finally方法指定的回调函数

----

# Promise.all()
* Promise.all方法用于将多个 Promise 实例，包装成一个新的 Promise 实例。
* 本扩展实现了将多个异步操作合并为一个操作，也就是并行处理异步，最后统一操作结果，注意:本方法只能通过Promise对象直接调用，实例不能进行此操作。
   all()接收一个参数数组，数组中的每一项都对应一个

-----

# Promise.race()
* Promise.race方法同样是将多个 Promise 实例，包装成一个新的 Promise 实例。
  ```
  const p = Promise.race([p1, p2, p3]);
  ```
* 只要p1、p2、p3之中有一个实例率先改变状态，p的状态就跟着改变。那个率先改变的 Promise 实例的返回值，就传递给p的回调函数。
* Promise.race方法的参数与Promise.all方法一样，如果不是 Promise 实例，就会先调用下面讲到的Promise.resolve方法，将参数转为 Promise 实例，再进一步处理。

----

# Promise.resolve
* 将对象转化成Promise对象
* 参数：
    * 参数是一个Promise实例，则不做任何变化，直接返回该Promise实例
    * 参数是一个thenable对象，就是有then方法的对象，Promise.resolve方法会将这个对象转为 Promise 对象，然后就立即执行thenable对象的then方法。
        ```
        let thenable = {
          then: function(resolve, reject) {
            resolve(42);
          }
        };
        
        let p1 = Promise.resolve(thenable);
        p1.then(function(value) {
          console.log(value);  // 42
        });
        ```
    * 参数不是具有then方法的对象，或根本就不是对象,则Promise.resolve方法返回一个新的Promise对象，状态为resolve
    * 不传参数，直接返回一个resolved状态的 Promise对象
    ```
    //这样可以得到一个Promise对象
    const p = Promise.resolve();
    
    p.then(function () {
      // ...
    });
    ```
 
----

# Promise.reject()
* 返回一个状态为rejected的Promise对象
* 参数
  * 传入的参数作为后续then中reject状态回调函数的参数
  * 具有then方法的对象，则后续的then的reject状态回调参数函数接受的参数是该对象
    ```
    const thenable = {
      then(resolve, reject) {
        reject('出错了');
      }
    };
    
    Promise.reject(thenable)
    .catch(e => {
      console.log(e === thenable) //这里捕获的是thenable对象，而不是‘出错了’字符串，不像Promise.resolve会执行thenable对象的then方法
    })
    ```
# Promise.try()
* 同步的函数同步执行，异步函数异步执行
    ```
    const f = () => console.log('now');
    Promise.try(f);
    console.log('next');
    // now
    // next
    ```