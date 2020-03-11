---
title: Thymeleaf
tags:
  - thymeleaf
categories: 后端
date: 2019-07-24 13:26:13
cover: true
---


# 简介
Thymeleaf是一款用于渲染XML/XHTML/HTML5内容的模板引擎，类似JSP，Velocity，FreeMaker等，它也可以轻易的与Spring MVC等Web框架进行集成作为Web应用的模板引擎。
Thymeleaf是spring boot推荐使用的模板引擎，最大的特点是能够直接在浏览器中打开并正确显示模板页面，而不需要启动整个Web应用，但是总是看到说其效率有点低
<!--more-->
# 引入
在html页面中引入Thymeleaf命名空间，即`<html lang="en" xmlns:th="http://www.thymeleaf.org">`此时在html模板文件中动态的属性使用`th:某某某`命名空间修饰


# 变量表达式（替换变量的值）

``` html
<p th:text="'你是否读过，'+${book.name}+'!!'">
    同EL表达式有些相似的效果，如果有数据，被替换
    完成前后端分离效果(这些是前端代码)
</p>
```

# URL表达式（引入css/js）

- 用来引入js和css（CSS使用th:href，js使用使用th:src)）

``` html
<link th:href="@{/css/xx.css}"/>
<script th:src="@{/js/xx.js}"></script>
```
spring boot默认配置Thymeleaf的静态资源路径为resource/static，上面的代码将引入resource/static/css/ss.css文件

# *号表达式

对$变量表达式的简化，直接看代码

``` html
<div th:object="${session.user}">
    <p>Name: <span th:text="*{firstName}">Sebastian</span>.</p>
    <p>Surname: <span th:text="*{lastName}">Pepper</span>.</p>
    <p>Nationality: <span th:text="*{nationality}">Saturn</span>.</p>
  </div>

<!--等价于-->
<div>
  <p>Name: <span th:text="${session.user.firstName}">Sebastian</span>.</p>
  <p>Surname: <span th:text="${session.user.lastName}">Pepper</span>.</p>
  <p>Nationality: <span th:text="${session.user.nationality}">Saturn</span>.</p>
</div>
```

# 国际化

`#{}`简单看一下就可以，文字国际化表达式允许我们从一个外部文件获取区域文字信息(.properties)，用Key索引Value，还可以提供一组参数(可选).

``` html
<head>
<title th:test="#{main.title}"></title>    
<body>
    <table>
        <th th:text="#{header.address.city}">
        <th th:text="#{header.address.country}">
    </table>
</body>  

```

# 表达式支持的语法

- 字面值

    - 文本文字（Text literals）: 'one text', 'Another one!',…
    - 数字文本（Number literals）: 0, 34, 3.0, 12.3,…
    - 布尔文本（Boolean literals）: true, false
    - 空（Null literal）: null
    - 文字标记（Literal tokens）: one , sometext

- 文本操作（Text operations）

    - 字符串连接（String concatenation）: +
    - 文本替换（Literal substitutions）: |The name is ${name}|

- 算术运算（Arithmetic operations）

    - 二元运算符（Binary operators）: + , - , * , / , %
    - 减号（Minus sign (unary operator)）: -

- 布尔操作（Boolean operations）

    - Binary operators: and , or
    - Boolean negation (unary operator): ! , not

- 比较和等价(Comparisons and equality)

    - Comparators: > , < , >= , <= ( gt , lt , ge , le )
    - Equality operators: == , != ( eq , ne )

- 条件运算符（Conditional operators）三元运算符

    - If-then: (if) ? (then)
    - If-then-else: (if) ? (then) : (else)
    - Default: (value) ?: (defaultvalue)

# 常用标记

- 条件判断

```html
<a href="comments.html" th:href="@{/comments(prodId=${prod.id})}" th:unless="${#lists.isEmpty(prod.comments)}">view</a>
<a href="comments.html"  th:href="@{/product/comments(prodId=${prod.id})}"   th:if="${not #lists.isEmpty(prod.comments)}">view</a>
```

- 循环遍历

```html
<tr th:each="prod,iterStat : ${prods}" th:class="${iterStat.odd}? 'odd'">
    <td th:text="${prod.name}">Onions</td>
    <td th:text="${prod.price}">2.41</td>
    <td th:text="${prod.inStock}? #{true} : #{false}">yes</td>
</tr>
```

- 模板

    - 定义模板

    ```html
    <div th:fragment="copy">

    </div>
    ```
    - 使用模板

    ```html
    <div th:import="copy">

    </div>
    ```