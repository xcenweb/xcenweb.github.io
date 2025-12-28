# 图片管理

## 上传图片

**接口地址**
`POST /upload`

**说明**
上传图片文件到服务器，支持选择存储策略。

**请求示例**
```bash
curl -X POST https://img.yuncen.top/api/v1/upload \
  -H "Authorization: Bearer 1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5" \
  -H "Accept: application/json" \
  -H "Content-Type: multipart/form-data" \
  -F "file=@/path/to/your/image.jpg" \
  -F "strategy_id=2"
```

**请求 Headers**

| 字段             | 类型   | 必填 | 说明                           |
|------------------|--------|------|--------------------------------|
| Authorization    | string | 否   | Bearer Token（游客上传可选）   |
| Accept           | string | 是   | 必须设为 `application/json`    |
| Content-Type     | string | 是   | 必须设为 `multipart/form-data` |

**请求参数（Body）**

| 参数名       | 类型 | 必填 | 说明                         |
|--------------|------|------|------------------------------|
| file<span class="text-red-500">*</span> | file | 是   | 图片文件                     |
| strategy_id  | integer | 否   | 存储策略 ID（默认使用系统默认策略） |

> 📌 提示：若不提供 `Authorization`，将作为游客上传，可能受到配额限制。

**成功响应（200）**
```json
{
  "status": true,
  "message": "图片上传成功",
  "data": {
    "key": "abc123def456",
    "name": "image_abc123.jpg",
    "pathname": "2025/03/28/image_abc123.jpg",
    "origin_name": "original_image.jpg",
    "size": 1024.5,
    "mimetype": "image/jpeg",
    "extension": "jpg",
    "md5": "d41d8cd98f00b204e9800998ecf8427e",
    "sha1": "da39a3ee5e6b4b0d3255bfef95601890afd80709",
    "links": {
      "url": "https://img.yuncen.top/upload/2025/03/28/image_abc123.jpg",
      "html": "<img src='https://img.yuncen.top/upload/2025/03/28/image_abc123.jpg' alt='image_abc123.jpg'>",
      "bbcode": "[img]https://img.yuncen.top/upload/2025/03/28/image_abc123.jpg[/img]",
      "markdown": "![image_abc123.jpg](https://img.yuncen.top/upload/2025/03/28/image_abc123.jpg)",
      "markdown_with_link": "[![image_abc123.jpg](https://img.yuncen.top/upload/2025/03/28/image_abc123.jpg)](https://img.yuncen.top/upload/2025/03/28/image_abc123.jpg)",
      "thumbnail_url": "https://img.yuncen.top/upload/2025/03/28/image_abc123_thumb.jpg"
    }
  }
}
```

**响应参数说明**

| 字段                                    | 类型      | 说明                           |
|-----------------------------------------|-----------|--------------------------------|
| status                                  | boolean   | 状态，true 或 false            |
| message                                 | string    | 描述信息                       |
| data                                    | object    | 数据                           |
| data.key                                | string    | 图片唯一密钥                   |
| data.name                               | string    | 图片名称                       |
| data.pathname                           | string    | 图片路径名                     |
| data.origin_name                        | string    | 图片原始名称                   |
| data.size                               | float     | 图片大小，单位 KB              |
| data.mimetype                           | string    | 图片 MIME 类型                 |
| data.extension                          | string    | 图片扩展名                     |
| data.md5                                | string    | 图片 MD5 值                    |
| data.sha1                               | string    | 图片 SHA1 值                   |
| data.links                              | object    | 图片链接                       |
| data.links.url                          | string    | 图片访问 URL                   |
| data.links.html                         | string    | HTML 格式引用                  |
| data.links.bbcode                       | string    | BBCode 格式引用                |
| data.links.markdown                     | string    | Markdown 格式引用              |
| data.links.markdown_with_link           | string    | 带链接的 Markdown 格式引用     |
| data.links.thumbnail_url                | string    | 缩略图 URL                     |

**错误响应**

- `401 Unauthorized`：Token 无效（当需要登录时）
- `413 Request Entity Too Large`：文件大小超出限制
- `422 Unprocessable Entity`：文件格式不支持或缺少必填参数
- `429 Too Many Requests`：超出上传配额
- `500 Internal Server Error`：服务器内部错误

---

## 获取图片列表

**接口地址**
`GET /images`

**说明**
获取当前用户上传的图片列表，支持分页、排序、权限筛选和关键字搜索。

**请求示例**
```bash
curl -X GET "https://img.yuncen.top/api/v1/images?page=1&order=newest&permission=public&keyword=风景" \
  -H "Authorization: Bearer 1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5" \
  -H "Accept: application/json"
```

