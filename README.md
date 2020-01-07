# asuswrt-merlin-ddns-dnspod

DNSPod DDNS update script for Asuswrt-Merlin

*Read this in other languages: [English](README.md), [简体中文](README-zh.md).*

## Usage

1. Download the `ddns-start` script to `/jffs/scripts/`.

   ```shell
   wget https://raw.githubusercontent.com/huxuan/asuswrt-merlin-ddns-dnspod/master/ddns-start -P /jffs/scripts/
   ```

1. Modify the parameters in the script accordingly. More detailed information please refer to the [Parameter Specification](#Parameter-Specification).

1. Last but not least, ensure the script is executable.

   ```shell
   chmod +x /jffs/scripts/ddns-start
   ```

## Parameter Specification

1. DDNS_DOMAIN

   The domain name without subdomain, e.g., `example.com`.

1. DDNS_SUB_DOMAIN

   Only the subdomain part, e.g., `www`.

1. [DNSPOD_LOGIN_TOKEN](https://support.dnspod.cn/Kb/showarticle/tsid/227/)

   The token for authorization to modify the DNS record on DNSPod. Note that it is a combination of `ID` and `Token`, so it looks like `13490,6b5976c68aba5b14a0558b77c17c3932`.

1. [DNSPOD_RECORD_ID](https://www.dnspod.cn/docs/records.html#record-list)

   The ID of the DNS record. Just fill the following command with the proceeding parameters and the record ids (only one usually) will return.

   This is a one-time effort so I pick it out intentionally so as not to run it every time within `ddns-start` script.

   ```shell
   curl -x POST https://dnsapi.cn/Record.List \
   -d login_token=<YOUR_DDNS_LOGIN_TOKEN> \
   -d domain=<YOUR_DDNS_DOMAIN> \
   -d sub_domain=<YOUR_DDNS_SUB_DOMAIN> \
   -d format=json
   ```

1. [DNSPOD_RECORD_LINE_ID](https://www.dnspod.cn/docs/domains.html#record-line)

   The allowed line's ids for the domain's DNS record. This is mostly used for dynamic DNS policy for different ISPs, for general usage, just use the default value `0`.
