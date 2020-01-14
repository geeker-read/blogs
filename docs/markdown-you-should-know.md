# 文章 | Markdown 一种现代化的文章编写方式


Markdown 是由 [John Gruber](https://daringfireball.net/projects/markdown/) 在 2004 年创建一种轻量级的标记语言，如今已成为世界上最受欢迎的标记语言之一（尤其被开发者、创作者广泛使用）。

你不用学习复杂的 HTML 标签，只需**掌握几种常用的标记符号**和一个**支持 Markdown 语法的编辑器**，就能快速的进行创作了。一旦你熟练掌握它的语法，将会大**大提高你的生产效率**。

**它的标记真的很简单！**

> “时间就是金钱，效率就是生命”

本文内容包括以下 3 部分：
1. 先通过视频让你快速了解 Markdown 的使用
2. 列出常用是标记写法及一张速查表（可以打印出来）
3. 一些支持 Markdown 的工具

## 视频

## Markdown 常用标记

### 1. 使用 `#` 定义标题（`注意 # 与文字之间要有空格`）：

```
# 一级标题 (相当于 HTML 代码中 h1)
## 二级标题
### 三级标题
#### 四级标题
#### 五级标题
##### 六级标题
```

预览：

![](https://imgkr.cn-bj.ufileos.com/12ee190d-43e3-426e-895e-008ee59da763.png)



### 2. 使用 `-` 或 `*` 表示无序列表，使用 `1. 2. 3.` 等表示有序列表

```
* 红色
* 绿色
* 蓝色

- 中文
- 英文

1. 张三
2. 李四
3. 王五
4. 赵六
```

预览

![](https://imgkr.cn-bj.ufileos.com/e6bc837e-35dc-426a-bf94-9e953652b936.png)


### 3. 列表的嵌套

通过 **tab 键**或 **2 个空格**缩进来实现列表的嵌套

```
* 第一章
  * 第一节
  * 第二节
* 第二章
* 第三章

1. 第一季
  1.1. 第一集
  1.2. 第二集
2. 第二季
3. 第三季
```

预览

![](https://imgkr.cn-bj.ufileos.com/c18e1c40-33e8-4234-ac08-7de4770f01dc.png)


### 3. 使用 `>` 这种尖括号（大于号）表示`引用`

```
> “时间就是金钱，效率就是生命”

> 床前明月光，
> 疑是地上霜。
> 举头望明月，
> 低头思故乡。
```

预览

![](https://imgkr.cn-bj.ufileos.com/f612163e-aa41-4e85-a0fa-c468222847cf.png)


### 4. 字体样式：粗体、斜体

通过**两个** `*` 或两个 `_` 包裹文字来**加粗文字**
通过**一个** `*` 或一个 `_` 包裹文字来**斜体文字**

```
**粗体写法一**
__粗体写法二__

*斜体写法一*
_斜体写法二_
```

预览

![](https://imgkr.cn-bj.ufileos.com/acb1a782-e20d-42bf-b45d-fdb96cdd0080.png)


### 5. 超链接：标签格式为 ` [链接文字](链接网址)`

```
[极客阅读](https://geeker-read.com)
```

预览

![](https://imgkr.cn-bj.ufileos.com/06db7d8a-e541-4d56-ac73-ed3114946d15.png)


### 6. 图片

图片的格式和超链接很像，区去在于：
1. 在中括号`[`前加一个半角叹号`!`
2. 中括号里的文字代表的是 **Alt 值**，正常不会显示在页面（提示：`当图片不可用时会显现这个 Alt 文字`）

```
![极客阅读 Logo](https://geeker-read.com)

![极客阅读 Logo](https://geeker-read.com/static/images/logo-home.png)
```

预览

![](https://imgkr.cn-bj.ufileos.com/61bfff64-001a-408f-8006-02e842c4d5b6.png)


### 7. 代码块

代码块有两种：
1. 行内，在一行文字中嵌入一块代码。用 **1 个 \`** (反引号) 包裹文字，在键盘的 Tab 键上面那个键，如图
![](https://imgkr.cn-bj.ufileos.com/2394917c-4dd9-4c57-894a-99d52d247a8b.png)
2. 块，一般会是多行占用的形式显示代码。用 **3 个 \`** (反引号) 包裹文字。

```
在命令行执行命令 `cd /`。

\```
离离原上草，一岁一枯荣。
野火烧不尽，春风吹又生。
远芳侵古道，晴翠接荒城。
又送王孙去，萋萋满别情。
\```

\```js
import Vue from 'vue'
import Element from 'element-ui'

Vue.use(Element)

import {
  Select,
} from 'element-ui'

Vue.component(Select.name, Select)
\```
```

预览

![](https://imgkr.cn-bj.ufileos.com/dc0a7694-5e97-40dc-8b4d-967e2a124e99.png)


### 8. 表格

表格会相对复杂一点点。

格式如下：

```
|  表头   | 表头  |
|  ----  | ----  |
| 单元格  | 单元格 |
| 单元格  | 单元格 |
```

预览

![](https://imgkr.cn-bj.ufileos.com/2ed4e671-b5b4-4b13-9788-fe602baae048.png)


### 9. 任务列表，用 `* [ ] Task name` 表示一个带复选框的列表（`注意空格`）

```
* [ ] 码字
* [ ] 摸鱼
```

预览

![](https://imgkr.cn-bj.ufileos.com/0e259e36-6a29-43c7-b751-bc12e6581533.png)

### 10. 横向分隔符， 3 个 `-`

```
上文

---

下文
```

预览

![](https://imgkr.cn-bj.ufileos.com/dff406d5-7104-41b2-b3c4-a6a29280e844.png)

## Markdown 速查表


![](https://imgkr.cn-bj.ufileos.com/90519bc2-203b-4a33-9643-dbd3182992ba.png)


## 支持 Markdown 的编辑器

- [语雀](https://www.yuque.com)
- [Typora](https://typora.io)
- [VS Code](https://code.visualstudio.com/download)
- [dillinger](https://dillinger.io)
- [StackEdit](https://stackedit.io/app)
- [印象笔记](https://www.yinxiang.com)
- [马克飞象](https://maxiang.io/)
