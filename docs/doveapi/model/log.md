# 日志/Log

[](../_include/not-hardcode.md ':include')

```php
<?php 
use dove\Log;
// 然后使用方法
Log::method();
```

---

# 模块配置

`./config/dove.php`
```php
    // 自定义log 相关预设
    // ['类型，默认unknown','目录，默认unknown','记录log的文件名，默认unknown']
    'log_preset' => [
        'eg' => ['Bad','test','test_log'],
    ],
```

---

# static::save

该方法用于保存日志。

```php
  public static function save($add = [], $path = 'unknown', $logname = 'unknown', $type = 'unknown') 
```


### 参数

- `$add` (数组)：需要添加到日志中的额外信息，键值对的形式。
- `$path` (字符串)：日志保存的路径，默认为'unknown'。
- `$logname` (字符串)：日志文件的名称，默认为'unknown'。
- `$type` (字符串)：日志类型，默认为'unknown'。 


### 返回值

- 如果成功保存日志，则返回布尔值 `true`。
- 如果配置有误或保存失败，则直接返回布尔值 `false`。

### 例子

```php
Log::save(['user_id' => 123, 'action' => 'login'], 'auth', 'auth_log', 'login');
```

此示例将会保存一条包含用户ID和登录动作的日志到指定的日志文件。

---

# static::saveErr

该方法用于保存错误日志。 

```php
public static function saveErr($errFile = '未知', $errInfo = '未知', $remarks = '无')
```

### 参数

- `$errFile` (字符串)：发生错误的文件路径，默认为'未知'。
- `$errInfo` (字符串)：错误的详细信息，默认为'未知'。
- `$remarks` (字符串)：错误的备注信息，默认为'无'。 

### 返回值 

- 如果成功保存错误日志，则返回 `true`。
- 如果配置不支持保存错误日志，则直接返回 `true`。

### 示例

```php
Log::saveErr('path/to/file.php', 'Undefined variable: foo', '处理用户输入时发生错误'); 
```

此示例将会保存一条包含文件路径、错误信息和备注的错误日志到指定的日志文件。

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

此示例将会将文本内容写入指定的文件。