
# 徽章接口 (Badge API)

用于获取用户拥有的徽章，以及当前展示的徽章。

需要登录状态。

---

# 获取徽章列表

## 接口地址

```text
POST /api/badge
```

Base URL

```text
https://beta.noyteam.online
```

完整地址

```text
https://beta.noyteam.online/api/badge
```

---

# 请求方式

```
POST
```

---

# 请求头 (Headers)

| 参数           | 必须 | 示例                                  | 说明              |
| ------------ | -- | ----------------------------------- | --------------- |
| Cookie       | ✔  | `NOY_SESSION=xxxx`                  | 用户登录 Session    |
| Content-Type | ✔  | `application/x-www-form-urlencoded` | 请求类型            |
| allow-adult  | ✖  | `false`                             | 成人内容过滤（该接口通常忽略） |

---

# 请求参数

无

```
(empty)
```

---

# 返回示例

```json
{
  "data": [
    {
      "Id": 8,
      "Name": "諾莉亞的凝視",
      "Img": "https://bucket.239847.xyz/image/nry-bge.webp",
      "Minimg": "https://bucket.239847.xyz/image/nry-bgem.webp",
      "Des": "有這個徽章的人，應該積分都比較多"
    },
    {
      "Id": 9,
      "Name": "丸",
      "Img": "https://bucket.239847.xyz/image/kimeemaru.webp",
      "Minimg": "https://bucket.239847.xyz/image/kimeemaru-m.webp",
      "Des": "2025 愚人節限定徽章"
    }
  ],
  "show": [
    "9",
    "8"
  ],
  "status": "ok"
}
```

---

# 返回字段说明

## data

所有可用徽章列表。

类型

```
Badge[]
```

---

## Badge 对象

| 字段     | 类型     | 说明    |
| ------ | ------ | ----- |
| Id     | int    | 徽章 ID |
| Name   | string | 徽章名称  |
| Img    | string | 徽章大图  |
| Minimg | string | 徽章小图  |
| Des    | string | 徽章描述  |

---

## show

当前 **用户正在展示的徽章 ID 列表**。

类型

```
string[]
```

仅表示 **哪些徽章被展示**。

---

## status

| 值     | 说明              |
| ----- | --------------- |
| ok    | 请求成功            |
| login | 未登录或 Session 失效 |
| error | 请求失败            |

当 `NOY_SESSION` 失效时返回：

```json
{
  "status": "login"
}
```

