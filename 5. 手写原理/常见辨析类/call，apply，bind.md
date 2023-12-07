
## call
```js
 Function.prototype.myCall = function(context, ...args) {
    context = context || window; // 参数默认值并不会排除null，所以重新赋值
    let fn = Symbol();
    context[fn] = this; // this是调用call的函数
    const result = context.fn(...args);
    delete context.fn; // 执行后删除新增属性
    return result;
  }

  let Person = {
      name: 'Tom',
      say(age) {
          console.log(this)
          console.log(`我叫${this.name}我今年${age}`)
      }
  }

  Person1 = {
      name: 'Tom1'
  }

  Person.say.call(Person1,18)//我叫Tom1我今年18
```



## apply
```js
// apply原理一致  只是第二个参数是传入的数组
Function.prototype.myApply = function (context, args) {
    context = context || window; 
  // 创造唯一的key值  作为我们构造的context内部方法名
  let fn = Symbol();
  context[fn] = this;
  const result = context.fn(...args);
  delete context.fn;
  return result;
  // 执行函数并返回结果
};
```

## 手写bind函数

```
Function.prototype.bind1 = function() {
  let args = Array.prototype.slice.call(arguments)
  let t = args.shift()
  let self = this;
  return function() {
    self.apply(t,arguments)
  }
}
```


```
Function.prototype.bind1 = function () { // 这块不可以使用箭头函数，因为 this 的指向不同
  // arguments 可以获取一个函数的所有参数，arguments 是一个伪数组
  // 使用 Array.from() 方法将 arguments 伪数组转化成数组
  const args = Array.from(arguments)
  // 获取 this 指向取出数组第一项，数组剩余的就是传递的参数
  const t = args.shift()
  const self = this // 当前函数 fn1.bind(...) 中的 fn1
  return () => {
    return self.apply(t, args)
  }
}

function fn1(a, b, c) {
  console.log('this', this)
  console.log(a, b, c)
}

const fn2 = fn1.bind1({x: 100}, 10, 20, 30)
const res = fn2()
```
