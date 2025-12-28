# 相册管理

## 获取相册列表

**接口地址**
`GET /albums`

**说明**
获取当前用户的相册列表，支持分页、排序和关键字搜索。

**请求示例**
```bash
curl -X GET "https://img.yuncen.top/api/v1/albums?page=1&order=newest&keyword=旅行" \
  -H "Authorization: Bearer 1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5" \
  -H "Accept: application/json"
```

**请求参数（Query）**

| 参数名    | 类型   | 必填 | 说明                                                                 |
|-----------|--------|------|----------------------------------------------------------------------|
| page      | integer| 否   | 页码（默认为 1）                                                     |
| order     | string | 否   | 排序方式：newest=最新（默认），earliest=最早，most=图片最多，least=图片最少 |
| keyword   | string | 否   | 关键字，用于搜索相册名称或简介                                       |

**请求 Headers**

| 字段           | 说明                     |
|----------------|--------------------------|
| Authorization  | Bearer Token（必填）     |
| Accept         | `application/json`（必填）|

**成功响应（200）**
```json
{
  "status": true,
  "message": "获取相册列表成功",
  "data": {
    "current_page": 1,
    "last_page": 2,
    "per_page": 10,
    "total": 15,
    "data": [
      {
        "id": 1,
        "name": "旅行相册",
        "intro": "记录我的旅行足迹",
        "image_num": 25,
        "created_at": "2025-03-01 10:30:00",
        "updated_at": "2025-03-28 15:45:00"
      },
      {
        "id": 2,
        "name": "工作项目",
        "intro": "项目相关截图和图片",
        "image_num": 12,
        "created_at": "2025-02-15 09:20:00",
        "updated_at": "2025-03-25 11:10:00"
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
| data.total                              | integer   | 相册总数量                     |
| data.data                               | object[]  | 相册列表数组                   |
| data.data[].id                          | integer   | 相册自增 ID                    |
| data.data[].name                        | string    | 相册名称                       |
| data.data[].intro                       | string    | 相册简介                       |
| data.data[].image_num                   | integer   | 相册内图片数量                 |
| data.data[].created_at                  | string    | 相册创建时间（yyyy-MM-dd HH:mm:ss）|
| data.data[].updated_at                  | string    | 相册最后更新时间（yyyy-MM-dd HH:mm:ss）|

**错误响应**

- `401 Unauthorized`：Token 无效或缺失
- `500 Internal Server Error`：服务器内部错误

---

## 删除相册

**接口地址**
`DELETE /albums/{id}`

**说明**
根据相册 ID 删除指定相册及其包含的所有图片。

**请求示例**
```bash
curl -X DELETE "https://img.yuncen.top/api/v1/albums/1" \
  -H "Authorization: Bearer 1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5" \
  -H "Accept: application/json"
```

**请求参数（Params）**

| 参数名     | 类型   | 必填 | 说明         |
|------------|--------|------|--------------|
| id<span class="text-red-500">*</span> | integer | 是   | 相册自增 ID  |

**请求 Headers**

| 字段           | 说明                     |
|----------------|--------------------------|
| Authorization  | Bearer Token（必填）     |
| Accept         | `application/json`（必填）|

**成功响应（200）**
```json
{
  "status": true,
  "message": "相册删除成功",
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
- `403 Forbidden`：无权限删除该相册
- `404 Not Found`：相册不存在
- `500 Internal Server Error`：服务器内部错误