**请求参数（Query）**

| 参数名      | 类型   | 必填 | 说明                                                                 |
|-------------|--------|------|----------------------------------------------------------------------|
| page        | integer| 否   | 页码（默认为 1）                                                     |
| order       | string | 否   | 排序方式：newest=最新（默认），earliest=最早，utmost=最大，least=最小 |
| permission  | string | 否   | 权限：public=公开，private=私有（默认全部）                           |
| album_id    | integer| 否   | 相册 ID，用于筛选指定相册的图片                                       |
| keyword     | string | 否   | 关键字，用于搜索图片名称或路径                                       |

**请求 Headers**

| 字段           | 说明                     |
|----------------|--------------------------|
| Authorization  | Bearer Token（必填）     |
| Accept         | `application/json`（必填）|

**成功响应（200）**
```json
{
  "status": true,
  "message": "获取图片列表成功",
  "data": {
    "current_page": 1,
    "last_page": 5,
    "per_page": 10,
    "total": 45,
    "data": [
      {
        "key": "xyz789",
        "name": "sunset_view.jpg",
        "origin_name": "sunset.jpg",
        "pathname": "2025/03/27/sunset_view.jpg",
        "size": 2048.0,
        "width": 1920,
        "height": 1080,
        "md5": "a1b2c3d4e5f6...",
        "sha1": "f6e5d4c3b2a1...",
        "human_date": "2 小时前",
        "date": "2025-03-28 10:30:00",
        "links": {
          "url": "https://img.yuncen.top/upload/2025/03/27/sunset_view.jpg",
          "thumbnail_url": "https://img.yuncen.top/upload/2025/03/27/sunset_view_thumb.jpg"
        }
      }
    ]
  }
}
```

**响应参数说明**

| 字段                                    | 类型      | 说明                           |
|-----------------------------------------|-----------|--------------------------------|
| status                                  | boolean   | 状态，true 或 false            |
| message                                 | string    | 描述信息                       |
| data                                    | object    | 数据                           |
| data.current_page                       | integer   | 当前所在页码                   |
| data.last_page                          | integer   | 最后一页页码                   |
| data.per_page                           | integer   | 每页展示数据数量               |
| data.total                              | integer   | 图片总数量                     |
| data.data                               | object[]  | 图片列表数组                   |
| data.data[].key                         | string    | 图片唯一密钥                   |
| data.data[].name                        | string    | 图片名称                       |
| data.data[].origin_name                 | string    | 图片原始名称                   |
| data.data[].pathname                    | string    | 图片路径名                     |
| data.data[].size                        | float     | 图片大小，单位 KB              |
| data.data[].width                       | integer   | 图片宽度                       |
| data.data[].height                      | integer   | 图片高度                       |
| data.data[].md5                         | string    | 图片 MD5 值                    |
| data.data[].sha1                        | string    | 图片 SHA1 值                   |
| data.data[].human_date                  | string    | 上传时间（友好格式）           |
| data.data[].date                        | string    | 上传日期（yyyy-MM-dd HH:mm:ss）|
| data.data[].links                       | object    | 图片链接                       |
| data.data[].links.url                   | string    | 图片访问 URL                   |
| data.data[].links.thumbnail_url         | string    | 缩略图 URL                     |

**错误响应**

- `401 Unauthorized`：Token 无效或缺失
- `500 Internal Server Error`：服务器内部错误

---

## 删除图片

**接口地址**
`DELETE /images/{key}`

**说明**
根据图片密钥删除指定图片。

**请求示例**
```bash
curl -X DELETE "https://img.yuncen.top/api/v1/images/abc123def456" \
  -H "Authorization: Bearer 1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5" \
  -H "Accept: application/json"
```

**请求参数（Params）**

| 参数名     | 类型   | 必填 | 说明         |
|------------|--------|------|--------------|
| key<span class="text-red-500">*</span> | string | 是   | 图片唯一密钥 |

**请求 Headers**

| 字段           | 说明                     |
|----------------|--------------------------|
| Authorization  | Bearer Token（必填）     |
| Accept         | `application/json`（必填）|

**成功响应（200）**
```json
{
  "status": true,
  "message": "图片删除成功",
  "data": {}
}
```

**响应参数说明**

| 字段    | 类型    | 说明               |
|---------|---------|--------------------|
| status  | boolean | 状态，true 或 false|
| message | string  | 描述信息           |
| data    | object  | 数据（通常为空）   |

**错误响应**

- `401 Unauthorized`：Token 无效或缺失
- `403 Forbidden`：无权限删除该图片
- `404 Not Found`：图片不存在
- `500 Internal Server Error`：服务器内部错误
