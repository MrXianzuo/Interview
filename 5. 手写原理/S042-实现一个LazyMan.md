
## 实现以一个 lazyMan 类,他具有 sleep 和 sleepFist 和 eat方法
eat 输出正在吃 xx
sleep 输出睡了 xxx s
sleepFist 输出 首先睡了 xxx s



let joe = new LazyMan('joe')
joe.eat('apple')
    .eat('bananan')
    .sleepFisrt(10)
    .eat('orange')
    .sleep(20)
    .eat("pear")
 // 应该 等待 10s 输出 apple bananan  orange 等待 20s pear



```js

class LazyMan {
      constructor() {
        this.tasks = []
        setTimeout(() => {
          this.run()
        }, 0)
      }

      sleep(time) {
        this.tasks.push(() => {
          setTimeout(() => {
            console.log(`sleep ${time}`)
            this.run()
          }, time * 1000)
        })

        return this
      }

      sleepFirst(time) {
        this.tasks.unshift(() => {
          setTimeout(() => {
            console.log('slep first')
            this.run()
          }, time * 1000)
        })

        return this
      }

      eat(food) {
        this.tasks.push(() => {
          console.log(`eat fruit is${food}`)
          this.run()
        })

        return this
      }

      run() {
        let task = this.tasks?.shift();
        if (task) {
          task()
        }
      }
    }

    let lazyman = new LazyMan('tony')
        lazyman.eat('apple')
                .eat('banana')
                .sleepFirst(10)
                .eat("orange")
                .sleep(5)
                .eat("pear")



```
————————————————————————————————————————————————————————————————————————————————


题目描述：

实现一个LazyMan，可以按照以下方式调用:
LazyMan(“Hank”)输出:
Hi! This is Hank!

LazyMan(“Hank”).sleep(10).eat(“dinner”)输出
Hi! This is Hank!
//等待10秒..
Wake up after 10
Eat dinner~

LazyMan(“Hank”).eat(“dinner”).eat(“supper”)输出
Hi This is Hank!
Eat dinner~
Eat supper~

LazyMan(“Hank”).eat(“supper”).sleepFirst(5)输出
//等待5秒
Wake up after 5
Hi This is Hank!
Eat supper


实现如下：
```js
class _LazyMan {
  constructor(name) {
    this.tasks = []
    const task = () => {
      console.log(`Hi! This is ${name}`)
      this.next()
    }
    this.tasks.push(task)
    setTimeout(() => {
      this.next()
    }, 0)
  }
  next() {
    const task = this.tasks.shift()
    task && task()
  }
  sleep(time) {
    this.sleepWrapper(time, false)
    return this
  }
  sleepFirst(time) {
    this.sleepWrapper(time, true)
    return this
  }
  sleepWrapper(time, first) {
    const task = () => {
      setTimeout(() => {
        console.log(`Wake up after ${time}`)
        this.next()
      }, time * 1000)
    }
    if (first) {
      this.tasks.unshift(task)
    } else {
      this.tasks.push(task)
    }
  }
  eat(food) {
    const task = () => {
      console.log(`Eat ${food}`);
      this.next();
    };
    this.tasks.push(task);
    return this;
  }
}

// 测试
const lazyMan = (name) => new _LazyMan(name)

lazyMan('Hank').sleep(1).eat('dinner')

lazyMan('Hank').eat('dinner').eat('supper')

lazyMan('Hank').eat('supper').sleepFirst(5)

```