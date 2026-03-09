# NOY_SESSION

## 简述

`NOY_SESSION` 是 API 的核心鉴权凭证，通过 HTTP 请求头中的 `Cookie` 字段进行传递。

该凭证通常在用户成功登录后由服务器通过 `Set-Cookie` 响应头下发，有效时长约为 30 天。

几乎所有api调用都需要NOY_SESSION。
