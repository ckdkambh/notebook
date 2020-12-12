- [flask教程](https://blog.csdn.net/sinat_38682860/article/details/82354342)
- [异步，协程](https://docs.python.org/zh-cn/3.7/library/asyncio.html)
- asyncio.create_task() 函数用来并发运行作为 asyncio 任务 的多个协程。
- asyncio.run(coro, *, debug=False) 总是会创建一个新的事件循环并在结束时关闭之。它应当被用作 asyncio 程序的主入口点，理想情况下应当只被调用一次
- awaitable asyncio.gather 如果 aws 中的某个可等待对象为协程，它将自动作为一个任务加入日程。
- coroutine asyncio.wait(aws, *, loop=None, timeout=None, return_when=ALL_COMPLETED)
- asyncio.run报错，可以用以下代码代替
```
        loop = asyncio.get_event_loop()
        loop.run_until_complete(func())
```
- [python类变量，实例变量的区别](https://blog.csdn.net/weixin_39986952/article/details/84842567)
- 递归定义defaultdict
```
nested_dict = lambda: defaultdict(nested_dict)
```

