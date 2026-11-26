# QLScriptHub

[简体中文](README.md)

QLScriptHub is a collection of Python scripts for the QingLong panel. It contains daily check-in tasks and provides a place to develop additional automation scripts.

## Main scripts

| Service | Script | QingLong environment variable |
| --- | --- | --- |
| Aliyun Drive | [aliyunpan_checkin.py](aliyunpan_checkin.py) | `ALIYUN_REFRESH_TOKEN` |
| Baidu Netdisk | [baiduwangpan_checkin.py](baiduwangpan_checkin.py) | `BAIDU_COOKIE` |
| Tastien | [tsthb_checkin.py](tsthb_checkin.py) | `tsthbck` |

All three scripts support multiple accounts, with one account credential per line. Store cookies, tokens, and notification keys in the QingLong environment and keep them out of the repository.

## QingLong setup

1. In QingLong's Dependency Management, confirm that the Python package `requests` is available. The Aliyun Drive script also imports `urllib3` directly.
2. In Subscription Management, add the public repository `https://github.com/kkdxisme/QLScriptHub.git`, use branch `main`, and set the file extension to `py`. To subscribe to the three scripts above, use the allowlist `(aliyunpan_checkin|baiduwangpan_checkin|tsthb_checkin)\.py$`.
3. Run the subscription. Set the required environment variables or reuse the variables already configured in the same QingLong instance.
4. Run each task manually and check its logs and notifications. When migrating existing tasks, check the new commands and schedules first. Once the manual runs pass, disable the corresponding old tasks before enabling the new schedules.

The three scripts send notifications through a `notify.py` module available in the QingLong environment. You can reuse an existing PushPlus setup. If the module cannot be imported, the scripts report their results in the logs.

Set `RANDOM_SIGNIN=false` for a test run to skip the initial random delay. Aliyun Drive enables `AUTO_UPDATE_TOKEN` by default and attempts to update the QingLong variable when the service returns a new token.

## Other scripts

| Service | Script | Main environment variables |
| --- | --- | --- |
| Chengdu Metro | [CDRail.py](CDRail.py) | `CDRAIL_DATA` |
| Deepflood | [deepflood_checkin.py](deepflood_checkin.py) | `DEEPFLOOD_COOKIE` |
| Enshan Forum | [enshan_checkin.py](enshan_checkin.py) | `enshan_cookie` |
| HiFiTi / HiFiHi | [HiFiti_checkin.py](HiFiti_checkin.py) | `HiFiTi_COOKIE`, `HIFIHI_COOKIE` |
| ikuuu | [ikuuu_checkin.py](ikuuu_checkin.py) | `IKUUU_EMAIL`, `IKUUU_PASSWD` |
| NGA | [nga_checkin.py](nga_checkin.py) | `NGA_CREDENTIALS` |
| NodeSeek | [nodeseek_checkin.py](nodeseek_checkin.py) | `NODESEEK_COOKIE` |
| PassNAT | [passnat_checkin.py](passnat_checkin.py) | `PASSNAT_SK` |
| Quark Drive | [quark_signin.py](quark_signin.py) | `QUARK_COOKIE` |
| SF Express | [SFSU_checkin.py](SFSU_checkin.py) | `sfsyUrl` |
| SMZDM | [SMZDM_checkin.py](SMZDM_checkin.py) | `SMZDM_COOKIE` |
| Baidu Tieba | [tieba_checkin.py](tieba_checkin.py) | `TIEBA_COOKIE` |
| Tianyi Cloud Drive | [ty_netdisk_checkin.py](ty_netdisk_checkin.py) | `TY_USERNAME`, `TY_PASSWORD` |

Deepflood and NodeSeek use `curl_cffi`. Tianyi Cloud Drive also requires `rsa`. Archived scripts are kept in [archive/](archive/). Check each script's configuration and run results before including it in a subscription.

## Development

Give each new script a standalone Python entry point, read configuration from environment variables, and document the script's purpose and suggested schedule in its header. Update both READMEs when dependencies or configuration change. Run new tasks manually in QingLong before enabling their schedules.

## License and attribution

See [LICENSE](LICENSE) for the repository license file. The imported scripts come from [agluo/ql-script-hub](https://github.com/agluo/ql-script-hub), which uses the [MIT license](https://github.com/agluo/ql-script-hub/blob/master/LICENSE). See individual script headers for additional source attribution where provided.
