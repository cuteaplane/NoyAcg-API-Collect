
# 设置徽章展示状态

用于 **勾选或取消勾选徽章展示**。

请求接口会 **切换状态**：

* 未展示 → 勾选展示
* 已展示 → 取消展示

---

## 接口地址

* 地址：```/api/v3/set_badge_show```

* 完整地址：```https://beta.noyteam.online/api/v3/set_badge_show```

* 请求方式：```POST```
---

# 请求参数

| 参数 | 类型  | 示例  | 说明    |
| -- | --- | --- | ----- |
| id | int | `8` | 徽章 ID |

请求示例：

```
id=8
```

---

# 返回示例

```json
{
  "status": "ok"
}
```

---

# curl 测试示例

## 勾选 / 取消勾选徽章

Windows CMD

```cmd
curl "https://beta.noyteam.online/api/v3/set_badge_show" ^
  -X POST ^
  -H "accept: application/json" ^
  -H "content-type: application/x-www-form-urlencoded" ^
  -b "NOY_SESSION=你的session" ^
  --data-raw "id=8"
```

说明：

* 如果该徽章 **未展示** → 请求后会 **勾选**
* 如果该徽章 **已展示** → 请求后会 **取消勾选**
* 请求不存在的id时貌似也会返回ok

```cmd
curl "https://beta.noyteam.online/api/v3/set_badge_show" ^
  -X POST ^
  -H "accept: application/json" ^
  -H "content-type: application/x-www-form-urlencoded" ^
  -b "NOY_SESSION=你的session" ^
  --data-raw "id=114514"
```
```json
{
  "status": "ok"
}
```

---
