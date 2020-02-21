# 视频 + 文字 | JavaScript 除了 console.log，这些 console 也应该了解下

<img src="https://cdn.nlark.com/yuque/0/2020/png/639317/1579079219778-040f6599-22ee-47f1-8229-4c45d9e0288b.png" />


「视频」https://www.bilibili.com/video/av90533709/

---

**文字版：**

console 是浏览器内置的调试器，作为前端开发对它应该并不陌生，打印 `console.log(console)` 时，你会发现它提供比你想象的多的方法。

![](https://imgkr.cn-bj.ufileos.com/a2b8bc44-7d0b-4b3d-a6e0-ca99aeb3eec0.png)

# 错误（false）断言

通过 `console.assert()` 可以将条件为 **false** 时的 log 打印出来，例如：`console.assert(false, 'user not logged in 😷');`


![](https://imgkr.cn-bj.ufileos.com/c375bc74-62fd-45e2-8089-2b99751a66a5.png)


![](https://imgkr.cn-bj.ufileos.com/22846c40-89dc-4fd3-b63a-3206ab1acdf8.png)

# 将数据以表格的形式显示

该方法可以将数据已表格的方式更加直观的展示出来。

> 这个方法需要一个必须参数 data，data 必须是一个**数组**或者是一个**对象**；还可以使用一个可选参数 columns。

![](https://imgkr.cn-bj.ufileos.com/67215191-963f-4098-8ea2-58061e86d77a.png)

![](https://imgkr.cn-bj.ufileos.com/ce851457-13f8-4dea-a0f8-dcbd6732b29c.png)

# 分组（group）输出

在循环或定时器中不断输入内容，真的很糟糕。

![](https://imgkr.cn-bj.ufileos.com/65e47c04-1bdc-4411-9888-93dd975a92a7.png)

通过 `console.group()` 将输出分组，随后输出到控制台上的内容都会被添加一个缩进，表示该内容属于当前分组，直到调用 `console.groupEnd() `之后,当前分组结束。

![](https://imgkr.cn-bj.ufileos.com/76c0a527-68ae-4659-abad-bbf279c75ada.png)

![](https://imgkr.cn-bj.ufileos.com/9fddace0-94e5-44f8-ae99-2bf520bfed05.png)

# 显示指定 JavaScript 对象的属性

在控制台中显示指定 JavaScript 对象的属性，并通过类似文件树样式的交互列表显示。

![](https://imgkr.cn-bj.ufileos.com/7e48752d-0602-467f-a436-41f9576e120e.png)

![](https://imgkr.cn-bj.ufileos.com/440e5fab-affc-445d-b816-7dfe4cdb68ee.png)

> Chrome 中通过 console.log 也能显示类似的结果。

# 计数统计

对于有需要做计数统计的工作可以使用 `console.count()` 完成，此函数接受一个可选参数 label。

![](https://imgkr.cn-bj.ufileos.com/ceae265b-ee18-4358-8b41-a2f8d001fd55.png)

![](https://imgkr.cn-bj.ufileos.com/5ee8cba0-5cb7-466d-83b6-da6edecb760c.png)

# 性能调试 - 计时器

当需要查看一段代码运行时间时，可以通过 `console.time()` 来实现。它会启动一个计时器来跟踪某一个操作的占用时长。每一个计时器必须拥有唯一的名字。当以此计时器名字为参数调用 `console.timeEnd()` 时，浏览器将以毫秒为单位，输出对应计时器所经过的时间。

![](https://imgkr.cn-bj.ufileos.com/0c9e9143-dbc6-4abb-b436-b08b1614faa4.png)

![](https://imgkr.cn-bj.ufileos.com/b572b8a7-b579-4454-9e20-f64bf0875dc2.png)

# 堆栈跟踪

通过 `console.trace()` 展示运行到该 console.trace() 所经过的调用路径。

![](https://imgkr.cn-bj.ufileos.com/39994a82-665a-489b-9266-226ba40fae7c.png)

> 提示：从下至上查看调用路径

# 不单调的 console.log 🌈

通过 CSS 改变输出样式。

`console.log('%c JavaScript is beautiful 🌈', 'color: pink; background-color: black; padding: 10px; font-weight: bold')`

![](https://imgkr.cn-bj.ufileos.com/772b474c-3846-4540-9191-4eee1346ca4a.png)

> 注意：`%c` 和第二个参数对样式的设置。

以上就是视频中提到的 console 技巧。**注意 console 主要用于代码的调试，生产环境上建议将 console 相关代码删除**。
