# 存储策略

## 获取策略列表

**接口地址**
`GET /strategies`

**说明**
获取系统中所有可用的存储策略列表，支持按关键字筛选。

**请求示例**
```bash
curl -X GET "https://img.yuncen.top/api/v1/strategies" \
  -H "Authorization: Bearer 1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5" \
  -H "Accept: application/json"
```

**请求参数（Query）**

| 参数名    | 类型   | 必填 | 说明                   |
|-----------|--------|------|------------------------|
| keyword   | string | 否   | 筛选关键字，模糊匹配策略名称 |

**请求 Headers**

| 字段           | 说明                     |
|----------------|--------------------------|
| Authorization  | Bearer Token（必填）     |
| Accept         | `application/json`（必填）|

**成功响应（200）**
```json
{
  "status": true,
  "message": "获取策略列表成功",
  "data": {
    "strategies": [
      {
        "id": 1,
        "name": "本地存储",
        "description": "将文件存储在服务器本地磁盘",
        "driver": "local",
        "is_default": true,
        "created_at": "2024-01-01T00:00:00.000000Z"
      },
      {
        "id": 2,
        "name": "阿里云OSS",
        "description": "使用阿里云对象存储服务",
        "driver": "oss",
        "is_default": false,
        "created_at": "2024-03-15T10:30:00.000000Z"
      },
      {
        "id": 3,
        "name": "腾讯云COS",
        "description": "使用腾讯云对象存储服务",
        "driver": "cos",
        "is_default": false,
        "created_at": "2024-05-20T14:20:00.000000Z"
      }
    ]
  }
}
```

**响应参数说明**

| 字段                    | 类型      | 说明                           |
|-------------------------|-----------|--------------------------------|
| status                  | boolean   | 状态，true 或 false            |
| message                 | string    | 描述信息                       |
| data                    | object    | 数据                           |
| data.strategies         | object[]  | 策略数据数组                   |
| data.strategies[].id    | integer   | 策略 ID                        |
| data.strategies[].name  | string    | 策略名称                       |
| data.strategies[].description | string | 策略描述                     |
| data.strategies[].driver | string   | 存储驱动类型                   |
| data.strategies[].is_default | boolean | 是否为默认策略              |
| data.strategies[].created_at | string | 创建时间（yyyy-MM-dd HH:mm:ss）|

**错误响应**

- `401 Unauthorized`：Token 无效或缺失
- `403 Forbidden`：权限不足，无法访问此功能
- `500 Internal Server Error`：服务器内部错误