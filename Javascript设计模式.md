![image](https://github.com/HowToMeetYou/blog--/assets/41479550/ee5f58cf-8445-42c3-802f-49e6e0791140)## 1.面向对象编程设计的5个基本原则（SOLID）：

* 单一功能原则(Single Responsibility Principle)
* 开放封闭原则(Opened Closed Principle)
* 里氏替换原则(Liskov Substitution Principle)
* 接口隔离原则(Interface Segregation Principle)
* 依赖反转原则(Dependency Inversion Principle)
## 2.23种设计模式

![image](https://github.com/HowToMeetYou/blog--/assets/41479550/fc870b5f-a596-4760-b6b0-73294969bd92)



## 3.设计模式

### 3.1工厂模式

将共性封装，将特性单独处理

### 3.2抽象工厂模式

### 3.3单例模式

* 一个类有且仅有一个实例，并提供一个全局访问点
* 应用场景：vuex全局管理
* 实现方式
1.静态方法-ES6 class static
2.闭包
### 3.4代理模式([代理模式](https://juejin.cn/book/6844733790204461070/section/6844733790275780621))

#### 3.4.1事件代理

* 如通过冒泡特点，父元素代理子元素的事件
#### 3.4.2虚拟代理

* 类似骨架屏或者图片预加载，未加载完成前使用占位符，加载后替换src
#### 3.4.3缓存代理

* 用到过某个计算过的值的时候，不再重新计算而是使用原先计算过的结果
#### 3.4.4保护代理

* 需满足一定条件才可以访问相应的数据，类似拦截器
### 4.策略模式

* 定义一系列算法，将他们封装起来并且他们可以相互替换
如将if-else的复杂条件判断优化为对象映射的方式
* 应用场景([JavaScript 复杂判断的更优雅写法](https://juejin.cn/post/6844903705058213896))

这其实就是策略模式的应用，根据SOLID，还可以将funcA等方法提出来
```javascript
const actions = ()=>{
  return new Map([
    [/^guest_[1-4]$/,functionA],
    [/^guest_5$/,functionB],
    [/^guest_.*$/,functionC],
    //...
  ])
}

const functionA = ()=>{/*do sth*/}
const functionB = ()=>{/*do sth*/}
const functionC = ()=>{/*send log*/}

const onButtonClick = (identity,status)=>{
  let action = [...actions()].filter(([key,value])=>(key.test(`${identity}_${status}`)))
  action.forEach(([key,value])=>value.call(this))
}
```
* 5.状态模式
* 和策略模式很相似，但多了一个状态
```javascript
和策略模式相比，stateToProcessor和CoffeeMaker多了一个状态关联leftMilk，
而且逻辑耦合加重了（stateToProcessor放在CoffeeMaker中）
class CoffeeMaker {
  constructor() {
    /**
    这里略去咖啡机中与咖啡状态切换无关的一些初始化逻辑
  **/
    // 初始化状态，没有切换任何咖啡模式
    this.state = 'init';
    // 初始化牛奶的存储量
    this.leftMilk = '500ml';
  }
  stateToProcessor = {
    that: this,
    american() {
      // 尝试在行为函数里拿到咖啡机实例的信息并输出
      console.log('咖啡机现在的牛奶存储量是:', this.that.leftMilk)
      console.log('我只吐黑咖啡');
    },
    latte() {
      this.american()
      console.log('加点奶');
    },
    vanillaLatte() {
      this.latte();
      console.log('再加香草糖浆');
    },
    mocha() {
      this.latte();
      console.log('再加巧克力');
    }
  }
  // 关注咖啡机状态切换函数
  changeState(state) {
    this.state = state;
    if (!this.stateToProcessor[state]) {
      return;
    }
    this.stateToProcessor[state]();
  }
}
const mk = new CoffeeMaker();
mk.changeState('latte');
```
## 4.其他

* 发布-订阅模式源码阅读([EventEmitter](https://github.com/facebookarchive/emitter))
