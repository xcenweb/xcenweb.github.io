# 结构

欢迎使用该框架！以下是关于框架目录结构的介绍

# 结构图

```text
wwwroot (框架部署的目录)
├─app          应用
│  ├─ __begin.php 起始文件
│  └─ __coda.php  结束文件
│ 
├─config       配置
│  ├─ AccessControl.php
│  ├─ api.php
│  ├─ cache.php
│  ├─ db.php
│  ├─ dove.php
│  ├─ filter.php
│  └─ ...
│
├─data         数据文件存储
│  ├─cache       缓存
│  │  └─ file       filecacheClass 默认文件夹
│  │
│  └─tpl         页面模板
│      └─ debug     报错页面模板
│
├─extend       自定义拓展类
│
├─public       运行目录
│  └─ static    静态文件目录
│
├─runtime      运行时目录
│  └─ log       日志存储
│
└─vendor       composer目录
   └─ ...
```

# 详细内容

- `app`：应用目录，存放应用程序相关代码文件。
  - `__begin.php`：起始文件，在应用程序执行之前运行的代码可以放在这里。
  - `__coda.php`：结束文件，在应用程序执行之后运行的代码可以放在这里。

- `config`：配置目录，存放框架和应用程序的配置文件。
  - `AccessControl.php`：访问控制配置文件。
  - `api.php`：API 相关配置文件。
  - `cache.php`：缓存配置文件。
  - `db.php`：数据库配置文件。
  - `dove.php`：框架配置文件。
  - `filter.php`：过滤器配置文件。
  - ...

- `data`：数据文件存储目录。
  - `cache`：缓存目录，存放缓存文件。
    - `file`：默认的文件缓存文件夹。
  - `tpl`：页面模板目录，存放页面模板文件。
    - `debug`：报错页面模板目录。

- `extend`：自定义拓展类目录，可以将自定义的类文件放在这里。

- `public`：运行目录，公开访问的文件应该放在此处。
  - `static`：静态文件目录，存放静态资源文件，如 CSS、JavaScript 和图片文件等。

- `runtime`：运行时目录，存放运行时生成的文件。
  - `log`：日志存储目录，存放框架和应用程序的日志文件。

- `vendor`：Composer 目录，存放 Composer 安装的依赖包及自动生成的类文件等。