#### React组件的渲染流程是什么？
+ 使用React.createElement或JSX编写React组件，实际上所有的JSX代码最后都会转换成React.createElement(...), Babel帮助我们完成了这个转换的过程。
+ createElement函数对key和ref等特殊的props进行处理，并获取defaultProps对默认props进行赋值，并且对传入的孩子节点进行处理，最终构成一个ReactElement对象（所谓虚拟DOM）
+ ReactDOM.render将生成好的虚拟DOM渲染到指定的容器上，其中采用了批处理、事务等机制并且对特定浏览器进行了性能优化，最终转换为真实的DOM。







作者：我真的好想学习啊
链接：https://juejin.im/post/5d89cbd26fb9a06b2005a597
来源：掘金
