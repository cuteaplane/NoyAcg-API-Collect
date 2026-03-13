# 图床上传 API（bucket.noymanga.com/api/upload_image）

当你准备发帖并附带图片时，需要先把图片文件上传到图床。

这条接口会把你本地的 `jpg/png/webp/...` 上传上去，并返回一个 `file` 文件名。
后续发帖并不是把图片二次上传，而是把这个 `file` 作为引用传给发帖接口。

---


## 接口信息

| 项目 | 内容 |
| --- | --- |
| Endpoint | `https://bucket.noymanga.com/api/upload_image` |
| 请求方式 | `POST` |
| Content-Type | `multipart/form-data` |
| 返回格式 | `application/json` |

---

## 请求头（Headers）

| 字段 | 必填 | 示例 | 说明 |
| --- | --- | --- | --- |
| `Origin` | 建议 | `https://beta.noyteam.online` | 模拟跨域上传（但其实这个接口CORS过不去awa） |
| `Referer` | 建议 | `https://beta.noyteam.online/` | 同上 |
| `allow-adult` | 否 | `false` | 参考前端请求 |


---

## 请求参数（表单）

| 字段 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `token` | string | 是 | 上传凭证（上一步接口返回） |
| `file` | file | 是 | 图片文件（字段名必须是 `file`） |


---

## 响应

成功示例：
```json
{
  "file": "91266-13025882b9402bd576b628a1030433a6388156d5aaeccb40362960af47a4aa79.webp",
  "status": "ok"
}
```

字段说明：
- `file`：图床文件名。注意服务端可能会统一转成 `.webp`。

失败示例：
- `{"status":"token_format_error"}`：token 不对或已过期，或者上传表单字段不符合预期。
- HTTP 500：服务端异常（可能是cf发威）。

排查顺序建议：
1. 重新调用 `get_image_bucket_token` 拿新 token。
2. 确认表单字段名为 `token` + `file`。
3. 不要自己拼 boundary。

---

## 示例

### curl（推荐）
```bash
curl "https://bucket.noymanga.com/api/upload_image" \
  -X POST \
  -H "origin: https://beta.noyteam.online" \
  -H "referer: https://beta.noyteam.online/" \
  -F "token=<上一步返回的token>" \
  -F "file=@b57f10d4a0a40adb08ef3e6f55b64f07.jpg"
```

