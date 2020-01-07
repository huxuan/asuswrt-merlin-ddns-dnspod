# asuswrt-merlin-ddns-dnspod

华硕梅林系统上更新 DNSPod DDNS 的脚本

*其他语言版本: [English](README.md), [简体中文](README-zh.md).*

## 使用方法

1. 将 `ddns-start` 脚本下载到 `/jffs/scripts/`。

   ```shell
   wget https://raw.githubusercontent.com/huxuan/asuswrt-merlin-ddns-dnspod/master/ddns-start -P /jffs/scripts/
   ```

1. 修改脚本中相应的参数，具体信息参见[参数说明](#参数说明)。

1. 最后，确保脚本是可执行状态。

   ```shell
   chmod +x /jffs/scripts/ddns-start
   ```

## 参数说明

1. DDNS_DOMAIN

   不包含子域名的域名，如 `example.com`。

1. DDNS_SUB_DOMAIN

   仅需要子域名部分，如 `www`。

1. [DNSPOD_LOGIN_TOKEN](https://support.dnspod.cn/Kb/showarticle/tsid/227/)

   授权修改 DNSPod 上 DNS 记录的 Token。需要注意它是由 `ID` 和 `Token` 组合而成，所以应该形如 `13490,6b5976c68aba5b14a0558b77c17c3932`

1. [DNSPOD_RECORD_ID](https://www.dnspod.cn/docs/records.html#record-list)

   DNS 记录的 ID. 用前面提到的参数替换掉下方命令中的相应部分，然后就会得到所需要的记录 ID（通常只有一个）。

   这是一次性的工作，所以我故意把它摘出来为了不用在 `ddns-start` 中每次都运行。

   ```shell
   curl -x POST https://dnsapi.cn/Record.List \
   -d login_token=<YOUR_DDNS_LOGIN_TOKEN> \
   -d domain=<YOUR_DDNS_DOMAIN> \
   -d sub_domain=<YOUR_DDNS_SUB_DOMAIN> \
   -d format=json
   ```

1. [DNSPOD_RECORD_LINE_ID](https://www.dnspod.cn/docs/domains.html#record-line)

   对应域名所允许的 DNS 记录线路 ID。这主要是用于不同网络服务提供商的动态 DNS 策略，通常情况下只需要使用默认值 `0` 。
