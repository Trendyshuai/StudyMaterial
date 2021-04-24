# 一、准备工作
1. 建立项目
    * 项目名 XXX.Api
    * 解决方案名 XXX
    * API模板
2. EF Core
   * Tools
   * Sqlite
3. 建立类
   * 体现关系
   * 建立Data文件夹。建立ApplicationDbContext
``` C#
﻿using System;
using Microsoft.EntityFrameworkCore;
using Routine.Api.Entities;

namespace Routine.Api.Data
{
    public class RoutineDbContext: DbContext
    {
        public RoutineDbContext(DbContextOptions<RoutineDbContext> options)
            : base(options)
        {
            
        }

        public DbSet<Company> Companies { get; set; }
        public DbSet<Employee> Employees { get; set; }

        protected override void OnModelCreating(ModelBuilder modelBuilder)
        {
            modelBuilder.Entity<Company>()
                .Property(x => x.Name).IsRequired().HasMaxLength(100);
            modelBuilder.Entity<Company>()
                .Property(x => x.Country).HasMaxLength(50);
            modelBuilder.Entity<Company>()
                .Property(x => x.Industry).HasMaxLength(50);
            modelBuilder.Entity<Company>()
                .Property(x => x.Product).HasMaxLength(100);
            modelBuilder.Entity<Company>()
                .Property(x => x.Introduction).HasMaxLength(500);

            modelBuilder.Entity<Employee>()
                .Property(x => x.EmployeeNo).IsRequired().HasMaxLength(10);
            modelBuilder.Entity<Employee>()
                .Property(x => x.FirstName).IsRequired().HasMaxLength(50);
            modelBuilder.Entity<Employee>()
                .Property(x => x.LastName).IsRequired().HasMaxLength(50);

            modelBuilder.Entity<Employee>()
                .HasOne(x => x.Company)
                .WithMany(x => x.Employees)
                .HasForeignKey(x => x.CompanyId)
                .OnDelete(DeleteBehavior.Cascade);

            modelBuilder.Entity<Company>().HasData(
                new Company
                {
                    Id = Guid.Parse("bbdee09c-089b-4d30-bece-44df5923716c"),
                    Name = "Microsoft",
                    Introduction = "Great Company",
                    Country = "USA",
                    Industry = "Software",
                    Product = "Software"
                },
                new Company
                {
                    Id = Guid.Parse("6fb600c1-9011-4fd7-9234-881379716440"),
                    Name = "Google",
                    Introduction = "Don't be evil",
                    Country = "USA",
                    Industry = "Internet",
                    Product = "Software"
                },
                new Company
                {
                    Id = Guid.Parse("5efc910b-2f45-43df-afae-620d40542853"),
                    Name = "Alipapa",
                    Introduction = "Fubao Company",
                    Country = "China",
                    Industry = "Internet",
                    Product = "Software"
                },
                new Company
                {
                    Id = Guid.Parse("bbdee09c-089b-4d30-bece-44df59237100"),
                    Name = "Tencent",
                    Introduction = "From Shenzhen",
                    Country = "China",
                    Industry = "ECommerce",
                    Product = "Software"
                },
                new Company
                {
                    Id = Guid.Parse("6fb600c1-9011-4fd7-9234-881379716400"),
                    Name = "Baidu",
                    Introduction = "From Beijing",
                    Country = "China",
                    Industry = "Internet",
                    Product = "Software"
                },
                new Company
                {
                    Id = Guid.Parse("5efc910b-2f45-43df-afae-620d40542800"),
                    Name = "Adobe",
                    Introduction = "Photoshop?",
                    Country = "USA",
                    Industry = "Software",
                    Product = "Software"
                },
                new Company
                {
                    Id = Guid.Parse("bbdee09c-089b-4d30-bece-44df59237111"),
                    Name = "SpaceX",
                    Introduction = "Wow",
                    Country = "USA",
                    Industry = "Technology",
                    Product = "Rocket"
                },
                new Company
                {
                    Id = Guid.Parse("6fb600c1-9011-4fd7-9234-881379716411"),
                    Name = "AC Milan",
                    Introduction = "Football Club",
                    Country = "Italy",
                    Industry = "Football",
                    Product = "Football Match"
                },
                new Company
                {
                    Id = Guid.Parse("5efc910b-2f45-43df-afae-620d40542811"),
                    Name = "Suning",
                    Introduction = "From Jiangsu",
                    Country = "China",
                    Industry = "ECommerce",
                    Product = "Goods"
                },
                new Company
                {
                    Id = Guid.Parse("bbdee09c-089b-4d30-bece-44df59237122"),
                    Name = "Twitter",
                    Introduction = "Blocked",
                    Country = "USA",
                    Industry = "Internet",
                    Product = "Tweets"
                },
                new Company
                {
                    Id = Guid.Parse("6fb600c1-9011-4fd7-9234-881379716422"),
                    Name = "Youtube",
                    Introduction = "Blocked",
                    Country = "USA",
                    Industry = "Internet",
                    Product = "Videos"
                },
                new Company
                {
                    Id = Guid.Parse("5efc910b-2f45-43df-afae-620d40542822"),
                    Name = "360",
                    Introduction = "- -",
                    Country = "China",
                    Industry = "Security",
                    Product = "Security Product"
                },
                new Company
                {
                    Id = Guid.Parse("bbdee09c-089b-4d30-bece-44df59237133"),
                    Name = "Jingdong",
                    Introduction = "Brothers",
                    Country = "China",
                    Industry = "ECommerce",
                    Product = "Goods"
                },
                new Company
                {
                    Id = Guid.Parse("6fb600c1-9011-4fd7-9234-881379716433"),
                    Name = "NetEase",
                    Introduction = "Music?",
                    Country = "China",
                    Industry = "Internet",
                    Product = "Songs"
                },
                new Company
                {
                    Id = Guid.Parse("5efc910b-2f45-43df-afae-620d40542833"),
                    Name = "Amazon",
                    Introduction = "Store",
                    Country = "USA",
                    Industry = "ECommerce",
                    Product = "Books"
                },
                new Company
                {
                    Id = Guid.Parse("bbdee09c-089b-4d30-bece-44df59237144"),
                    Name = "AOL",
                    Introduction = "Not Exists?",
                    Country = "USA",
                    Industry = "Internet",
                    Product = "Website"
                },
                new Company
                {
                    Id = Guid.Parse("6fb600c1-9011-4fd7-9234-881379716444"),
                    Name = "Yahoo",
                    Introduction = "Who?",
                    Country = "USA",
                    Industry = "Internet",
                    Product = "Mail"
                },
                new Company
                {
                    Id = Guid.Parse("5efc910b-2f45-43df-afae-620d40542844"),
                    Name = "Firefox",
                    Introduction = "Is it a company?",
                    Country = "USA",
                    Industry = "Internet",
                    Product = "Browser"
                });

            modelBuilder.Entity<Employee>().HasData(
                new Employee
                {
                    Id = Guid.Parse("4b501cb3-d168-4cc0-b375-48fb33f318a4"),
                    CompanyId = Guid.Parse("bbdee09c-089b-4d30-bece-44df5923716c"),
                    DateOfBirth = new DateTime(1976, 1, 2),
                    EmployeeNo = "MSFT231",
                    FirstName = "Nick",
                    LastName = "Carter",
                    Gender = Gender.男
                },
                new Employee
                {
                    Id = Guid.Parse("7eaa532c-1be5-472c-a738-94fd26e5fad6"),
                    CompanyId = Guid.Parse("bbdee09c-089b-4d30-bece-44df5923716c"),
                    DateOfBirth = new DateTime(1981, 12, 5),
                    EmployeeNo = "MSFT245",
                    FirstName = "Vince",
                    LastName = "Carter",
                    Gender = Gender.男
                },
                new Employee
                {
                    Id = Guid.Parse("72457e73-ea34-4e02-b575-8d384e82a481"),
                    CompanyId = Guid.Parse("6fb600c1-9011-4fd7-9234-881379716440"),
                    DateOfBirth = new DateTime(1986, 11, 4),
                    EmployeeNo = "G003",
                    FirstName = "Mary",
                    LastName = "King",
                    Gender = Gender.女
                },
                new Employee
                {
                    Id = Guid.Parse("7644b71d-d74e-43e2-ac32-8cbadd7b1c3a"),
                    CompanyId = Guid.Parse("6fb600c1-9011-4fd7-9234-881379716440"),
                    DateOfBirth = new DateTime(1977, 4, 6),
                    EmployeeNo = "G097",
                    FirstName = "Kevin",
                    LastName = "Richardson",
                    Gender = Gender.男
                },
                new Employee
                {
                    Id = Guid.Parse("679dfd33-32e4-4393-b061-f7abb8956f53"),
                    CompanyId = Guid.Parse("5efc910b-2f45-43df-afae-620d40542853"),
                    DateOfBirth = new DateTime(1967, 1, 24),
                    EmployeeNo = "A009",
                    FirstName = "卡",
                    LastName = "里",
                    Gender = Gender.女
                },
                new Employee
                {
                    Id = Guid.Parse("1861341e-b42b-410c-ae21-cf11f36fc574"),
                    CompanyId = Guid.Parse("5efc910b-2f45-43df-afae-620d40542853"),
                    DateOfBirth = new DateTime(1957, 3, 8),
                    EmployeeNo = "A404",
                    FirstName = "Not",
                    LastName = "Man",
                    Gender = Gender.男
                });
        }
    }
}

```
4. 建立Services文件夹
    * 建立仓储接口
    * 实现接口
