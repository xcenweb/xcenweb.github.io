# 日志/Log

<!-- [](../_include/not-hardcode.md ':include') -->

```php
<?php 
use dove\Log;
// 然后使用方法
Log::method();
```

---

# 模块配置

`./config/log.php`

```php
    // log开关，关闭后所有log将不会被记录（包括debug_log）, Log::save() 只返回 true
    'log_switch' => true,
```

---

# static::add

该方法用于添加一条日志。

```php
  public static function add($add = [], $type = 'NOTE') 
```


### 参数

- `$add` (数组)：需要添加到日志中的额外信息，键值对的形式。
- `$type` (字符串)：日志类型，默认为'NOTE'。 


### 返回值

- 如果成功保存日志，则返回布尔值 `true`。
- 如果配置有误或保存失败，则直接返回布尔值 `false`。

### 例子

此示例将会保存一条包含用户ID和登录动作的日志到指定的日志文件。

```php
Log::add(['user_id' => 123, 'action' => 'login'], 'login');
// [login][1970-01-01 00:00:00][127.0.0.1]
// user_id: 123
// action: login
```

---

# static::debug

该方法用于 `dove\Debug` 保存错误日志。 

```php
public static function debug($errFile = 'null', $errInfo = 'false', $remarks = 'false')
```

### 参数

- `$errFile` (字符串)：发生错误的文件路径，默认为 'null'。
- `$errInfo` (字符串)：错误的详细信息，默认为 'false'。
- `$remarks` (字符串)：错误的备注信息，默认为 'false'。 

### 返回值 

- 如果成功保存错误日志，则返回 `true`。
- 如果配置不支持保存错误日志，则直接返回 `true`。

### 示例

此示例将会保存一条包含文件路径、错误信息和备注的错误日志到指定的日志文件。

```php
Log::debug('path/to/file.php', 'Undefined variable: foo', '处理用户输入时发生错误'); 
```

---

# self::write

**[内部方法]** 该方法用于将文本内容写入文件。

```php
private static function write($text, $path, $file)
```

### 参数
- `$text` (字符串)：要写入文件的文本内容。
- `$path` (字符串)：文件保存的路径。
- `$file` (字符串)：文件的名称。

### 返回值
- 如果成功将文本写入文件，则返回写入的字节数。 
- 如果无法写入文件或发生错误，则返回 `false`。

### 示例

```php
$text = "This is some text to write into the file.";
$path = "/path/to/directory";
$file = "example.txt";
$result = Log::write($text, $path, $file);
``` 

此示例将会将文本内容插入指定的文件。