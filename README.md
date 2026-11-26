# QLScriptHub

[English](README_EN.md)

QLScriptHub 是一个面向青龙面板的 Python 脚本仓库，用于维护常用的签到任务和后续自行开发的自动化脚本。

## 常用脚本

| 平台 | 脚本 | 青龙环境变量 |
| --- | --- | --- |
| 阿里云盘 | [aliyunpan_checkin.py](aliyunpan_checkin.py) | `ALIYUN_REFRESH_TOKEN` |
| 百度网盘 | [baiduwangpan_checkin.py](baiduwangpan_checkin.py) | `BAIDU_COOKIE` |
| 塔斯汀汉堡 | [tsthb_checkin.py](tsthb_checkin.py) | `tsthbck` |

三个脚本均支持多账号，每行填写一个账号的凭据。Cookie、Token 和推送密钥请配置在青龙环境中，避免写入仓库。

## 青龙面板接入

1. 在青龙的「依赖管理」中确认 Python 依赖 `requests` 可用。阿里云盘脚本还会直接导入 `urllib3`。
2. 在「订阅管理」中添加公开仓库，地址填 `https://github.com/kkdxisme/QLScriptHub.git`，分支填 `main`，文件后缀填 `py`。只订阅上面三个脚本时，白名单填 `(aliyunpan_checkin|baiduwangpan_checkin|tsthb_checkin)\.py$`。
3. 运行订阅，在「环境变量」中配置所需变量，或沿用同一青龙实例中的已有配置。
4. 从「定时任务」手动运行各脚本，核对日志和通知。迁移已有任务时，先核对新任务的命令路径和执行时间，验证通过后停用对应的旧任务，再启用新任务的定时运行。

三个脚本通过青龙环境中可导入的 `notify.py` 发送通知。已有 PushPlus 配置可继续复用。若通知模块无法导入，脚本会在日志中输出结果。

首次手动验证时，可为测试运行设置 `RANDOM_SIGNIN=false`，跳过脚本启动时的随机等待。阿里云盘的 `AUTO_UPDATE_TOKEN` 默认开启，服务返回新 Token 时会尝试更新青龙中的变量。

## 其他脚本

| 平台 | 脚本 | 主要环境变量 |
| --- | --- | --- |
| 成都地铁 | [CDRail.py](CDRail.py) | `CDRAIL_DATA` |
| Deepflood | [deepflood_checkin.py](deepflood_checkin.py) | `DEEPFLOOD_COOKIE` |
| 恩山论坛 | [enshan_checkin.py](enshan_checkin.py) | `enshan_cookie` |
| HiFiTi / HiFiHi | [HiFiti_checkin.py](HiFiti_checkin.py) | `HiFiTi_COOKIE`、`HIFIHI_COOKIE` |
| ikuuu | [ikuuu_checkin.py](ikuuu_checkin.py) | `IKUUU_EMAIL`、`IKUUU_PASSWD` |
| NGA | [nga_checkin.py](nga_checkin.py) | `NGA_CREDENTIALS` |
| NodeSeek | [nodeseek_checkin.py](nodeseek_checkin.py) | `NODESEEK_COOKIE` |
| PassNAT | [passnat_checkin.py](passnat_checkin.py) | `PASSNAT_SK` |
| 夸克网盘 | [quark_signin.py](quark_signin.py) | `QUARK_COOKIE` |
| 顺丰速运 | [SFSU_checkin.py](SFSU_checkin.py) | `sfsyUrl` |
| 什么值得买 | [SMZDM_checkin.py](SMZDM_checkin.py) | `SMZDM_COOKIE` |
| 百度贴吧 | [tieba_checkin.py](tieba_checkin.py) | `TIEBA_COOKIE` |
| 天翼云盘 | [ty_netdisk_checkin.py](ty_netdisk_checkin.py) | `TY_USERNAME`、`TY_PASSWORD` |

Deepflood 和 NodeSeek 使用 `curl_cffi`，天翼云盘另外需要 `rsa`。[archive/](archive/) 保存归档脚本。其他脚本可按需核对其配置和运行结果后加入订阅。

## 后续开发

新增脚本时，沿用独立的 Python 入口，通过环境变量读取配置，并在文件头说明用途和建议的执行时间。增加依赖或修改配置时，同步更新中英文 README。发布前先用青龙手动验证任务，再加入定时调度。

## 许可与来源

仓库许可文件见 [LICENSE](LICENSE)。移植脚本源自 [agluo/ql-script-hub](https://github.com/agluo/ql-script-hub)，原项目使用 [MIT 许可](https://github.com/agluo/ql-script-hub/blob/master/LICENSE)。脚本文件头另有来源说明的，以相应标注为准。
