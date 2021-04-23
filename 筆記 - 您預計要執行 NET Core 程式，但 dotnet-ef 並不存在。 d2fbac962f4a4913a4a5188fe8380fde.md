# 筆記 - 您預計要執行 .NET Core 程式，但 dotnet-ef 並不存在。

有點久沒寫 dotnet core

今天重新把環境都裝回來，然後趁機更新到最新版本的 dotnet core

於是在開發的第一步要執行 dotnet ef 就發生了錯誤

如圖

![%E7%AD%86%E8%A8%98%20-%20%E6%82%A8%E9%A0%90%E8%A8%88%E8%A6%81%E5%9F%B7%E8%A1%8C%20NET%20Core%20%E7%A8%8B%E5%BC%8F%EF%BC%8C%E4%BD%86%20dotnet-ef%20%E4%B8%A6%E4%B8%8D%E5%AD%98%E5%9C%A8%E3%80%82%20d2fbac962f4a4913a4a5188fe8380fde/Untitled.png](%E7%AD%86%E8%A8%98%20-%20%E6%82%A8%E9%A0%90%E8%A8%88%E8%A6%81%E5%9F%B7%E8%A1%8C%20NET%20Core%20%E7%A8%8B%E5%BC%8F%EF%BC%8C%E4%BD%86%20dotnet-ef%20%E4%B8%A6%E4%B8%8D%E5%AD%98%E5%9C%A8%E3%80%82%20d2fbac962f4a4913a4a5188fe8380fde/Untitled.png)

原來是因為在 dotnet core 3.0 之後 .NET SDK 就不再包含 dotnet ef，所以如果要在 dotnet 裡面用 dotnet ef 的指令，必須要先進行安裝

```jsx
dotnet tool install --global dotnet-ef
```

執行安裝後就可以看到安裝完成的畫面啦

![%E7%AD%86%E8%A8%98%20-%20%E6%82%A8%E9%A0%90%E8%A8%88%E8%A6%81%E5%9F%B7%E8%A1%8C%20NET%20Core%20%E7%A8%8B%E5%BC%8F%EF%BC%8C%E4%BD%86%20dotnet-ef%20%E4%B8%A6%E4%B8%8D%E5%AD%98%E5%9C%A8%E3%80%82%20d2fbac962f4a4913a4a5188fe8380fde/Untitled%201.png](%E7%AD%86%E8%A8%98%20-%20%E6%82%A8%E9%A0%90%E8%A8%88%E8%A6%81%E5%9F%B7%E8%A1%8C%20NET%20Core%20%E7%A8%8B%E5%BC%8F%EF%BC%8C%E4%BD%86%20dotnet-ef%20%E4%B8%A6%E4%B8%8D%E5%AD%98%E5%9C%A8%E3%80%82%20d2fbac962f4a4913a4a5188fe8380fde/Untitled%201.png)

歡迎回來 dotnet-ef!