# 获取租户访问凭证 (auth/v3/tenant_access_token/internal)

自建应用通过此接口获取 `tenant_access_token`。

## 注意事项

### 模板说明

此处说明该接口的使用场景、注意事项等重要信息，特别是：

- 用户身份（user_access_token）调用时的过滤行为
- 应用身份（tenant_access_token）调用时的过滤行为
- 特殊字段的返回条件

### 模板示例

`tenant_access_token` 的最大有效期是 2 小时。

- 剩余有效期小于 30 分钟时，调用本接口会返回一个新的 `tenant_access_token`，这会同时存在两个有效的 `tenant_access_token`。
- 剩余有效期大于等于 30 分钟时，调用本接口会返回原有的 `tenant_access_token`。

## 权限要求

### 必要权限

#### 模板说明

调用该 API **必须开启**的权限。开启其中任意一项权限即可调用该接口。

权限类型通常为：
- `应用权限（开启任一即可）` - 应用需要配置的权限

#### 模板示例

| 类型 | 名称 |
|----------|----------|
| 无权限要求 | 该接口无需任何权限 |

### 可选权限

#### 模板说明

敏感字段的权限要求。如果无需获取这些敏感字段，则不需要申请这些权限。

权限类型通常为：
- `字段权限（敏感字段）` - 敏感字段需要的权限

#### 模板示例

该接口无敏感字段权限要求。

## 接口信息

### 模板说明

接口信息表格展示接口的基本信息，包括：

- **API 路径**：接口的完整 URL
- **请求方法**：GET/POST/PUT/DELETE 等
- **调用频率限制**：每分钟/每秒的调用次数限制
- **支持的应用类型**：Custom App 或 Store App
- **文档地址**：飞书开放平台的文档链接

### 模板示例

| API 路径 | `https://open.feishu.cn/open-apis/auth/v3/tenant_access_token/internal` |
|----------|------------------------------------------------------------------------|
| 请求方法 | POST |
| 调用频率限制 | - |
| 支持的应用类型 | Custom App |
| 文档地址 | [飞书开放平台](https://open.feishu.cn/document/ukTMukTMukTM/reference/auth-v3/tenant_access_token/internal) |

## 接口请求

### 请求头

#### 模板说明

HTTP 请求头字段，用于身份认证和内容类型声明。

**如果某个字段有权限要求，要在"描述"字段中注明权限要求**。权限名称的格式为：`获取用户 user ID (contact:user.employee_id:readonly)`。参考请求参数下模板示例中的 `user_id_type` 权限要求写法。

#### 模板示例

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `Content-Type` | string | 是 | **固定值**："application/json; charset=utf-8" |

### 请求参数

#### 模板说明

URL 查询参数或路径参数，用于传递请求所需的数据。

**如果某个参数有权限要求，要在"描述"字段中注明权限要求**。权限名称的格式为：`获取用户 user ID (contact:user.employee_id:readonly)`。参考请求参数下模板示例中的 `user_id_type` 权限要求写法。

#### 模板示例

该接口无 URL 查询参数。

### 请求体

#### 模板说明

POST/PUT 请求的 JSON body，GET 请求通常无请求体。

**如果请求体中有字段有权限要求，要在"描述"字段中注明权限要求**。权限名称的格式为：`获取用户 user ID (contact:user.employee_id:readonly)`。参考请求参数下模板示例中的 `user_id_type` 权限要求写法。

#### 模板示例

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `app_id` | string | 是 | 应用唯一标识，创建应用后获得。有关 `app_id` 的详细介绍，请参考[通用参数](https://open.feishu.cn/document/ukTMukTMukTM/uYTM5UjL2ETO14iNxkTN/terminology)介绍<br>示例值：`"cli_slkdjalasdkjasd"` |
| `app_secret` | string | 是 | 应用秘钥，创建应用后获得。有关 `app_secret` 的详细介绍，请参考[通用参数](https://open.feishu.cn/document/ukTMukTMukTM/uYTM5UjL2ETO14iNxkTN/terminology)介绍<br>示例值：`"dskLLdkasdjlasdKK"` |

### 请求示例

#### 模板说明

代码示例展示如何调用该接口，以 Go 和 Java 为例。

#### 模板示例

##### Go 请求示例

```go
import (
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

##### Java 请求示例

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

### 响应头

#### 模板说明

HTTP 响应头字段，通常该接口无额外响应头。

**如果某个字段有权限要求，要在"描述"字段中注明权限要求**。权限名称的格式为：`获取用户 user ID (contact:user.employee_id:readonly)`。参考请求参数下模板示例中的 `user_id_type` 权限要求写法。

#### 模板示例

| 名称 | 类型 | 描述 |
|------|------|------|
| - | - | 无额外响应头字段 |

### 响应体

#### 模板说明

JSON 响应体结构，包含 code、msg 和 data 字段。

**如果某个字段有权限要求，要在"描述"字段中注明权限要求**。权限名称的格式为：`获取用户 user ID (contact:user.employee_id:readonly)`。参考请求参数下模板示例中的 `user_id_type` 权限要求写法。

#### 模板示例

| 字段 | 类型 | 描述 |
|------|------|------|
| `code` | int | 错误码，非 0 取值表示失败 |
| `msg` | string | 错误描述 |
| `tenant_access_token` | string | 租户访问凭证 |
| `expire` | int | `tenant_access_token` 的过期时间，单位为秒 |

### 响应示例

#### 模板说明

完整的响应 JSON 示例。

#### 模板示例

```json
{
    "code": 0,
    "msg": "ok",
    "tenant_access_token": "t-caecc734c2e3328a62489fe0648c4b98779515d3",
    "expire": 7200
}
```

## 响应码定义

### 模板说明

响应码表格列出该接口可能返回的 HTTP 状态码、错误码或成功码。

**请按以下顺序组织响应码**：

1. **成功码**（2xx）放在最上边，表示请求成功处理
2. **客户端错误码**（4xx）在中间，表示客户端请求问题
3. **服务端错误码**（5xx）在最后，表示服务端错误

这样可以快速区分成功和错误情况。

### 模板示例

| HTTP状态码 | 错误码 | 描述 |
|------------|--------|------|
| 200 | 0 | 请求成功 |
| 400 | - | 请求参数错误 |
| 401 | - | 应用凭证无效 |
| 500 | - | 服务器内部错误 |

## 附录

### 模板说明

附录是一个总括性的章节，用于存放接口文档的补充信息。

通过模板在生成接口文档时，会根据接口实际情况自动判断是否需要添加额外的补充信息章节，补充信息章节必须用二级分类章节的形式。请参考"模板示例"下的"相关链接"

### 模板示例

#### 相关链接

| 链接类型 | 链接 |
|----------|------|
| 通用参数 | [https://open.feishu.cn/document/ukTMukTMukTM/uYTM5UjL2ETO14iNxkTN/terminology](https://open.feishu.cn/document/ukTMukTMukTM/uYTM5UjL2ETO14iNxkTN/terminology) |
| 通用错误码 | [https://open.feishu.cn/document/ukTMukTMukTM/ugjM14COyUjL4ITN](https://open.feishu.cn/document/ukTMukTMukTM/ugjM14COyUjL4ITN) |