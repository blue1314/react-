#### 为什么React组件首字母必须大写？

babel在编译时会判断 JSX中组件的首字母，当首字母为小写时，其被认定为原生 DOM标签， createElement的第一个变量被编译为字符串；当首字母为大写时，其被认定为自定义组件， createElement的第一个变量被编译为对象；


作者：我真的好想学习啊
链接：https://juejin.im/post/5d89cbd26fb9a06b2005a597
来源：掘金
