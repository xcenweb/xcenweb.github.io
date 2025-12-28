# 接口总览

本系统提供一套 RESTful 风格的 API 接口，用于图片上传、用户授权、相册管理等功能。所有接口均基于以下基础路径：

## 接口 URL

```
https://img.yuncen.top/api/v1
```

例如，上传图片的完整地址为：
`https://img.yuncen.top/api/v1/upload`

---

## 验证方式

当前版本采用 **Bearer Token**（即 HTTP Bearer Authentication）进行身份验证。

- 获取 Token 后，在每次请求时需在 Header 中添加：
  ```http
  Authorization: Bearer 1|1bJbwlqBfnggmOMEZqXT5XusaIwqiZjCDs7r1Ob5
  ```
- 若未提供 `Authorization`，上传请求将被视为 **游客上传**（受限功能）。

> 💡 Token 可通过 [生成 Token](#生成-token) 接口获取。

---

## 公共请求 Headers

所有 API 请求（除生成 Token 外）必须包含以下 Header：

| 字段         | 类型   | 说明                                      |
|--------------|--------|-------------------------------------------|
| `Authorization` | String | 授权 Token，格式：`Bearer <token>`        |
| `Accept`<span class="text-red-500">*</span> | String | 必须设为 `application/json`               |

> 🔴 带红色星号（*）的字段为必填项。

---

## 公共响应 Headers

服务器会在每个响应中返回以下限流信息：

| 字段                    | 类型    | 说明                             |
|-------------------------|---------|----------------------------------|
| `X-RateLimit-Limit`     | Integer | 当前客户端每分钟允许的最大请求数 |
| `X-RateLimit-Remaining` | Integer | 当前客户端剩余的请求次数         |

---

## HTTP 状态码说明

| 状态码 | 说明                         |
|--------|------------------------------|
| `401`  | 未登录或授权失败             |
| `403`  | 管理员已关闭接口功能         |
| `429`  | 超出请求配额，请求被限制     |
| `500`  | 服务端发生内部错误           |

---

> 📌 提示：所有接口的请求参数中，若字段名前带有红色星号（<span style="color:red">*</span>），表示该参数为**必传项**。