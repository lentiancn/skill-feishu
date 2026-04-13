# 发送消息

## 说明

调用该接口向指定用户或者群聊发送消息。支持发送的消息类型包括文本、富文本、卡片、群名片、个人名片、图片、视频、音频、文件以及表情包等。

**注意事项**：
- 应用需要开启[机器人能力](https://open.feishu.cn/document/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-enable-bot-ability)，开启能力后需要发布版本才能生效
- 给用户发送消息时，用户需要在机器人的可用范围内
- 给群组发送消息时，机器人需要在该群组中且在群组内拥有发言权限
- 为避免消息发送频繁打扰用户，向同一用户发送消息限频为 5 QPS，向同一群组发送消息限频为群内机器人共享 5 QPS
- 该接口仅支持在开发者后台创建的应用机器人调用，群自定义机器人无法调用该接口

## 权限要求

### 必要权限

| 类型 | 名称 |
|----------|----------|
| 应用权限（开启任一即可） | 获取与发送单聊、群组消息 (im:message) |
| 应用权限（开启任一即可） | 以应用的身份发消息 (im:message:send_as_bot) |
| 应用权限（开启任一即可） | 发送消息V2 (im:message:send) |

### 可选权限

| 类型 | 名称 |
|----------|----------|
| 字段权限（敏感字段） | 获取用户 user ID (contact:user.employee_id:readonly) |
| 用户身份权限 | 以用户身份发送消息 (im:message.send_as_user) |

> **说明**：
> - 用户身份发消息需同时申请获取与发送单聊、群组消息 (im:message) 和以用户身份发送消息 (im:message.send_as_user) 两个权限
> - 敏感字段仅在开启对应权限后才会返回；如无需获取这些字段，不建议申请

## 接口信息

| API 路径 | `https://open.feishu.cn/open-apis/im/v1/messages` |
|----------|---------------------------------------------------|
| 请求方法 | POST |
| 调用频率限制 | 1000 次/分钟、50 次/秒 |
| 支持的应用类型 | Custom App、Store App |
| 文档地址 | [飞书开放平台](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/im-v1/message/create) |

## 接口请求

### 请求头

HTTP 请求头字段，用于身份认证和内容类型声明。

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `Authorization` | string | 是 | `tenant_access_token` 或 `user_access_token`<br>值格式："Bearer `access_token`"<br>示例值："Bearer u-7f1bcd13fc57d46bac21793a18e560"<br>**了解更多**：[如何选择与获取 access token](https://open.feishu.cn/document/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-choose-which-type-of-token-to-use) |
| `Content-Type` | string | 是 | 固定值："application/json; charset=utf-8" |

### 请求参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `receive_id_type` | string | 是 | 消息接收者 ID 类型<br>支持 `open_id`/`union_id`/`user_id`/`email`/`chat_id`<br>**可选值**：<br>- `open_id`：标识一个用户在某个应用中的身份<br>- `union_id`：标识一个用户在某个应用开发商下的身份<br>- `user_id`：标识一个用户在某个租户内的身份<br>- `email`：以用户的真实邮箱来标识用户<br>- `chat_id`：以群 ID 来标识群聊<br>**字段权限**：当值为 `user_id` 时，需要获取用户 user ID (contact:user.employee_id:readonly) |

### 请求体

| 名称 | 类型 | 必填 | 描述 |
|------|------|------|------|
| `receive_id` | string | 是 | 消息接收者的 ID，ID 类型与 `receive_id_type` 参数一致<br>**注意事项**：<br>- 给用户发送消息时，用户需要在机器人的可用范围内<br>- 给群组发送消息时，机器人需要在该群组中且在群组内拥有发言权限<br>- 推荐使用用户的 `open_id` |
| `msg_type` | string | 是 | 消息类型<br>可选值：text、post、image、file、audio、media、sticker、interactive、share_chat、share_user、system |
| `content` | string | 是 | 消息内容，JSON 结构序列化后的字符串<br>**注意**：<br>- JSON 字符串需进行转义（如换行符 `\n` 转义为 `\\n`）<br>- 文本消息最大不超过 150 KB<br>- 卡片消息、富文本消息最大不超过 30 KB<br>- 图片/音频/视频/文件需先上传，使用 Key 发送 |
| `uuid` | string | 否 | 自定义设置的唯一字符串序列，用于请求去重<br>长度不超过 50 字符<br>相同 uuid 在 1 小时内至多成功发送一条消息 |

### 请求示例

##### cURL 请求示例

```bash
curl --location --request POST 'https://open.feishu.cn/open-apis/im/v1/messages?receive_id_type=chat_id' \
--header 'Authorization: Bearer t-XXX' \
--header 'Content-Type: application/json; charset=utf-8' \
--data-raw '{
    "receive_id": "oc_84983ff6516d731e5b5f68d4ea2e1da5",
    "msg_type": "text",
    "content": "{\"text\":\"test content\"}"
}'
```

##### Python 请求示例

```python
import json
import requests

def send():
    url = "https://open.feishu.cn/open-apis/im/v1/messages"
    params = {"receive_id_type":"chat_id"}
    msg = "text content"
    msgContent = {
        "text": msg,
    }
    req = {
        "receive_id": "oc_xxx",
        "msg_type": "text",
        "content": json.dumps(msgContent)
    }
    payload = json.dumps(req)
    headers = {
        'Authorization': 'Bearer xxx',
        'Content-Type': 'application/json'
    }
    response = requests.request("POST", url, params=params, headers=headers, data=payload)
    print(response.headers['X-Tt-Logid'])
    print(response.content)

if __name__ == '__main__':
    send()
```

##### Go 请求示例

请参考[机器人自动拉群报警教程（含 Go 示例代码）](https://open.feishu.cn/document/uAjLw4CM/ukTMukTMukTM/reference/im-v1/message-development-tutorial/determine-the-api-and-event-to-call)

## 接口响应

### 响应头

| 名称 | 类型 | 描述 |
|------|------|------|
| - | - | 无额外响应头字段 |

### 响应体

| 字段 | 类型 | 描述 |
|------|------|------|
| `code` | int | 错误码，非 0 表示失败 |
| `msg` | string | 错误描述 |
| `data` | object | 响应数据，根据接口类型动态变化 |

### 响应示例

```json
{
    "code": 0,
    "msg": "success",
    "data": {
        "message_id": "om_dc13264520392913993dd051dba21dcf",
        "root_id": "om_40eb06e7b84dc71c03e009ad3c754195",
        "parent_id": "om_d4be107c616aed9c1da8ed8068570a9f",
        "thread_id": "omt_d4be107c616a",
        "msg_type": "interactive",
        "create_time": "1615380573411",
        "update_time": "1615380573411",
        "deleted": false,
        "updated": false,
        "chat_id": "oc_5ad11d72b830411d72b836c20",
        "sender": {
            "id": "cli_9f427eec54ae901b",
            "id_type": "app_id",
            "sender_type": "app",
            "tenant_key": "736588c9260f175e"
        },
        "body": {
            "content": "{\"text\":\"@_user_1 test content\"}"
        },
        "mentions": [
            {
                "key": "@_user_1",
                "id": "ou_155184d1e73cbfb8973e5a9e698e74f2",
                "id_type": "open_id",
                "name": "Tom",
                "tenant_key": "736588c9260f175e"
            }
        ],
        "upper_message_id": "om_40eb06e7b84dc71c03e009ad3c754195"
    }
}
```

## 响应码定义

### 成功码

| HTTP状态码 | 错误码 | 描述 |
|------------|--------|------|
| 200 | 0 | 请求成功 |

### 客户端错误码 (4xx)

| HTTP状态码 | 错误码 | 描述 |
|------------|--------|------|
| 400 | 230001 | Your request contains an invalid request parameter. |
| 400 | 230002 | The bot can not be outside the group. |
| 400 | 230006 | Bot ability is not activated. |
| 400 | 230013 | Bot has NO availability to this user. |
| 400 | 230015 | P2P chat can NOT be shared. |
| 400 | 230017 | Bot is NOT the owner of the resource. |
| 400 | 230018 | These operations are NOT allowed at current group settings. |
| 400 | 230019 | The topic does NOT exist. |
| 400 | 230020 | This operation triggers the frequency limit. |
| 400 | 230022 | The content of the message contains sensitive information. |
| 400 | 230025 | The length of the message content reaches its limit. |
| 400 | 230027 | Lack of necessary permissions. |
| 400 | 230099 | Failed to create card content. |
| 400 | 230028 | The messages do NOT pass the audit. |
| 400 | 230029 | User has resigned. |
| 400 | 230034 | The receive_id is invalid. |
| 400 | 230035 | Send Message Permission deny. |
| 400 | 230036 | Tenant crypt key has been deleted. |
| 400 | 230038 | Cross tenant p2p chat operate forbid. |
| 400 | 230049 | The message is being sent. |
| 400 | 230053 | The user has stopped the bot from sending messages. |
| 400 | 230054 | This type of message is unavailable in the connection group. |
| 400 | 230055 | The type of file upload does not match the type of message being sent. |
| 400 | 230075 | Sending encrypted messages is not supported. |
| 400 | 232009 | Your request specifies a chat which has already been dissolved. |

### 230099 子错误码

| 错误码 | 描述 |
|--------|------|
| 100290 | Failed to create card content, ext=ErrCode: 100290; ErrMsg: There is an invalid user resource(at/person) in your card |
| 11310 | Failed to create card content, ext=ErrCode: 11310; ErrMsg: %v; code:230099 |
| 200380 | Failed to create card content, ext=ErrCode: 200380; ErrMsg: template does not exist |
| 200381 | Failed to create card content, ext=ErrCode: 200381; ErrMsg: template is not visible to app |
| 200621 | Failed to create card content, ext=ErrCode: 200621; ErrMsg: parse card json err |
| 200732 | Failed to create card content, ext=ErrCode: 200732; ErrMsg: the actual type of the variable is inconsistent with the specified type |
| 200737 | Failed to create card content, ext=ErrCode: 200737; ErrMsg: the format of the variable is incorrect |
| 200550 | Failed to create card content, ext=ErrCode: 200550; ErrMsg: chart spec is invalid |
| 200861 | Failed to create card content, ext=ErrCode: 200861; ErrMsg: cards of schema V2 no longer support this capability |
| 200570 | Failed to create card content, ext=ErrCode: 200570; ErrMsg: card contains invalid image keys |
| 200914 | table rows is invalid |
| 200915 | table rows name is invalid |
| 300240 | Failed to create card content, ext=ErrCode: 300240; ErrMsg: This application cannot retrieve audio information |
| 300230 | Failed to create card content, ext=ErrCode: 300230; ErrMsg: duplicate audio id |
| 300220 | Failed to create card content, ext=ErrCode: 300220; ErrMsg: audio elem don't support forward |

## 附录

### 相关链接

| 链接类型 | 链接 |
|----------|------|
| 机器人能力启用 | [https://open.feishu.cn/document/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-enable-bot-ability](https://open.feishu.cn/document/uAjLw4CM/ugTN1YjL4UTN24CO1UjN/trouble-shooting/how-to-enable-bot-ability) |
| 可用范围配置 | [https://open.feishu.cn/document/home/introduction-to-scope-and-authorization/availability](https://open.feishu.cn/document/home/introduction-to-scope-and-authorization/availability) |
| 权限范围校验 | [https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority](https://open.feishu.cn/document/ukTMukTMukTM/uETNz4SM1MjLxUzM/v3/guides/scope_authority) |
| 通用错误码 | [https://open.feishu.cn/document/ukTMukTMukTM/ugjM14COyUjL4ITN](https://open.feishu.cn/document/ukTMukTMukTM/ugjM14COyUjL4ITN) |
