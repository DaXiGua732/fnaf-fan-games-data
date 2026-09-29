# fnaf-fan-games-data

**本仓库只放「数据」与「图片」，不放任何代码。**

代码在 [`fnaf-fan-games-archive`](https://github.com/DaXiGua732/fnaf-fan-games-archive)。

## 为什么要拆成两个仓库

为了让**管理员能改数据、但碰不到代码**。

权限边界由 GitHub 的仓库权限天然给出，不需要自建任何服务：

| 仓库 | 谁有写权限 | 里面有什么 |
| --- | --- | --- |
| `fnaf-fan-games-archive`（代码仓） | 只有站长 | 站点源码 |
| **`fnaf-fan-games-data`（本仓库）** | 站长 + 各位管理员 | `db.json` + `images/` |

管理员**只需要**本仓库的权限。代码仓不要加入管理员。

## 目录结构

```
db.json          网站的全部游戏数据（后台编辑的就是它）
images/          封面 / Banner / 图库图片
```

## 怎么改数据

**推荐：用后台管理界面改。** 打开站点的 `/#/admin`，登录后正常编辑、保存即可 ——
保存会通过 GitHub API 直接提交到本仓库，触发代码仓重新构建发布。

**也可以：直接编辑 `db.json` 提交。** 它是唯一的真实数据源，格式见下。

## 图片地址约定

`db.json` 里的图片字段写**本站 Pages 的绝对地址**：

```json
"coverImage": "https://daxigua732.github.io/fnaf-fan-games-data/images/xxx.jpg"
```

这样做的好处是**前台不需要做任何改动** —— 前台的 `assetUrl()` 会原样放行完整外链，
站内路径与绝对地址两种形态都支持。

> ⚠️ 不要写成 `/images/xxx.jpg`（以斜杠开头的站内路径）。
> 那会被解析到**代码仓**的域名下，图片会 404。

## 改动怎么生效

1. 本仓库的 `db.json` / `images/` 更新
2. 代码仓的 Actions 重新构建（构建时会把本仓库的 `db.json` 拉过去）
3. GitHub Pages 发布新版本

（详见代码仓的 `README.md` 与 `admin_phase13_persistence_decision.md`。）

## 注意

- 本仓库是 **Public** 的 —— 因为 GitHub Pages 的免费额度只覆盖公开仓库。
  这里的内容本来就会通过前台对公众可见，所以不构成额外暴露。
- **不要**往这里放任何代码、密钥、配置文件。管理员有本仓库的写权限，
  放代码就等于把代码交给了所有人。
- 历史即备份：本仓库的 git 历史是完整、可逐行 diff 的回滚手段。改错了直接 revert。
