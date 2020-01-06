> 原文: [RESTful API Designing Guidelines — The Best Practices](https://medium.com/better-programming/restful-api-designing-guidelines-the-best-practices-39454135f61)

Facebook、Google、GitHub、Netflix 和其他一些科技巨头都为开发人员和产品提供了通过 API 来使用它们的数据。

即使你不为其他开发者或产品提供 API，通过精细设计的 API 也是对你的应用有益的。


关于 API 设计的最佳实践争论了很长时间，页并没有一个官方的定义。

API 是开发人员与数据进行交互的接口。 一个精心设计的 API 应该是易于使用的。

···

## 术语

下面列出来的是与 REST AP I相关的重要术语。

* `资源（Resource）`   实体对象或由一些相关联数据及可对其操纵的方法组成的事物。例如：动物、学校和员工都是资源。增删改查是对这些资源执行操作的方法。
* `集合（Collections）`一组资源，例如 compan**ies** 是 company 的集合。
* `URL`用来定位资源和执行操作的路径。

## API 终端（endpoint）

我们通过公司员工的例子来理解。

`/getAllEmployees` 是一个 API，将员工列表作为响应结果。围绕着公司的其他一些 API 如下：

* `/addNewEmployee`
* `/updateEmployee`
* `/deleteEmployee`
* `/deleteAllEmployees`
* `/promoteEmployee`
* `/promoteAllEmployees`

诸如此类不同操作的 API endpoint 会很多很多。大家会注意到每个 API endpoint 都包含了动作（action）的描述，当 API 增加时 API endpoint 将会变得越来难以维护。

### 错在哪里？

URL 应该只包含资源（名词），而不应该有动作（action）或动词。API `/addNewEmployee` 包含动作 `addNew` 和资源名 `Employee`。

### 正确的方式是什么？

`/companies` 是一个不包含动作的好例子。但问题是“我们怎么告诉服务器该对`companies`资源执行增删改查？”

这就是 HTTP 方法（GET、POST、PUT、DELETE）派上用场的时候了。

资源名应该始终使用`复数`形式，如果想查看一个实例，可以通过在 URL 中传递一个 ID。

* `GET` 方法 `/companies`：获取所有公司列表
* `GET` 方法 `/companies/34`：获取 ID 为 34 的公司详细信息。
* `DELETE` 方法 `/companies/34`：删除 ID 为 34 的公司
