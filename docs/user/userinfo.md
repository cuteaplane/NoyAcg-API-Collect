
# 获取用户信息 API

## 简述

用于获取当前登录账户的详细个人资料、资产状态（积分）以及佩戴的勋章列表。此接口还可用于在执行自动化任务前检查 `NOY_SESSION` 的存活状态。

## 接口信息

- **Endpoint**: `https://beta.noyteam.online/api/v3/userinfo`
- **请求方式**: `POST`
- **Content-Type**: `application/x-www-form-urlencoded`
- **鉴权方式**: 请求头 `Cookie` 中必须包含有效的 `NOY_SESSION`。

> **注意**：该 POST 请求通常不携带请求体（`Content-Length: 0`）。

## 响应定义

### 1. 成功响应 (Session 有效)
HTTP 状态码: `200 OK`
Example Response:
```json
{
  "status": "ok",
  "userinfo": {
    "Email": "your@email.com",
    "Integral": 41,
    "Time": 1673114514,
    "Uhash": "1343a10d7",
    "Uid": [your uid],
    "Username": "[your username]",
    "Avatar": "avatar/91266-231a7416383ae44f5a6562ac75d79b84f3863d742152405be1be8b3cd6f4b19d.webp",
    "Bg": "bg/91266-c558855dbf5fba56abea7eaf975a978249001c73a47c13774c65438f762f6ebb.webp",
    "CommentLen": 0,
    "Badge": [
      {
        "Id": 0,
        "Name": "諾莉亞的凝視",
        "Img": "[https://bucket.239847.xyz/image/nry-bge.webp](https://bucket.239847.xyz/image/nry-bge.webp)",
        "Minimg": "[https://bucket.239847.xyz/image/nry-bgem.webp](https://bucket.239847.xyz/image/nry-bgem.webp)",
        "Des": "有這個徽章的人，應該積分都比較多"
      },
      {
        "Id": 0,
        "Name": "丸",
        "Img": "[https://bucket.239847.xyz/image/kimeemaru.webp](https://bucket.239847.xyz/image/kimeemaru.webp)",
        "Minimg": "[https://bucket.239847.xyz/image/kimeemaru-m.webp](https://bucket.239847.xyz/image/kimeemaru-m.webp)",
        "Des": "2025 愚人節限定徽章"
      }
    ],
    "Su": 0
  }
}

```

#### 关键字段解析:

| 路径 | 类型 | 说明 |
| --- | --- | --- |
| `status` | str | 业务状态标识，成功时为 `"ok"` |
| `userinfo.Integral` | int | 账户当前积分余额 |
| `userinfo.Uid` | int | 用户 UID |
| `userinfo.Username` | str | 账户昵称 |
| `userinfo.Badge` | array | 当前佩戴的勋章列表 |
| `userinfo.avatar` | str | 头像图片 |
| `userinfo.Bg` | str | 背景图片 |

### 2. 失效响应 (Session 过期或未登录)

```json
{
  "status": "login"
}

```





还有什么要补充的细节吗？Gemini 随时准备待命喵！(✿◡‿◡)

```
