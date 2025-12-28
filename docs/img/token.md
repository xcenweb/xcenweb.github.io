# 授权管理

## 生成 Token

**接口地址**
`POST /auth/token`

**请求示例**
```bash
curl -X POST https://img.yuncen.top/api/v1/auth/token \
  -H "Accept: application/json" \
  -d "email=your_email@example.com" \
  -d "password=your_password"
```

**请求参数**

| 参数名   | 类型   | 必填 | 说明         |
|----------|--------|------|--------------|
| email    | string | 是   | 用户邮箱     |
| password | string | 是   | 用户密码     |

**成功响应（200）**
```json
{
  "token": "1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5",
  "expires_at": "2025-12-29T21:53:00.000000Z"
}
```

**错误响应**

- `401 Unauthorized`：邮箱或密码错误
- `403 Forbidden`：账号被禁用
- `422 Unprocessable Entity`：缺少必填参数或格式错误

---

## 清空 Token

**接口地址**
`DELETE /auth/token`

**说明**
用于注销当前 Token，使其立即失效。

**请求示例**
```bash
curl -X DELETE https://img.yuncen.top/api/v1/auth/token \
  -H "Authorization: Bearer 1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5" \
  -H "Accept: application/json"
```

**请求 Headers**

| 字段           | 说明                     |
|----------------|--------------------------|
| Authorization  | Bearer Token（必填）     |
| Accept         | `application/json`（必填）|

**成功响应（204）**
无返回内容，状态码为 `204 No Content`。

**错误响应**

- `401 Unauthorized`：Token 无效或缺失

---

## 获取用户资料

**接口地址**
`GET /user/profile`

**说明**
获取当前授权用户的详细信息。

**请求示例**
```bash
curl -X GET https://img.yuncen.top/api/v1/user/profile \
  -H "Authorization: Bearer 1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5" \
  -H "Accept: application/json"
```

**请求 Headers**

| 字段           | 说明                     |
|----------------|--------------------------|
| Authorization  | Bearer Token（必填）     |
| Accept         | `application/json`（必填）|

**成功响应（200）**
```json
{
  "id": 1,
  "name": "example_user",
  "email": "your_email@example.com",
  "created_at": "2024-01-01T00:00:00.000000Z",
  "updated_at": "2025-12-28T21:53:00.000000Z"
}
```

**错误响应**

- `401 Unauthorized`：Token 无效或缺失