# net core learning

create a unit test project

```python
dotnet new mstest
```

create a empty web project

```python
dotnet new web
```

net core test should install `Moq` to mock class instance

need to register DI in startup 

## Ef Core

you need these package to launch

```jsx
Install-Package Microsoft.EntityFrameworkCore
Install-Package Microsoft.EntityFrameworkCore.Tools
Install-Package Microsoft.EntityFrameworkCore.SqlServer
```

### how to update database?

```jsx
add-migration {message-for-this-migration}
update-database
```

LibMan

[https://blog.darkthread.net/blog/libman-in-vs2017/](https://blog.darkthread.net/blog/libman-in-vs2017/)

[pre-lesson 3](net%20core%20learning%20b15b3b300d56492c99224fdcd04a113a/pre-lesson%203%20d2e4ea3f31744e929ade5452cf6de515.md)

[Lesson 3-動手做啦](net%20core%20learning%20b15b3b300d56492c99224fdcd04a113a/Lesson%203-%E5%8B%95%E6%89%8B%E5%81%9A%E5%95%A6%201488fc5fa831430fa3af174be0e5345d.md)

[Exam Analyze](net%20core%20learning%20b15b3b300d56492c99224fdcd04a113a/Exam%20Analyze%203a9e24dc217c401cb306f0f261ba3e55.md)

source: [https://stackoverflow.com/questions/58072703/jsonresultobject-causes-the-collection-type-newtonsoft-json-linq-jtoken-is](https://stackoverflow.com/questions/58072703/jsonresultobject-causes-the-collection-type-newtonsoft-json-linq-jtoken-is)

NotSupportedException: The collection type 'Newtonsoft.Json.Linq.JToken' is not supported.

```csharp
services.AddMvc().AddNewtonsoftJson();
```

```csharp
PM> Install-Package Microsoft.AspNetCore.Mvc.NewtonsoftJson -Version 3.1.0
```

![net%20core%20learning%20b15b3b300d56492c99224fdcd04a113a/Untitled.png](net%20core%20learning%20b15b3b300d56492c99224fdcd04a113a/Untitled.png)