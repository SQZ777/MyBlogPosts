# pre-lesson 3

## 下載專案

Lesson 3 的 Code 是沿用上週 Lesson2 的
為了更方便使用，此專案已將原本放在 Controller 中與 DB 相依的部分抽出來

[SQZ777/DotnetCoreCourse](https://github.com/SQZ777/DotnetCoreCourse)

## libman

安裝 libman (mac 應該一開始就已經裝好了)

```bash
dotnet tool install -g Microsoft.Web.LibraryManager.Cli
```

若有遇到 command not found: libman的話可以用過

```bash
sudo ln -s ~/.dotnet/tools/libman /usr/local/bin/libman
```

使用libman restore bootstrap

```bash
cd Course.WebApi
libman restore
```

## Data

將上次裝的 Mysql 叫起來

```bash
cd Course.Tools
sh dev.sh
```

如果你把db, table 砍了回顧一下上週的指令

```bash
1. 執行，產出migrations
dotnet ef migrations add InitialCreat --context=WeatherDbContext
2. 確認更新db
dotnet ef database update --context=WeatherDbContext
```

把專案跑起來之後（dotnet run），新增N筆資料 (12/6會用到)

```bash
curl -X "POST" "https://localhost:5001/WeatherForecast" -H 'Content-Type: application/json; charset=utf-8' -d $'{
      "date": "2019-11-30T18:25:43.511Z",
      "temperaturec": "222",
      "summary": "熱死了C"
    }' -k
```