# 筆記 - ASP.NET Core 使用 LibMan CLI

用 libman 來管理需要的前端程式庫

## libman 是甚麼?

*程式庫管理員 (LibMan) 是輕量型的用戶端程式庫取得工具。 LibMan 會從檔案系統或內容傳遞網路 (CDN)下載熱門的程式庫和架構。 支援的 Cdn 包括 CDNJS、 jsDelivr和 unpkg。 所選程式庫檔會擷取並放置在 [ASP.NET](http://asp.net/) Core 專案中的適當位置。*

source: [https://docs.microsoft.com/zh-tw/aspnet/core/client-side/libman/?view=aspnetcore-3.1](https://docs.microsoft.com/zh-tw/aspnet/core/client-side/libman/?view=aspnetcore-3.1)

環境準備

- .NET Core 2.1 SDK 以上

安裝指令

```bash
dotnet tool install -g Microsoft.Web.LibraryManager.Cli
```

![%E7%AD%86%E8%A8%98%20-%20ASP%20NET%20Core%20%E4%BD%BF%E7%94%A8%20LibMan%20CLI%20eafa5932f0964003aa5afa680b0e5aa4/Untitled.png](%E7%AD%86%E8%A8%98%20-%20ASP%20NET%20Core%20%E4%BD%BF%E7%94%A8%20LibMan%20CLI%20eafa5932f0964003aa5afa680b0e5aa4/Untitled.png)

使用指令來確認是否安裝成功

```bash
libman --version
```

![%E7%AD%86%E8%A8%98%20-%20ASP%20NET%20Core%20%E4%BD%BF%E7%94%A8%20LibMan%20CLI%20eafa5932f0964003aa5afa680b0e5aa4/Untitled%201.png](%E7%AD%86%E8%A8%98%20-%20ASP%20NET%20Core%20%E4%BD%BF%E7%94%A8%20LibMan%20CLI%20eafa5932f0964003aa5afa680b0e5aa4/Untitled%201.png)

使用指令來建立 libman.json

```bash
libman init
```

預設就直接用 cdnjs 即可 (直接按下 Enter)

![%E7%AD%86%E8%A8%98%20-%20ASP%20NET%20Core%20%E4%BD%BF%E7%94%A8%20LibMan%20CLI%20eafa5932f0964003aa5afa680b0e5aa4/Untitled%202.png](%E7%AD%86%E8%A8%98%20-%20ASP%20NET%20Core%20%E4%BD%BF%E7%94%A8%20LibMan%20CLI%20eafa5932f0964003aa5afa680b0e5aa4/Untitled%202.png)

會看到目前的資料夾出現 libman.json，內容為

```bash
{
  "version": "1.0",
  "defaultProvider": "cdnjs",
  "libraries": []
}
```

## 已安裝 jquery 為例

使用以下 libman 指令來安裝 jquery 到指定資料夾中

```bash
libman install jquery@3.2.1 --provider cdnjs --destination wwwroot/scripts/jquery --files jquery.min.js
```

![%E7%AD%86%E8%A8%98%20-%20ASP%20NET%20Core%20%E4%BD%BF%E7%94%A8%20LibMan%20CLI%20eafa5932f0964003aa5afa680b0e5aa4/Untitled%203.png](%E7%AD%86%E8%A8%98%20-%20ASP%20NET%20Core%20%E4%BD%BF%E7%94%A8%20LibMan%20CLI%20eafa5932f0964003aa5afa680b0e5aa4/Untitled%203.png)

安裝完成後 libman.json 的內容會如下

```bash
{
  "version": "1.0",
  "defaultProvider": "cdnjs",
  "libraries": [
    {
      "library": "jquery@3.2.1",
      "destination": "wwwroot/scripts/jquery",
      "files": [
        "jquery.min.js"
      ]
    }
  ]
}
```

之後只要根據這一個 libman.json 即可使用以下指令來重新還原專案需要的檔案

```bash
libman restore
```