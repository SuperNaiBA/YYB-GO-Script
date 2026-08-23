
推荐https://github.com/lcmovie/YYB-GO-Script-i 本仓库没时间维护了

# YYB_SERVER

YYB Go 适配版。

## 环境变量

| 变量名 | 格式 | 示例 |
|--------|------|------|
| `YYB_SERVER` | `地址@微信账号标识`，一行一个 | `172.17.0.4:8000@XXXXXXXXXX` |

## 青龙订阅

```
ql repo https://github.com/SuperNaiBA/YYB-GO-Script.git "" "SendNotify.py" "main" ""
```

## 京东 Cookie 脚本

仓库提供两个京东小程序登录脚本，登录逻辑相同（code → login_lt → PT OAuth 兜底），区别在于 cookie 写入方式：

| 脚本 | 写入方式 | 依赖环境变量 |
|------|----------|--------------|
| `JDCode.py` | 青龙 OpenAPI 写入 `JD_COOKIE` | `QL_URL` / `QL_CLIENT_ID` / `QL_CLIENT_SECRET` |
| `JDCodeLocal.py` | 直写青龙 SQLite 数据库 | 无需以上三个 |

### 配置示例

```bash
# 必填
export YYB_SERVER='应用宝地址@openid'

# 可选：单/多账号配置（不填则自动读取 YYB_SERVER 的 /accounts）
export JD_ACCOUNTS_JSON='[{"name":"京东账号1","ref":"1"},{"name":"京东账号2","ref":"2"}]'

# JDCode.py 额外需要
export QL_URL='青龙地址'
export QL_CLIENT_ID='你的client_id'
export QL_CLIENT_SECRET='你的client_secret'

# JDCodeLocal.py 不需要上面三个，自动写 /ql/data/db/database.sqlite
```

### 可选配置

| 变量名 | 默认值 | 说明 |
|--------|--------|------|
| `JD_ACCOUNTS_JSON` | 空 | 单/多账号配置，JSON 数组，例：`[{"name":"京东账号1","ref":"1"},{"name":"京东账号2","ref":"2"}]` |
| `JD_LOGIN_MODE` | `auto` | `auto` / `code` / `full` |
| `JD_COOKIE_MODE` | `pt` | `pt`（仅 pt_key/pt_pin）/ `all`（全部 cookie） |
| `JD_COOKIE_ENV_NAME` | `JD_COOKIE` | 写入青龙的变量名 |
| `QL_DB_PATH` | `/ql/data/db/database.sqlite` | 仅 JDCodeLocal，青龙数据库路径 |

### 青龙任务

```
task SuperNaiBA_YYB-GO-Script/JDCode.py
task SuperNaiBA_YYB-GO-Script/JDCodeLocal.py
```

cron 建议 `0 */2 * * *`。两个脚本二选一即可，不要同时跑。

## 注意事项

- 不要带 `http://` 前缀
- 不要用容器名（如 `yyb-go`），用 IP
- 脚本不会同时执行，青龙定时任务需手动错开 cron

## 免责声明

这里的脚本只是自己学习 js 的一个实践 仅用于测试和学习研究，禁止用于商业用途，不能保证其合法性，准确性，完整性和有效性，请根据情况自行判断.

仓库内所有资源文件，禁止任何公众号、自媒体进行任何形式的转载、发布。

SuperNaiBA 对任何脚本问题概不负责，包括但不限于由任何脚本错误导致的任何损失或损害.

间接使用脚本的任何用户，包括但不限于建立VPS或在某些行为违反国家/地区法律或相关法规的情况下进行传播, SuperNaiBA 对于由此引起的任何隐私泄漏或其他后果概不负责.

如果任何单位或个人认为该项目的脚本可能涉嫌侵犯其权利，则应及时通知并提供身份证明，所有权证明，我们将在收到认证文件后删除相关脚本.

任何以任何方式查看此项目的人或直接或间接使用该Script项目的任何脚本的使用者都应仔细阅读此声明。 SuperNaiBA 保留随时更改或补充此免责声明的权利。一旦使用并复制了任何相关脚本或Script项目的规则，则视为您已接受此免责声明.

您必须在下载后的24小时内从计算机或手机中完全删除以上内容.严禁产生利益链！
