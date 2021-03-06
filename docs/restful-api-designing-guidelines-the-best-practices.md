# [译] RESTful API 设计指南 - 最佳实践

![Snipaste_2020-01-06_16-52-11.png](https://cdn.nlark.com/yuque/0/2020/png/639317/1578302570478-810015d8-90ed-439e-be2e-dc17c56050c6.png#align=left&display=inline&height=634&name=Snipaste_2020-01-06_16-52-11.png&originHeight=634&originWidth=1344&size=1269474&status=done&style=none&width=1344)<br />


> 原文: [RESTful API Designing Guidelines — The Best Practices](https://medium.com/better-programming/restful-api-designing-guidelines-the-best-practices-39454135f61)

Facebook、Google、GitHub、Netflix 和其他一些科技巨头都为开发人员和产品提供了通过 API 来使用它们的数据。

即使你不为其他开发者或产品提供 API，但通过精细设计的 API 对你的应用也是有益的。


关于 API 设计的最佳实践争论了很长时间，并没有一个官方的定义。

API 是开发人员与数据进行交互的接口。 一个精心设计的 API 应该是易于使用的。


## 术语

下面列出来的是与 REST API 相关的重要术语。

* `资源（Resource）` 实体对象或由一些相关联数据及可对其操纵的方法组成的事物。例如：动物、学校和员工都是资源。增删改查是对这些资源执行操作的方法
* `集合（Collections）`一组资源，例如 compan**ies** 是 company 的集合
* `URL`用来定位资源和执行操作的路径


## API 终端（endpoint）

我们通过公司员工的例子来理解。

`/getAllEmployees` 是一个 API 来获取员工列表。围绕着公司的其他一些 API 如下：

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
* `GET` 方法 `/companies/34`：获取 ID 为 34 的公司详细信息
* `DELETE` 方法 `/companies/34`：删除 ID 为 34 的公司

其他例子，如果一个资源（resources）在另一个资源（resource）下，例如：一个公司的员工。

* `GET /companies/3/employees` ID 为 3 的公司所有员工列表
* `GET /companies/3/employees/45` ID 为 3 的公司里 ID 为 45 的员工信息
* `DELETE /companies/3/employees/45` 删除 ID 为 3 的公司里 ID 为 45 的员工
* `POST /companies` 创建新的公司，并返回新创建的公司详细信息

现在的 API 是不是更清晰一致呢？

### 结论

路径中的资源以`复数`形式存在，并通过 HTTP 方法对资源进行操作。


## HTTP 方法

HTTP 定义了一些方法来指示对资源的操作。

1. `GET` 获取资源数据，并不带有副作用。例如：`/companies/3/employees` 返回 ID 为 3 的公司里所有的员工列表。
2. `POST` 请求服务器在数据库中创建资源。例如：`/companies/3/employees` 给 ID 为 3 的公司创建新的员工。`POST` 是非幂等的。
3. `PUT` 请求服务更新资源或创建一个不存在的资源。例如：`/companies/3/employees/john` 更新或创建 ID 为 3 的公司下 employees 集合里的 *john*。`PUT` 是幂等的。
4. `DELETE` 请求从数据库中删除某个资源。例如： `/companies/3/employees/john/` 从 ID 为 3 的公司 employees 集合里的 *john*。


## HTTP 响应状态码

当客户端通过 API 请求服务器时，不论成功与否都应该知道反馈结果。

HTTP 状态码是几组在不同状况下给出说明的标准化代码，服务器应该返回正确的状态码。


### 2xx（成功）

表示服务器已经接收并成功处理了请求。

* 200 OK — 表示 GET、PUT 或 POST 成功
* 201 Created — 当有新的资源被创建时应该返回该状态码。例如：通过 POST 创建新资源，要返回 201
* 204 No Content — 表示请求已被成功处理但没有返回任何内容。例如：`DELETE /companies/43/employees/2` 删除 ID 为 2 的员工，删除成功后我们不需要返回任何数据。如果出现错误，如 `employee 2` 在数据库里不存在，返回码就不应该是 `2xx Success`，而是 `4xx Client Error`


### 3xxx（重定向）
* 304 Not Modified — 表示数据已被缓存。


### 4xx（客户端错误）

这些状态代码表示客户端发送了错误的请求。

* 400 Bad Request — 表示请求不能被处理，因为服务器不理解客户端发起的请求。
* 401 Unauthorized — 不允许客户端访问的资源，需要使用凭证（credentials）请求
* 403 Forbidden — 表示请求有效并通过了身份认证，但出于某个原因不允许访问
* 404 Not Found — 表示资源不可用或找不到
* 410 Gone — 表示资源已被永久删除，注意与 404 区别，资源以前存在但现在不存在会用 410 替代 404


### 5xx（服务器错误）

* 500 Internal Server Error — 表示请求有效，但是服务器端出现问题
* 503 Service Unavailable — 表示服务器宕机不能接收和处理请求。一般用在服务器维护期间

## 搜索、过滤、排序和分页

这些操作只是对数据集的查询。我么需要在 GET API 中附加查询参数。

* 排序 — 如果想获取有序的公司列表。`GET /companies` 应该接受多个排序查询参数。例如：`GET /companies?sort=rank_asc` 按公司升序排名排序
* 过滤 — 过滤数据集，通过传不同的查询参数。例如：`GET /companies?category=banking&location=india` 过滤出来在印度所属银行分类下的所有公司
* 搜索 — 例如：通过公司名搜索公司 `GET /companies?search=Digital Mckinsey`
* 分页 — 当数据很多时，需要将数据进行拆分。例如：`GET /companies?page=23`

如果 GET 请求的参数过长，服务端可能会返回 `414 URI Too long` 状态码，这时我们可以通过 POST 方式并将参数放在请求体（body）里。

## 版本控制

通过版本控制来升级你的 API，例子：`http://api.yourservice.com/v1/companies/34/employees`，如果有大版本升级，可以命名新的 API 版本 `v2` 或 `v1.x.x`。

---

极客阅读：[geeker-read.com](https://geeker-read.com)

<img src="https://github.com/geeker-read/weekly_issues/raw/master/docs/wx.png" width="450" />
