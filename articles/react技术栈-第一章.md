

React组件的构建方法

- React.createClass

调用几次组件，就会创建几次实例。

- ES6 classes

这中方式和React.createClass会创建实例对象。

在React组件开发中，组件多用组合的方式，常用的方式是将组件拆分到合理的粒度，用组合的方式合成业务组件，也就是HAS-A的关系。

- 无状态函数

无状态组件不能像 React.createClass和 class 两种方法在调用时会创建新实例，**它创建时始终保持了一个实例，避免了不必要的检查和内存分配，做到了内部优化**。



React数据流

在React中，数据是自顶向下单项流动的，即从父组件到子组件。这条原则让组件之间的关系变得简单且可预测。

