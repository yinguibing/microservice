# thymeleaf实践手册

## 标签

### th:utext

> **非转义文本：unescaped text**
>
> 与th:text标签对比，th:text 会将文本值直接放到html标签内部，不会进行语法解析。当标签内部需要放入HTML代码的时候，此时th:text就不能完成html语义解析。thymeleaf提供了th:utext标签进行文本解析，符合html规范的将解析展示。

```html
<p th:utext="${information.inforMationDeal.newsContent}">
  	<!--newsContent的值 -->
     <p>中国民航网 通讯员李鹏 报道：近日，石家庄机场联合河北航空共同举行了石家庄机场国际货运业务发展座谈		会，就拓展国际货运市场与开发进行了深入沟通和交流。厦门航空、中国邮政速递物流，以及各国际货运代理		公司、快件公司等相关负责人参加了会议。
    </p>
</p>
```

### th:href

> 超链接标签。
>
> 对超链接的文本用@{}进行标记，路径变量采用${}完成取值

```html
<img class="media-object" src="/common/images/8.jpg" th:src="@{${article.imageUrl}}"/>
```

**超链接分类及处理**

* 绝对URL

  > 通常是针对跨域访问，URL一般为http:///xxxx,

* 相对URL

* * 相对服务器
    * 调用同一应用服务器上其他应用的连接 ~/otherapp/api
  * 相对上下文
    * 本应用的接口 /api
  * 相对页面
    * 以本页面的路径为父路径，通常调用的是子页面及子页面的API   child/api
  * 相对协议
    * 不常用

### th:onclick

> 点击事件标签。难点在于点击方法参数值获取传入写法。

```html
<div class="div-pad"  th:onclick="'javascript:toInfromationDel(\''+${article.id}+'\');'" th:if="${#strings.isEmpty(article.imageUrl) }">
</div>
方法的参数值必须放到''中，所以需要对（）中的单引号进行转义处理\'
```



## 逻辑运算标签

### th:if

**对取值表达式取到值判断**

th:if="${attr}"

1、如果值不为null
　　值为boolean且为true
　　值为数字且非0
　　值为字符且非0
　　值是字符串且不是：“false”,“off”，“no”
　　值不是boolean、数字、字符、字符串
2、如果值为null，则th:if运算结果为false

## 内置对象方法

> >表达式工具对象，主要是对数据进行基本的逻辑处理，如字符串是否为空判断等，通常与逻辑运算符配合使用。

```html
#dates 与java.util.Date对象的方法对应，格式化、日期组件抽取等等
#calendars 类似#dates，与java.util.Calendar对象对应
#numbers 格式化数字对象的工具方法
#strings 与java.lang.String对应的工具方法：contains、startsWith、prepending/appending等等
#objects 用于对象的工具方法
#bools 用于布尔运算的工具方法
#arrays 用于数组的工具方法
#lists 用于列表的工具方法
#sets 用于set的工具方法
#maps 用于map的工具方法
#aggregates 用于创建数组或集合的聚合的工具方法
#messages 用于在变量表达式内部获取外化消息的工具方法，与#{…}语法获取的方式相同
#ids 用于处理可能重复出现（例如，作为遍历的结果）的id属性的工具方法
```



## 日期时间处理

### JDK8 日期时间处理