``` C#
using System;
using System.Collections.Generic;
using System.Linq;
using System.Threading.Tasks;
using Microsoft.EntityFrameworkCore;
using Routine.Api.Data;
using Routine.Api.DtoParameters;
using Routine.Api.Entities;
using Routine.Api.Helpers;
using Routine.Api.Models;

namespace Routine.Api.Services
{
    public class CompanyRepository : ICompanyRepository
    {
        private readonly RoutineDbContext _context;

        public CompanyRepository(RoutineDbContext context)
        {
            _context = context ?? throw new ArgumentNullException(nameof(context));
        }

        public async Task<PagedList<Company>> GetCompaniesAsync(CompanyDtoParameters parameters)
        {
            if (parameters == null)
            {
                throw new ArgumentNullException(nameof(parameters));
            }

            var queryExpression = _context.Companies as IQueryable<Company>;

            if (!string.IsNullOrWhiteSpace(parameters.CompanyName))
            {
                parameters.CompanyName = parameters.CompanyName.Trim();
                queryExpression = queryExpression.Where(x => x.Name == parameters.CompanyName);
            }

            if (!string.IsNullOrWhiteSpace(parameters.SearchTerm))
            {
                parameters.SearchTerm = parameters.SearchTerm.Trim();
                queryExpression = queryExpression.Where(x => x.Name.Contains(parameters.SearchTerm) ||
                                                             x.Introduction.Contains(parameters.SearchTerm));
            }

            var mappingDictionary = _propertyMappingService.GetPropertyMapping<CompanyDto, Company>();

            queryExpression = queryExpression.ApplySort(parameters.OrderBy, mappingDictionary);

            return await PagedList<Company>.CreateAsync(queryExpression, parameters.PageNumber, parameters.PageSize);
        }

        public async Task<Company> GetCompanyAsync(Guid companyId)
        {
            if (companyId == Guid.Empty)
            {
                throw new ArgumentNullException(nameof(companyId));
            }

            return await _context.Companies
                .FirstOrDefaultAsync(x => x.Id == companyId);
        }

        public async Task<IEnumerable<Company>>
            GetCompaniesAsync(IEnumerable<Guid> companyIds)
        {
            if (companyIds == null)
            {
                throw new ArgumentNullException(nameof(companyIds));
            }

            return await _context.Companies
                .Where(x => companyIds.Contains(x.Id))
                .OrderBy(x => x.Name)
                .ToListAsync();
        }

        public void AddCompany(Company company)
        {
            if (company == null)
            {
                throw new ArgumentNullException(nameof(company));
            }

            company.Id = Guid.NewGuid();

            if (company.Employees != null)
            {
                foreach (var employee in company.Employees)
                {
                    employee.Id = Guid.NewGuid();
                }
            }

            _context.Companies.Add(company);
        }

        public void UpdateCompany(Company company)
        {
            // _context.Entry(company).State = EntityState.Modified;
        }

        public void DeleteCompany(Company company)
        {
            if (company == null)
            {
                throw new ArgumentNullException(nameof(company));
            }

            _context.Companies.Remove(company);
        }

        public async Task<bool> CompanyExistsAsync(Guid companyId)
        {
            if (companyId == Guid.Empty)
            {
                throw new ArgumentNullException(nameof(companyId));
            }

            return await _context.Companies.AnyAsync(x => x.Id == companyId);
        }

        public async Task<IEnumerable<Employee>> GetEmployeesAsync(Guid companyId,
            EmployeeDtoParameters parameters)
        {
            if (companyId == Guid.Empty)
            {
                throw new ArgumentNullException(nameof(companyId));
            }

            var items = _context.Employees.Where(x => x.CompanyId == companyId);

            if (!string.IsNullOrWhiteSpace(parameters.Gender))
            {
                parameters.Gender = parameters.Gender.Trim();
                var gender = Enum.Parse<Gender>(parameters.Gender);

                items = items.Where(x => x.Gender == gender);
            }

            if (!string.IsNullOrWhiteSpace(parameters.Q))
            {
                parameters.Q = parameters.Q.Trim();

                items = items.Where(x => x.EmployeeNo.Contains(parameters.Q)
                                         || x.FirstName.Contains(parameters.Q)
                                         || x.LastName.Contains(parameters.Q));
            }

            var mappingDictionary = _propertyMappingService.GetPropertyMapping<EmployeeDto, Employee>();

            items = items.ApplySort(parameters.OrderBy, mappingDictionary);

            return await items.ToListAsync();
        }

        public async Task<Employee> GetEmployeeAsync(Guid companyId, Guid employeeId)
        {
            if (companyId == Guid.Empty)
            {
                throw new ArgumentNullException(nameof(companyId));
            }

            if (employeeId == Guid.Empty)
            {
                throw new ArgumentNullException(nameof(employeeId));
            }

            return await _context.Employees
                .Where(x => x.CompanyId == companyId && x.Id == employeeId)
                .FirstOrDefaultAsync();
        }

        public void AddEmployee(Guid companyId, Employee employee)
        {
            if (companyId == Guid.Empty)
            {
                throw new ArgumentNullException(nameof(companyId));
            }

            if (employee == null)
            {
                throw new ArgumentNullException(nameof(employee));
            }

            employee.CompanyId = companyId;
            _context.Employees.Add(employee);
        }

        public void UpdateEmployee(Employee employee)
        {
            // _context.Entry(employee).State = EntityState.Modified;
        }

        public void DeleteEmployee(Employee employee)
        {
            _context.Employees.Remove(employee);
        }

        public async Task<bool> SaveAsync()
        {
            return await _context.SaveChangesAsync() >= 0;
        }
    }
}
```

