## 手写Promise
```js
class MyPromise {
  constructor(executor) { // executor执行器
    this.status = 'pending' // 等待状态
    this.value = null // 成功或失败的参数
    this.fulfilledCallbacks = [] // 成功的函数队列
    this.rejectedCallbacks = [] // 失败的函数队列
    const that = this
    function resolve(value) { // 成功的方法
      if (that.status === 'pending') {
        that.status = 'resolved'
        that.value = value
        that.fulfilledCallbacks.forEach(myFn => myFn(that.value)) //执行回调方法
      }
    }
    function reject(value) { //失败的方法
      if (that.status === 'pending') {
        that.status = 'rejected'
        that.value = value
        that.rejectedCallbacks.forEach(myFn => myFn(that.value)) //执行回调方法
      }
    }
    try {
      executor(resolve, reject)
    } catch (err) {
      reject(err)
    }
  }
  then(onFulfilled, onRejected) {
    if (this.status === 'pending') {
      // 等待状态，添加回调函数到成功的函数队列
      this.fulfilledCallbacks.push(() => {
        onFulfilled(this.value)
      })
      // 等待状态，添加回调函数到失败的函数队列
      this.rejectedCallbacks.push(() => {
        onRejected(this.value)
      })
    }
    if (this.status === 'resolved') { // 支持同步调用
      console.log('this', this)
      onFulfilled(this.value)
    }
    if (this.status === 'rejected') { // 支持同步调用
      onRejected(this.value)
    }
  }
}

// 测试
function fn() {
  return new MyPromise((resolve, reject) => {
    setTimeout(() => {
      if(Math.random() > 0.6) {
        resolve(1)
      } else {
        reject(2)
      }
    }, 1000)
  })
}
fn().then(
  res => {
    console.log('res', res) // res 1
  },
  err => {
    console.log('err', err) // err 2
  })
```
## 手写Promise.then

## 手写Promise.catch

## 手写Promise.finally

## 手写Promise.all
```js
function promiseAll(arr) {
  return new Promise((resolve,reject) =>{
      if(!Array.isArray(arr)) {
        return reject(new Error('请传入数组'))
      }

      let data = [],count = 0,arrNum = arr.length;
      for(let i = 0; i < arrNum; i ++) {
        Promise.resolve(arr[i]).then(res => {
          data[i] = res
          count ++
          if(count == arrNum) {
            resolve(data)
          }
        })
        .catch(e => reject(e))
      }
  })
}


// 测试

let pro1 = new Promise((resolve,reject) => {
    setTimeout(()=>{
        resolve(1)
    },1000)
})
let pro2 = new Promise((resolve,reject) => {
    setTimeout(()=>{
        resolve(2)
    },2000)
})
let pro3 = new Promise((resolve,reject) => {
    setTimeout(()=>{
        resolve(3)
    },3000)
})
let data1 = [pro1,pro2,pro3]
promiseAll(data1).then(res => {
    console.log(res)
})

```
## 手写Promise.race


```js
static PromiseRace(arr) {
  return new Promise((resolve,reject) => {
      if(!Array.isArray(arr)) {
        reject(throw new Error('请输入数组'))
      }
      for(let i = 0;i < arr.length; i ++) {
        Promise.resolve(arr[i]).then(res => {
            resolve(res)
        },err => {
            reject(err)
        })
      }
  })
}




let p1 = new Promise((resolve,reject) => {
  setTimeout(() => {
    resolve(1)
  },1000)
})

let p2 = new Promise((resolve,reject) => {
  setTimeout(() => {
    reject(2)
  },200)
})



PromiseRace([p1,p2]).then(res => {
  console.log(res)
}).catch(err => {
  console.log(err)
})

```

二、Promise.race的使用
顾名思义，Promse.race就是赛跑的意思，意思就是说，Promise.race([p1, p2, p3])里面哪个结果获得的快，就返回那个结果，不管结果本身是成功状态还是失败状态。


返回只返回最快的那个（无论对错），但是也都执行一遍的


## 手写 async/await

```js

    // const aFunc = () => {
    //   return new Promise((resolve) => {
    //     setTimeout(() => {
    //       resolve('a')
    //     }, 1000)
    //   })
    // }
    // const bFunc = () => {
    //   return new Promise((resolve) => {
    //     setTimeout(() => {
    //       resolve('b')
    //     }, 1000)
    //   })
    // }

function* generator() {
    let result = yield aFunc();
    console.log(result);
    let other = yield bFunc();
    console.log(other);
}
myAwait(generator);

function myAwait(genner, ...args) {
    let iter = genner(...args); //得到生成器的迭代器
    return new Promise((resolve, reject) => {
        let result; //iter每次暂停时的结果
        //! inner就是在手动迭代iter
        let inner = function (yield) {
            result = iter.next(yield); //开始迭代 将这里的yield当作yield传入生成器
            if (result.done) {
                //迭代结束：
                resolve(result.value); //Promise结束
            } else {
                //如果没有结束 等到promise的结束继续递归
                return Promise.resolve(result.value).then((fulfilled) => {
                    inner(fulfilled);
                });
            }
        };
        inner(); //迭代器第一次不应该传入参数
    });
}
```
-----------------------------------
手写一个async/await的实现

## 用Promise封装一个delay函数
