# asuswrt-merlin-ddns-dnspod

DNSPod DDNS update script for Asuswrt-Merlin

华硕梅林系统上更新 DNSPod DDNS 的脚本

## Usage 使用方法

1. Download the `ddns-start` script to `/jffs/scripts/`.

   将 `ddns-start` 脚本下载到 `/jffs/scripts/`。

   ```shell
   wget https://raw.githubusercontent.com/huxuan/asuswrt-merlin-ddns-dnspod/master/ddns-start -P /jffs/scripts/
   ```

1. Modify the parameters in the script accordingly. More detailed information please refer to the [Parameter Specification](#Parameter-Specification-参数说明).

   修改脚本中相应的参数，具体信息参见[参数说明](#Parameter-Specification-参数说明)。

1. Last but not least, ensure the script is executable.

   最后，确保脚本是可执行状态。

   ```shell
   chmod +x /jffs/scripts/ddns-start
   ```

## Parameter Specification 参数说明

1. DDNS_DOMAIN

   The domain name without subdomain, e.g., `example.com`.

   不包含子域名的域名，如 `example.com`。

1. DDNS_SUB_DOMAIN

   Only the subdomain part, e.g., `www`.

   仅需要子域名部分，如 `www`。

1. DNSPOD_LOGIN_TOKEN

   The token for authorization to modify the DNS record on DNSPod. Note that it is a combination of `ID` and `Token`, so it looks like `13490,6b5976c68aba5b14a0558b77c17c3932`.

   [the corresponding official documentation](https://support.dnspod.cn/Kb/showarticle/tsid/227/)

   授权修改 DNSPod 上 DNS 记录的 Token。需要注意它是由 `ID` 和 `Token` 组合而成，所以应该形如 `13490,6b5976c68aba5b14a0558b77c17c3932`

   [相应的官方文档](https://support.dnspod.cn/Kb/showarticle/tsid/227/)

1. DNSPOD_RECORD_ID

   The ID of the DNS record. Just replace the following command with the proceeding parameters and the record ids (only one usually) will return.

   This is a one-time effort so it is not worthy to run it every time within `ddns-start`.

   [the corresponding official documentation](https://www.dnspod.cn/docs/records.html#record-list)

   DNS 记录的 ID. 用前面提到的参数替换掉下方命令中的相应部分，然后就会得到所需要的记录 ID（通常只有一个）。

   这是一次性的工作，所以不值得放在 `ddns-start` 中每次都运行。

   [相应的官方文档](https://www.dnspod.cn/docs/records.html#record-list)

   ```shell
   curl -x POST https://dnsapi.cn/Record.List \
   -d login_token=<YOUR_DDNS_LOGIN_TOKEN> \
   -d domain=<YOUR_DDNS_DOMAIN> \
   -d sub_domain=<YOUR_DDNS_SUB_DOMAIN> \
   -d format=json
   ```

1. DNSPOD_RECORD_LINE_ID

   The allowed line's ids for the domain's DNS record. This is mostly used for dynamic DNS policy for different ISPs, for general usage, just use the default `0`.

   [the corresponding official documentation](https://www.dnspod.cn/docs/domains.html#record-line)

   对应域名所允许的 DNS 记录线路 ID。这主要是用于不同网络服务提供商的动态 DNS 策略，通常情况下只需要使用默认值 `0` 。

   [相应的官方文档](https://www.dnspod.cn/docs/domains.html#record-line)
