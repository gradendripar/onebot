!!! tip "适用场景"

    - OneBot 实现能主动访问到应用端（后者有公网 IP，或两者在同一局域网内）
    - 对性能要求不高，要求接入简单

!!! tip "建议 OneBot 实现提供的配置项"

    - `url`：Webhook 上报地址
    - `access_token`：访问令牌
    - `timeout`：上报请求超时时间，单位：毫秒，0 表示不超时

    本页后续将使用 `配置项名称` 或 `<配置项名称>` 的形式引用上述配置项的内容。

OneBot 实现**应该**根据用户配置，在发生事件时，向指定的 `url` 使用 `POST` 请求推送事件，并根据情况将 HTTP 响应体的内容解析为动作请求列表，依次处理，丢弃动作响应。

## 请求头

OneBot 实现**必须**在请求时设置以下请求头：

- `Content-Type: application/json`
- `User-Agent`：具体的 UA 值**可以**由实现自行定义
    - 例如 `User-Agent: OneBot/12 (qq) Go-LibOneBot/1.0.0`
- `X-OneBot-Version: <onebot_version>`：`<onebot_version>` **应**为实现的 OneBot 标准版本
- `X-Impl: <impl>`：`<impl>` **应**为实现的名称，格式为 `[_a-z]+`
- `X-Platform: <platform>`：`<platform>` **应**为实现所针对的机器人平台名称，格式为 `[_a-z]+`
- `X-Self-ID: <self_id>`：`<self_id>` **应**为当前所“登录”的机器人 ID

如果配置了 `access_token`，还**应该**设置：

- `Authorization: Bearer <access_token>`

## 请求体

请求体中**必须**使用 JSON 和 UTF-8 编码的字符串表示事件。

## 超时

如果配置了 `timeout`，**应**在 HTTP 请求所用时间超过其值时认为事件推送失败。

## 响应

如果响应状态码为 `204 No Content`，**应**认为事件推送成功，并不做更多处理。

如果响应状态码为 `200 OK`，也**应**认为事件推送成功，此时**应该**根据响应头中的 `Content-Type` 将响应体解析为动作请求列表，依次处理动作请求，丢弃动作响应。

对于后一种情况，OneBot 实现**必须**同时支持两种 `Content-Type` 响应头：

- `application/json`：在响应体中使用 JSON 和 UTF-8 编码的字符串表示动作请求列表
- `application/msgpack`：在响应体中使用 MessagePack 编码的字节序列表示动作请求列表

如果响应状态码不是上述的任一个，**应**认为事件推送失败。

## 错误

- 如果尝试将响应体解析为动作请求列表并执行的任何一步出错，只需要输出日志，**不应该**向应用端返回错误