# 用户登录 API 

## 简述

用于通过用户凭据（邮箱与密码）换取会话令牌 `NOY_SESSION`。

## 接口信息

- **Endpoint**: `POST /api/login`
- **请求方式**: `POST`
- **Content-Type**: `application/x-www-form-urlencoded`

## 请求参数

| 参数名 | 类型 | 示例 | 必要性 | 备注 |
| :--- | :--- | :--- | :--- | :--- |
| `user` | str | `example@outlook.com` | **必要** | 注册时使用的邮箱地址 |
| `pass` | str | `your_password` | **必要** | 账户登录密码 |

## 响应定义

### 成功 (Success)
HTTP 状态码: `200`
```json
{
  "status": "ok"
}

```

响应头（Response Headers）中返回 `Set-Cookie`。
```example
NOY_SESSION=***; Path=/; Expires=Tue, 07 Apr 2026 11:45:14 GMT; Max-Age=2592000
```
### 失败 (Error)

HTTP 状态码: `200` (业务逻辑错误)

```json
{
  "status": "error"
}

```

> **可能原因**: 账号不存在、密码错误或请求频率过快。

## 代码示例 (Python)

使用 `requests.Session` 自动处理 Cookie 挂载：

```python
import requests

def login(email, password):
    url = "[https://beta.noyteam.online/api/login](https://beta.noyteam.online/api/login)"
    payload = {
        "user": email,
        "pass": password
    }
    
    # 建立会话对象，自动管理 Cookie
    session = requests.Session()
    
    try:
        response = session.post(url, data=payload)
        result = response.json()
        
        if result.get("status") == "ok":
            print("登录成功！已获取 NOY_SESSION")
            return session
        else:
            print("登录失败，请检查凭据")
            return None
    except Exception as e:
        print(f"网络请求异常: {e}")
        return None

```

---

