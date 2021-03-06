在Diff算法中，比较的两方是新的虚拟DOM和旧的虚拟DOM，而不是虚拟DOM和真实DOM，只不过Diff 的结果会更新到真实DOM上。

时间复杂度 O(N)

前提条件，做了两个假设：
（一）、如果两个元素的类型不同，那么他们将生成两颗不同的树
（二）、为列表中的元素设置key属性，用key标识对应的元素在多次render过程中是否发生变化

    正是有这两个假设的存在，才有时间复杂度为O(N)的Diff算法

在不同的情况下，React具体如何比较两颗树的差异的。

（一）、
    当根节点是不同类型时

    React会认为新的树和旧的树完全不同，不会再继续比较其他属性和子节点，而是把整棵树拆掉重建（包括虚拟DOM和真实的DOM树）


（二）、
    当根节点是相同的DOM元素类型时

    会保留根节点，而比较根节点的属性，然后只更新那些变化了的属性
（三）、
    当跟节点是相同的组件类型时
    如果两个根节点是相同类型的组件，对应的组件实例不会被销毁，只是会执行更新操作，同步变化的属性到虚拟DOM树上，这一过程组件实例的componentWillReceiveProps()和componentWillUpdate()会被调用。
    比较完根节点以后，React会以同样的原则继续递归比较子节点，每一个子节点相对于其他层级一下的节点来说又是一个根节点。如此递归比较，知道比较完两棵树上所有的节点，计算得到最终的差异，更新到DOM树中。


key属性是为了帮助React提高Diff算法的效率。当一组子节点定义了Key,React会根据key来匹配子节点，在每次渲染之后，只要子节点的key值没有变化，React会认为这是同一个节点。**注意：key值最好不要用在列表中的索引，因为列表中的顺序一旦发生改变，就可能导致大量的key失效**