5. StartUp里注册服务
``` C#
services.AddScoped<IBookRepository, BookRepository>();
```

6. 迁移数据库


# 二、REST简介
# 三、API的对外合约
1. 创建Controller
    * 命名复数
    * 继承于ControllerBase
2. 加标签
``` C#
[ApiController]
[Route("api/books")]
public class BooksController : ControllerBase
{
    private readonly IBookRepository _bookRepository;

    public BooksController(IBookRepository bookRepository)
    {
        _bookRepository = bookRepository ?? throw new ArgumentNullException(nameof(bookRepository));
    }

    [HttpGet]
    public async Task<IActionResult> GetBooksAsync()
    {
        return new JsonResult(await _bookRepository.GetBooksAsync());
    }
}
```

# 四、HTTP方法

# 五、HTTP状态码

# 六、写代码：状态码、路由

# 七、内容协商

# 八、写代码：内容协商
``` C#
services.AddControllers(setup =>
            {
                setup.ReturnHttpNotAcceptable = true;
            }).AddXmlDataContractSerializerFormatters();
```

# 九、Entity Model VS 面向外部的Model

# 十、写代码：Entity Model VS 面向外部的Model
1. 建立Models文件夹
2. Controller里赋值

# 十一、Action Result<T>

# 十二、添加AutoMapper
1. Nuget (AutoMapper.Extensions.Microsoft.DependencyInjection)
2. StartUp里注册
``` C#
services.AddAutoMapper(AppDomain.CurrentDomain.GetAssemblies());
```
3. 建立Profiles文件夹和类
``` C#
public class BookProfile : Profile
    {
        public BookProfile()
        {
            CreateMap<Book, BookDto>();

            //CreateMap<Book, BookDto>().ForMember(dest => dest.Author, opt => opt.MapFrom(src => src.Author));
        }
    }
```
4. Controller里注入
``` C#
[HttpGet]
public async Task<ActionResult<IEnumerable<BookDto>>> GetBooksAsync()
{
    var books = await _bookRepository.GetBooksAsync();
    var bookDtos = _mapper.Map<IEnumerable<BookDto>>(books);
    return Ok(bookDtos);
}
```

# 十三、获取父子关系的资源
1. 创建新的Controller
* 公司的员工写入

# 十四、

# 十五、处理服务器端故障
 1. 在StartUp里修改
``` C#
if (env.IsDevelopment())
            {
                app.UseDeveloperExceptionPage();
            }
            else
            {
                app.UseExceptionHandler(appBuilder =>
                {
                    app.Run(async context =>
                    {
                        context.Response.StatusCode = 500;
                        await context.Response.WriteAsync("Unexcept Error!");
                    });
                });
            }
```

# 十六、HTTP HEAD
1. [HttpHead]

# 十七、过滤和搜索


# 十九、查询参数
1. 新建文件夹 DtoParameters
2. 建立类BookDtoParameters
3. [FormQuery]


# 二十、安全性和幂等性


