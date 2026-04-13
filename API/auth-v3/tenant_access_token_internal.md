# 获取租户访问凭证 (auth/v3/tenant_access_token/internal)

自建应用通过此接口获取 `tenant_access_token`。

## 注意事项

`tenant_access_token` 的最大有效期是 2 小时。

- 剩余有效期小于 30 分钟时，调用本接口会返回一个新的 `tenant_access_token`，这会同时存在两个有效的 `tenant_access_token`。
- 剩余有效期大于等于 30 分钟时，调用本接口会返回原有的 `tenant_access_token`。

## 权限要求

### 必要权限

该接口**无需任何权限**即可调用。

### 可选权限

该接口无敏感字段，无需额外的字段权限。

## 接口信息

| API 路径 | `https://open.feishu.cn/open-apis/auth/v3/tenant_access_token/internal` |
|----------|------------------------------------------------------------------------|
| 请求方法 | POST |
| 调用频率限制 | - |
| 支持的应用类型 | Custom App |
| 文档地址 | [飞书开放平台](https://open.feishu.cn/document/ukTMukTMukTM/reference/auth-v3/tenant_access_token/internal) |

## 接口请求

### 请求头

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `Content-Type` | string | 是 | **固定值**："application/json; charset=utf-8" |

### 请求参数

该接口无 URL 查询参数。

### 请求体

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `app_id` | string | 是 | 应用唯一标识，创建应用后获得。有关 `app_id` 的详细介绍，请参考[通用参数](https://open.feishu.cn/document/ukTMukTMukTM/uYTM5UjL2ETO14iNxkTN/terminology)介绍 |
| `app_secret` | string | 是 | 应用秘钥，创建应用后获得。有关 `app_secret` 的详细介绍，请参考[通用参数](https://open.feishu.cn/document/ukTMukTMukTM/uYTM5UjL2ETO14iNxkTN/terminology)介绍 |

### 请求示例

#### Go 请求示例

```go
import (
	"bytes"
	"context"
	"encoding/json"
	"fmt"
	"net/http"
)

func main() {
	// 构建请求体
	reqBody := map[string]string{
		"app_id":     "cli_slkdjalasdkjasd",
		"app_secret": "dskLLdkasdjlasdKK",
	}
	bodyBytes, _ := json.Marshal(reqBody)

	// 发起请求
	req, _ := http.NewRequest("POST", "https://open.feishu.cn/open-apis/auth/v3/tenant_access_token/internal", bytes.NewReader(bodyBytes))
	req.Header.Set("Content-Type", "application/json; charset=utf-8")

	client := &http.Client{}
	resp, err := client.Do(req)
	if err != nil {
		fmt.Println("Error:", err)
		return
	}
	defer resp.Body.Close()
}
```

#### Java 请求示例

```java
import java.io.IOException;
import java.util.HashMap;
import java.util.Map;
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.RequestBody;
import okhttp3.Response;

public class Main {
    public static void main(String[] args) throws IOException {
        OkHttpClient client = new OkHttpClient();

        Map<String, String> body = new HashMap<>();
        body.put("app_id", "cli_slkdjalasdkjasd");
        body.put("app_secret", "dskLLdkasdjlasdKK");

        String jsonBody = new com.fasterxml.jackson.databind.ObjectMapper().writeValueAsString(body);
        RequestBody requestBody = RequestBody.create(jsonBody, okhttp3.MediaType.parse("application/json; charset=utf-8"));

        Request request = new Request.Builder()
                .url("https://open.feishu.cn/open-apis/auth/v3/tenant_access_token/internal")
                .post(requestBody)
                .addHeader("Content-Type", "application/json; charset=utf-8")
                .build();

        try (Response response = client.newCall(request).execute()) {
            System.out.println(response.body().string());
        }
    }
}
```

## 接口响应

### 响应体

| 字段 | 类型 | 描述 |
|------|------|------|
| `code` | int | 错误码，非 0 取值表示失败 |
| `msg` | string | 错误描述 |
| `tenant_access_token` | string | 租户访问凭证 |
| `expire` | int | `tenant_access_token` 的过期时间，单位为秒 |

### 响应示例

```json
{
    "code": 0,
    "msg": "ok",
    "tenant_access_token": "t-caecc734c2e3328a62489fe0648c4b98779515d3",
    "expire": 7200
}
```

## 响应码定义

| HTTP状态码 | 错误码 | 描述 |
|------------|--------|------|
| 200 | 0 | 请求成功 |
| 400 | - | 请求参数错误 |
| 401 | - | 应用凭证无效 |
| 500 | - | 服务器内部错误 |

## 附录

### 相关链接

| 链接类型 | 链接 |
|----------|------|
| 通用参数 | [https://open.feishu.cn/document/ukTMukTMukTM/uYTM5UjL2ETO14iNxkTN/terminology](https://open.feishu.cn/document/ukTMukTMukTM/uYTM5UjL2ETO14iNxkTN/terminology) |
| 通用错误码 | [https://open.feishu.cn/document/ukTMukTMukTM/ugjM14COyUjL4ITN](https://open.feishu.cn/document/ukTMukTMukTM/ugjM14COyUjL4ITN) |