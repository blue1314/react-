#### setState是同步的还是异步的？

1. 生命周期和合成事件中
在React的生命周期和合成事件中，React仍然处于他的更新机制中，这时无论调用多少次setState，都不会立即执行更新，而是将要更新的存入 `_pendingStateQueue`，将要更新的组件存入`dirtyComponent`。

当上一次更新机制执行完毕，以生命周期为例，所有组件，即最顶层组件`didmount`后会将批处理标志设置未`false`。这时将去除`dirtyComponent`中的组件以及`_pendingStateQueue`中的`state`进行更新。这样就可以确保组件不会被重新渲染多次。

所以。setState本生并不是异步的，而是 React 的批处理机制给人一种异步的假象。

2. 异步代码和原生事件中
```js
componentDidMount(){
    setTimeout(()=> {
        console.log('调用setState');
        this.setState({
            index: this.state.index+1
        })
        console.log('state', this.state.index);
    }, 0)
}
```
上面的代码，当我们在异步代码中调用 setState时，根据Javascript的异步机制，会将异步代码先暂存，等所有同步代码执行完毕后再执行，这时React的批处理机制已经走完，处理标志设置为false，这时再调用setState即可立即执行更新，拿到更新后的结果
3. 一个更好的获取方式
```js
setState({
    index: this.state.index+1
}, ()=>{
    console.log(this.state.index);
})
```
setState的第二个参数接收一个函数，该函数会在 React的批处理机制完成之后调用，所以你想在调用 setState后立即获取更新后的值，请在该回调函数中获取。
4. 为什么有时连续多次setState只有一次生效？
React会批处理机制中存储的多个 setState进行合并,传入的是对象，很明显会被合并成一次。
React会对多次连续的 setState进行合并，如果你想立即使用上次 setState后的结果进行下一次 setState，可以让 setState 接收一个函数而不是一个对象。这个函数用上一个 state 作为第一个参数，将此次更新被应用时的 props 做为第二个参数。



作者：我真的好想学习啊
链接：https://juejin.im/post/5d89cbd26fb9a06b2005a597
来源：掘金
