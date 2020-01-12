# 文章 | 分分钟吃透 <正则表达式>（理论 + 多图示例）

![](https://miro.medium.com/max/2560/0*qASU92GfMj2HCTMg.jpg)

> 翻译，原文来自：[Regex tutorial — A quick cheatsheet by examples](https://medium.com/factory-mind/regex-tutorial-a-simple-cheatsheet-by-examples-649dc1c3f285)

通过正则表达式在从文本中提取特定模式的内容时非常有用。

它应用很广泛，包括：验证、解析/替换字符串、数据格式转换以及网页爬取。

一旦你学会了它的语法，你几乎可以在所有编程语言（JavaScript、Java、VB、C#、C/C++、Python、Perl、Ruby、Delphi、R、Tcl 等等）中使用它。

让我们先看看一些示例和讲解吧。

## 基础

### 标记点（Anchors）：`^` 和 `$`

> * **^The** — 匹配任意以 `The` 开头的字符串 -> [试一试！](https://regex101.com/r/cO8lqs/2)
> ![](https://imgkr.cn-bj.ufileos.com/5383a267-653d-4060-a16c-12bce8f6f1fe.png)
> 
> * **end$** — 匹配以 `end` 结尾的字符串
> 
> * **^The end$** — 字符串**完整匹配** (也就是 `The end`)
> 
> * **roar** — 包含 `roar` 的任何字符串

### 量词：`*` `+` `?` 和 `{}`，即表示数量的

> * abc**\*** — 匹配 **ab 并且后面跟着 0 个或多个 c** 的字符串 -> [试一试！](https://regex101.com/r/cO8lqs/1)
> ![](https://imgkr.cn-bj.ufileos.com/f0b0738f-4702-4f00-a6fb-232928108705.png)
> 
> * abc**+** — 匹配 **ab 并且后面跟着 1 个或多个 c** 的字符串（至少一个 c）
> 
> * abc**?** — 匹配 **ab 并且后面跟着 0 个或 1 个 c** 的字符串
> 
> * abc**{2}** — 匹配 **ab 并且后面跟着 2 个 c** 的字符串
> 
> * abc**{2,}** — 匹配 **ab 并且后面跟着 2 个或更多个 c** 的字符串（至少 2 个）
>  
> * abc**{2,5}** — 匹配 **ab 并且后面跟着 2 到 5 个 c** 的字符串
> 
> * a**(bc)*** — 匹配 **a 并且后面跟着 0 个或多个 bc** 的字符串
> 
> * a**(bc){2,5}** — 匹配 **a 并且后面跟着 2 个到 5 个 bc** 的字符串

### 或操作符：`|` 或 `[]`

> * **a(b|c)** — 匹配 **a 并且后面跟着 b 或 c** 的字符串（也就是 ab 或 ac） -> [试一试！](https://regex101.com/r/cO8lqs/3)
> ![](https://imgkr.cn-bj.ufileos.com/31a870f6-08ed-4cde-9ca7-d56d274eaaa3.png)
>
> * **a[bc]** — 同上

### 字符类：`\d` `\w` `\s` 和 `.`

> * **\d** — 匹配**一个数字**（等同于 `[0-9]`） -> [试一试！](https://regex101.com/r/cO8lqs/4)
> ![](https://imgkr.cn-bj.ufileos.com/06696eaf-cd41-4c34-ab2b-037d89e76dcf.png)
> 
> * **\w** — 匹配**文字字符**（word character）(注：这里指的英文：数字、字母和下划线。等同于 `[a-zA-Z0-9_]`) -> [试一试！](https://regex101.com/r/cO8lqs/16779)
> ![](https://imgkr.cn-bj.ufileos.com/f82fcc5a-99f1-4f39-863f-58a67296bf24.png)
>
> * **\s** — 匹配**空格符**（包括制表符（tab） 和换行，等同于 ` [\r\n\t\f\v ]`） -> [试一试！](https://regex101.com/r/cO8lqs/16780)
> ![](https://imgkr.cn-bj.ufileos.com/66191a9f-04d3-4a84-8f94-db6b5ead00e3.png)
>
> * **.** — 匹配**任意字符** -> [试一试！](https://regex101.com/r/cO8lqs/5)
> ![](https://imgkr.cn-bj.ufileos.com/0b4af4a6-5cfd-4f5d-aae8-aed3b73e6188.png)


在使用 `.` 时要注意，有时使用字符类（`\d`, `\s`. `\w`）和反字符会更快更精准。

`\d`, `\s` 和 `\w` 的反义类是 `\D`, `\W` 和 `\S`（大写）。

例如：`\D` 得到与 `\d` 相反的结果。

> * **\D** — 匹配一个**非数字字符** -> [试一试！](https://regex101.com/r/cO8lqs/6)
> ![](https://imgkr.cn-bj.ufileos.com/2c8a1bff-fe1a-44dd-98d5-ddb351ba4f9c.png)


想要匹配 `^.[$()|*+?{\` 等这些字符，要是用 `\` 进行转义。

> * **\$\d** — 匹配**一个 $ 和一个数字** -> [试一试！](https://regex101.com/r/cO8lqs/9)
> ![](https://imgkr.cn-bj.ufileos.com/8e6bf1e9-c6e4-43d8-a369-e50402bfa341.png)


**提示：**通过正则表达式可以匹配那些**不可打印的字符**，例如：制表符（tab）用 `\t`、换行用 `\n`、回车用 `\r`。

### 标记（Flags）

正则通常以`/abc/`这种形式呈现，搜索模式以两个`/`进行分隔。并在结尾加上以下标记符：

* **g** (global) 返回所有匹配的
* **m**（multi-line）多行匹配，再同时使用 `^` 和 `$` 时会在多行匹配，而不是按完整的字符串匹配。
* **i**（insensitive）不区分大小写，例如：`/aBc/i` 能匹配 `AbC`。

## 中级

### 捕获分组（Grouping and capturing）： `()`

> * a**(**bc**)** — 用小括号创建**值是 bc 的捕获组** -> [试一试！](https://regex101.com/r/cO8lqs/11)
> ![](https://imgkr.cn-bj.ufileos.com/d9dd33cc-f460-44e5-95cf-f0628ef86b3b.png)
> 
> * a**(?:**bc**)**\* — 使用 **?: 来禁用捕获组** -> [试一试！](https://regex101.com/r/cO8lqs/12)
> ![](https://imgkr.cn-bj.ufileos.com/43ac7b1b-9162-4111-a2dc-2be8174d3ddc.png)
>
> * a(**?\<foo\>**bc) — 使用 **?\<foo\>** 给组命名 -> [试一试！](https://regex101.com/r/cO8lqs/17)
> ![](https://imgkr.cn-bj.ufileos.com/7c780ab2-61da-4136-ad53-a904e18cd7d3.png)


在数据提取中使用这种操作符非常实用，多个捕获分组会以数组形式呈现，所以可以通过索引获取这些值。

如果我们使用组命名 `(?<foo>...)`，我们就可以像使用字典（对象）一样，通过键名来取值。

### 中括号表达式：`[]`

> * **[abc]** — 匹配 **或是 a、或是 b、或是 c** 的字符串（等同于：`a|b|c`） -> [试一试！](https://regex101.com/r/cO8lqs/7)
> ![](https://imgkr.cn-bj.ufileos.com/7030f1f3-18b7-48a2-8564-53e8c28b9324.png)
> 
> * **[a-c]** — 同上
> 
> * **[a-fA-F0-9]** — 匹配**一个十六进制数字，不区分大小写** -> [试一试！](https://regex101.com/r/cO8lqs/22)
> ![](https://imgkr.cn-bj.ufileos.com/f835dcd0-9603-43a3-b06a-b3f4a4e3ec10.png)
> 
> * **[0-9]%** — 匹配 **% 前有一个 0 到 9 任意数字**的字符串
>
> * **[^a-zA-Z]** — 匹配**不包括 a 到 z，及 A 到 Z** 的字符串，这里的 `^` 是一个取反表达式 -> [试一试！](https://regex101.com/r/cO8lqs/10)
> ![](https://imgkr.cn-bj.ufileos.com/e6199016-6354-479a-8946-9c1482b5f8fe.png)


### 贪婪和懒惰（非贪婪）匹配

`* + {}`这几个量词就是贪婪操作符，什么意思？就是他们会匹配尽可能多的内容。

例如：`<.+>` 会从 `This is a <div>simple div</div> test` 中匹配出 `<div>simple div</div>`，如果我们只想要 `div` 标签，只需加上 `?` 使其变成懒惰的。

> * **<.+?>** — **懒惰匹配 < 和 > 里任意字符** -> [试一试！](https://regex101.com/r/cO8lqs/24)
> ![](https://imgkr.cn-bj.ufileos.com/f9491235-b6b1-4808-b58f-e8a5e8c621fc.png)


提示：最好避免使用 `.`，而选择严格的匹配方式。

> * **<[^<>]+>** — 匹配在 **< 和 > 里除了 < 和 > 外的任意字符** -> [试一试！](https://regex101.com/r/cO8lqs/23)
> ![](https://imgkr.cn-bj.ufileos.com/9b38967a-72b8-46c5-bd59-770a6ce8ed4e.png)


## 高级

### 边界：`\b` 和 `\B`（也就是单词边界）

> * **\babc\b** — 词 abc -> [试一试！](https://regex101.com/r/cO8lqs/25)
> ![](https://imgkr.cn-bj.ufileos.com/d0aee31e-9549-4b24-aa1f-1db7d97ecdcd.png)

`\b` 是和 `$` 与 `^` 类似的一个标记点。它的一侧是单词（`\w`），而另一侧不是单词（字符串的起始位置或空格）。

它的反义就是 `\B`。

> * **\Babc\B** — 匹配**有单词包围的 abc** -> [试一试！](https://regex101.com/r/cO8lqs/26)
> ![](https://imgkr.cn-bj.ufileos.com/79683458-8b67-40da-97af-fa3d752d50f7.png)


### 后向引用（Back-references）：`\1`

> * **(**[abc]**)\1** — 使用 `\1` 匹配和**第一个捕获组一样的文字** -> [试一试！](https://regex101.com/r/cO8lqs/14)
> ![](https://imgkr.cn-bj.ufileos.com/8755f1bc-8655-4134-aec7-adcd65b4c508.png)
>
> * ([abc])**(**[de]**)\2**\1 — 使用 `\2` (\3, \4 等) 来匹配和**第 2 个**（第 3 个、第 4 个等）**捕获组一样的文字** -> [试一试！](https://regex101.com/r/cO8lqs/15)
> ![](https://imgkr.cn-bj.ufileos.com/38b6944b-0e7a-4ddf-929a-83720bc633fc.png)
>
> * **(?\<foo\>**[abc])**\k\<foo\>** — 给捕获组命名为 **foo** 再通过 **\k\<foo\>** 引用他，同第一个例子结果一样 -> [试一试！](https://regex101.com/r/cO8lqs/16)
> ![](https://imgkr.cn-bj.ufileos.com/4be4fbd7-770a-446a-8a11-a2a73e05b142.png)


### 向前、向后：`(?=)` 和 `(?<=)`

> * d**(?=r)** — 匹配 **r** 前面的 **d**，不包括 **r** -> [试一试!](https://regex101.com/r/cO8lqs/18)
> ![](https://imgkr.cn-bj.ufileos.com/e3dcc9c9-0d5e-407c-a1f7-05c8635b0482.png)
> * **(?<=r)**d — 匹配 **r** 后面跟着的 **d**，不包括 **r**-> [试一试！](https://regex101.com/r/cO8lqs/19)
> ![](https://imgkr.cn-bj.ufileos.com/ba236774-27df-41ef-b922-ca96981ae901.png)

或使用反义操作

> * d**(?!r)** — 匹配 **r** 后面跟着的 **d**，不包括 **r** -> [试一试！](https://regex101.com/r/cO8lqs/20)
> ![](https://imgkr.cn-bj.ufileos.com/5a23dd34-bbcb-47ab-978b-f5b283896c10.png)
>
> * **(?<!r)**d — 匹配 **r** 前面的 **d**，不包括 **r** -> [试一试！](https://regex101.com/r/cO8lqs/21)
> ![](https://imgkr.cn-bj.ufileos.com/870bd1f1-e179-49af-9638-7721f891f732.png)

## 总结

如你所见，正则表达式的应用字段可以是多个的，估计你在开发中或多或少也用过一些，下面是几个常见的场景：

* 数据验证（例如，检查时间格式是否正确）
* 数据爬取（如网页爬虫，对内容的查找）
* 数据整理（Data Wrangling），将原始数据转换另一种格式
* 字符串解析（例如，URL GET参数）
* 字符串替换
* 语法高亮显示、文件重命名等
