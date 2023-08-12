# 路由/Route

```php
<?php 
use dove\Route;
// 然后使用方法
Route::method();
```

---

# 模块配置

`./config/AccessControl.php`
```php
// 默认执行文件
'default_file' => 'index.php',

// 禁止被访问的目录名，被禁止后访问会返回框架404错误
'padlock' => [],

// TODO 指定路径绑定域名
'band' => [
    // test.xcenadmin.top => app/abc/index.php
    // test.xcenadmin.top/abc => app/abc/abc.php
    'test' => 'abc',

    // xcenadmin.top => app/index.php
    // www.xcenadmin.top => app/index.php
    '__INDEX__' => '',
],
```

---
