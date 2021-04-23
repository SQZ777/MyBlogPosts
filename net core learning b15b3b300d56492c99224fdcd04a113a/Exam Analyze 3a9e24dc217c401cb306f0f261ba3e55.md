# Exam Analyze

## 使用本專案提供之MySql DB ( 請參閱 [initial.sh](http://initial.sh/) )

將 exam-mysql 啟動

```bash
sh Course.Tools/initial.sh
```

## 建立名為 my_company 的 Database

`Database 與 Table 將會使用code first 的方式產生，所以先把 Code 的部分寫好`

建立名為 my_company 的 Database

到 appsettings.json 的檔案中，加入新的connection string

![../%5B91APP%5D%20ASP%20NET%20Core%20%E5%AF%A6%E6%88%B0%E5%88%86%E6%9E%90%202dd61f4ec4ea406b9a75046d2f51fa79/Untitled.png](../%5B91APP%5D%20ASP%20NET%20Core%20%E5%AF%A6%E6%88%B0%E5%88%86%E6%9E%90%202dd61f4ec4ea406b9a75046d2f51fa79/Untitled.png)

應題目要求，將 weather_db 改成 my_company

```json
"companyDb": "server=localhost;database=my_company;uid=root;pwd=password;"
```

到 Startup.cs 中，會發現 startup 的 GetConnectionString 指定的 Key 是錯誤的

![../%5B91APP%5D%20ASP%20NET%20Core%20%E5%AF%A6%E6%88%B0%E5%88%86%E6%9E%90%202dd61f4ec4ea406b9a75046d2f51fa79/Untitled%201.png](../%5B91APP%5D%20ASP%20NET%20Core%20%E5%AF%A6%E6%88%B0%E5%88%86%E6%9E%90%202dd61f4ec4ea406b9a75046d2f51fa79/Untitled%201.png)

所以需要將 weatherDB 改成 自己改好的 connection string，以及將WeatherDbContext 改成  MyCompanyDbContext

```csharp
services.AddDbContext<MyCompanyDbContext>(options =>
            {
                // 透過Configuration.GetConnectionString方法取得連線字串
                options.UseMySql(Configuration.GetConnectionString("companyDb"));
            });
```

## 建立名為 Employee 的 Table

## Employee 的欄位至少包含 id, name, salary

在 Models 的資料夾底下新增 Employee.cs

```csharp
using System;
using System.ComponentModel.DataAnnotations;
using System.ComponentModel.DataAnnotations.Schema;

namespace Course.WebApi.Models
{
    [Table("Employee")] //自訂db table name 
    public class Employee
    {
        [Key]//主键
        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]//透過db自動產出的唯一識別值
        [Column("id")] //自訂db table 欄位名稱 
        public int Id { get; set; }
        
        [Column("name")]
        public string Name { get; set; }
        
        [Column("salary")]
        public string Salary { get; set; }
    }
}
```

在 Repositories 的資料夾底下建立 MyCompanyDbContext.cs

```csharp
using Microsoft.EntityFrameworkCore;
using Course.WebApi.Models;

namespace Course.WebApi.Repositories
{
    
    public class MyCompanyDbContext : DbContext
    {
        public MyCompanyDbContext(DbContextOptions<MyCompanyDbContext> options) : base(options)
        {
        }

        // DbSet 用來指定要使用的 table類別
        public DbSet<Employee> WeatherForecasts { get; set; }
    }
}
```

這些 Code 寫好之後就可以使用 dotnet 的工具 build up database、table

```bash
dotnet ef migrations add InitialCreate --context=MyCompanyDbContext
dotnet ef database update --context=MyCompanyDbContext
```

### 確認資料庫是否被建立成功

連進 docker 的機器

```bash
docker -it exam-mysql bash
```

在 docker 的機器中進到 mysql 資料庫

```bash
mysql -P 3306 --protocol=tcp -uroot -ppassword
```

輸入 取得已被建立的資料庫

```bash
> show databases;
```

預期結果：可以看到 my_company 被建立完成

```bash
+--------------------+
| Database           |
+--------------------+
| information_schema |
| my_company         |
| mysql              |
| performance_schema |
| sys                |
+--------------------+
```

### 確認資料表是否被建立成功

```bash
> use my_company;
> show tables;
```

預期結果： 可以看到 Employee 這張 table 已被成功建立於 my_company 的資料庫中

```bash
+-----------------------+
| Tables_in_my_company  |
+-----------------------+
| Employee              |
| __EFMigrationsHistory |
+-----------------------+
```

## 網頁畫面不拘，只要能夠執行 瀏覽/新增/刪除 功能即可

### 瀏覽

在 Interfaces 的資料夾底下建立 IEmployeeRepo.cs

```csharp
using System.Collections.Generic;
using Course.WebApi.Models;

namespace Course.WebApi.Interfaces
{
    public interface IEmployeeRepo
    {
        IEnumerable<Employee> Read();
        IEnumerable<Employee> Update(Employee employee, int id);
    }
}
```

在 Repositories 的資料夾底下建立 EmployeeRepo.cs

```csharp
using System.Collections.Generic;
using System.Linq;
using Course.WebApi.Interfaces;
using Course.WebApi.Models;
using Course.WebApi.Repositories;

namespace Course.WebApi.Repositories
{
    public class EmployeeRepo : IEmployeeRepo
    {
        private readonly MyCompanyDbContext _context;
        public EmployeeRepo(MyCompanyDbContext context)
        {
            _context = context;
        }

        public IEnumerable<Employee> Update(Employee employee, int id)
        {
            throw new System.NotImplementedException();
        }

        public IEnumerable<Employee> Delete(int id)
        {
            throw new System.NotImplementedException();
        }

        IEnumerable<Employee> IEmployeeRepo.Read()
        {
            throw new System.NotImplementedException();
        }
    }
}
```