# 公开 API

## `send_private_msg` 发送私聊消息

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `user_id` | number | - | 对方 QQ 号 |
| `message` | message | - | 要发送的内容 |
| `auto_escape` | boolean | `false` | 消息内容是否作为纯文本发送（即不解析 CQ 码），只在 `message` 字段是字符串时有效 |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `message_id` | number (int32) | 消息 ID |

## `send_group_msg` 发送群消息

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `message` | message | - | 要发送的内容 |
| `auto_escape` | boolean | `false` | 消息内容是否作为纯文本发送（即不解析 CQ 码），只在 `message` 字段是字符串时有效 |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `message_id` | number (int32) | 消息 ID |

## `send_discuss_msg` 发送讨论组消息

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `discuss_id` | number | - | 讨论组 ID（正常情况下看不到，需要从讨论组消息上报的数据中获得） |
| `message` | message | - | 要发送的内容 |
| `auto_escape` | boolean | `false` | 消息内容是否作为纯文本发送（即不解析 CQ 码），只在 `message` 字段是字符串时有效 |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `message_id` | number (int32) | 消息 ID |

## `send_msg` 发送消息

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `message_type` | string | - | 消息类型，支持 `private`、`group`、`discuss`，分别对应私聊、群组、讨论组，如不传入，则根据传入的 `*_id` 参数判断 |
| `user_id` | number | - | 对方 QQ 号（消息类型为 `private` 时需要） |
| `group_id` | number | - | 群号（消息类型为 `group` 时需要） |
| `discuss_id` | number | - | 讨论组 ID（消息类型为 `discuss` 时需要） |
| `message` | message | - | 要发送的内容 |
| `auto_escape` | boolean | `false` | 消息内容是否作为纯文本发送（即不解析 CQ 码），只在 `message` 字段是字符串时有效 |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `message_id` | number (int32) | 消息 ID |

## `delete_msg` 撤回消息

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `message_id` | number (int32) | - | 消息 ID |

### 响应数据

无

## `send_like` 发送好友赞

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `user_id` | number | - | 对方 QQ 号 |
| `times` | number | 1 | 赞的次数，每个好友每天最多 10 次 |

### 响应数据

无

## `set_group_kick` 群组踢人

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `user_id` | number | - | 要踢的 QQ 号  |
| `reject_add_request` | boolean | `false` | 拒绝此人的加群请求 |

### 响应数据

无

## `set_group_ban` 群组单人禁言

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `user_id` | number | - | 要禁言的 QQ 号 |
| `duration` | number | `30 * 60` | 禁言时长，单位秒，0 表示取消禁言 |

### 响应数据

无

## `set_group_anonymous_ban` 群组匿名用户禁言

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `anonymous` | object | - | 可选，要禁言的匿名用户对象（群消息上报的 `anonymous` 字段） |
| `anonymous_flag` 或 `flag` | string | - | 可选，要禁言的匿名用户的 flag（需从群消息上报的数据中获得） |
| `duration` | number | `30 * 60` | 禁言时长，单位秒，无法取消匿名用户禁言 |

上面的 `anonymous` 和 `anonymous_flag` 两者任选其一传入即可，若都传入，则使用 `anonymous`。

### 响应数据

无

## `set_group_whole_ban` 群组全员禁言

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `enable` | boolean | `true` | 是否禁言 |

### 响应数据

无

## `set_group_admin` 群组设置管理员

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `user_id` | number | - | 要设置管理员的 QQ 号 |
| `enable` | boolean | `true` | true 为设置，false 为取消 |

### 响应数据

无

## `set_group_anonymous` 群组匿名

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `enable` | boolean | `true` | 是否允许匿名聊天 |

### 响应数据

无

## `set_group_card` 设置群名片（群备注）

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `user_id` | number | - | 要设置的 QQ 号 |
| `card` | string | 空 | 群名片内容，不填或空字符串表示删除群名片 |

### 响应数据

无

## `set_group_leave` 退出群组

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `is_dismiss` | boolean | `false` | 是否解散，如果登录号是群主，则仅在此项为 true 时能够解散 |

### 响应数据

无

## `set_group_special_title` 设置群组专属头衔

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `user_id` | number | - | 要设置的 QQ 号 |
| `special_title` | string | 空 | 专属头衔，不填或空字符串表示删除专属头衔 |
| `duration` | number | `-1` | 专属头衔有效期，单位秒，-1 表示永久，不过此项似乎没有效果，可能是只有某些特殊的时间长度有效，有待测试 |

### 响应数据

无

## `set_discuss_leave` 退出讨论组

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `discuss_id` | number | - | 讨论组 ID（正常情况下看不到，需要从讨论组消息上报的数据中获得） |

### 响应数据

无

## `set_friend_add_request` 处理加好友请求

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `flag` | string | - | 加好友请求的 flag（需从上报的数据中获得） |
| `approve` | boolean | `true` | 是否同意请求 |
| `remark` | string | 空 | 添加后的好友备注（仅在同意时有效） |

### 响应数据

无

## `set_group_add_request` 处理加群请求／邀请

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `flag` | string | - | 加群请求的 flag（需从上报的数据中获得） |
| `sub_type` 或 `type` | string | - | `add` 或 `invite`，请求类型（需要和上报消息中的 `sub_type` 字段相符） |
| `approve` | boolean | `true` | 是否同意请求／邀请 |
| `reason` | string | 空 | 拒绝理由（仅在拒绝时有效） |

### 响应数据

无

## `set_group_name` 设置群名

### 参数

| 字段名   | 数据类型 | 说明 |
| -------- | ------ | ---- |
| `group_id` | number (int64)  | 群号 |
| `group_name` | string | 新群名 |

## `get_group_msg` 获取群历史消息

### 参数

| 字段名         | 数据类型  | 说明   |
| ------------ | ----- | ------ |
| `message_id` | number (int32) | 消息 ID |

### 响应数据

| 字段名         | 数据类型    | 说明       |
| ------------ | ------- | ---------- |
| `message_id` | number (int32) | 消息 ID     |
| `sender`     | object  | 发送者     |
| `time`       | number (int32) | 发送时间   |
| `content`    | message | 消息内容   |

其中 `sender` 字段参考 [群消息事件](../event/message.md#群消息)。

## `get_forward_msg` 获取合并转发内容

### 参数

| 字段名         | 数据类型   | 说明   |
| ------------ | ------ | ------ |
| `message_id` | string | 消息id |

### 响应数据

| 字段名       | 类型              | 说明     |
| ---------- | ----------------- | -------- |
| `messages` | forward message[] | 消息列表 |

## `send_group_forward_msg` 发送合并转发(群)

### 参数

| 字段名       | 数据类型           | 说明                         |
| ---------- | -------------- | ---------------------------- |
| `group_id` | number (int64) | 群号                         |
| `messages` | forward node[] | 自定义转发消息, 具体看CQCode |

### 响应数据

无

## `get_login_info` 获取登录号信息

### 参数

无

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `user_id` | number (int64) | QQ 号 |
| `nickname` | string | QQ 昵称 |

## `get_stranger_info` 获取陌生人信息

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `user_id` | number | - | QQ 号 |
| `no_cache` | boolean | `false` | 是否不使用缓存（使用缓存可能更新不及时，但响应更快） |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `user_id` | number (int64) | QQ 号 |
| `nickname` | string | 昵称 |
| `sex` | string | 性别，`male` 或 `female` 或 `unknown` |
| `age` | number (int32) | 年龄 |

## `get_friend_list` 获取好友列表

### 参数

无

### 响应数据

响应内容为 JSON 数组，每个元素如下：

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `user_id` | number (int64) | QQ 号 |
| `nickname` | string | 昵称 |
| `remark` | string | 备注名 |

## `get_group_list` 获取群列表

### 参数

无

### 响应数据

响应内容为 JSON 数组，每个元素如下：

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `group_id` | number (int64) | 群号 |
| `group_name` | string | 群名称 |

## `get_group_info` 获取群信息

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `no_cache` | boolean | `false` | 是否不使用缓存（使用缓存可能更新不及时，但响应更快） |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `group_id` | number (int64) | 群号 |
| `group_name` | string | 群名称 |
| `member_count` | number (int32) | 成员数 |
| `max_member_count` | number (int32) | 最大成员数（群容量） |

## `get_group_member_info` 获取群成员信息

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |
| `user_id`  | number | - | QQ 号 |
| `no_cache` | boolean | `false` | 是否不使用缓存（使用缓存可能更新不及时，但响应更快） |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `group_id` | number (int64) | 群号 |
| `user_id` | number (int64) | QQ 号 |
| `nickname` | string | 昵称 |
| `card` | string | 群名片／备注 |
| `sex` | string | 性别，`male` 或 `female` 或 `unknown` |
| `age` | number (int32) | 年龄 |
| `area` | string | 地区 |
| `join_time` | number (int32) | 加群时间戳 |
| `last_sent_time` | number (int32) | 最后发言时间戳 |
| `level` | string | 成员等级 |
| `role` | string | 角色，`owner` 或 `admin` 或 `member` |
| `unfriendly` | boolean | 是否不良记录成员 |
| `title` | string | 专属头衔 |
| `title_expire_time` | number (int32) | 专属头衔过期时间戳 |
| `card_changeable` | boolean | 是否允许修改群名片 |

## `get_group_member_list` 获取群成员列表

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `group_id` | number | - | 群号 |

### 响应数据

响应内容为 JSON 数组，每个元素的内容和上面的 `get_group_member_info` 接口相同，但对于同一个群组的同一个成员，获取列表时和获取单独的成员信息时，某些字段可能有所不同，例如 `area`、`title` 等字段在获取列表时无法获得，具体应以单独的成员信息为准。

## `get_cookies` 获取 Cookies

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `domain` | string | 空 | 需要获取 cookies 的域名 |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `cookies` | string | Cookies |

## `get_csrf_token` 获取 CSRF Token

### 参数

无

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `token` | number (int32) | CSRF Token |

## `get_credentials` 获取 QQ 相关接口凭证

即上面两个接口的合并。

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `domain` | string | 空 | 需要获取 cookies 的域名 |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `cookies` | string | Cookies |
| `csrf_token` | number (int32) | CSRF Token |

## `get_record` 获取语音

:::tip 提示
要使用此接口，通常需要安装 ffmpeg，请参考 CQHTTP 实现的相关说明。
:::

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `file` | string | - | 收到的语音文件名（消息段的 `file` 参数），如 `0B38145AA44505000B38145AA4450500.silk` |
| `out_format`  | string | - | 要转换到的格式，目前支持 `mp3`、`amr`、`wma`、`m4a`、`spx`、`ogg`、`wav`、`flac` |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `file` | string | 转换后的语音文件路径，如 `/home/somebody/cqhttp/data/record/0B38145AA44505000B38145AA4450500.mp3` |

## `get_image` 获取图片

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `file` | string | - | 收到的图片文件名（消息段的 `file` 参数），如 `6B4DE3DFD1BD271E3297859D41C530F5.jpg` |

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `file` | string | 下载后的图片文件路径，如 `/home/somebody/cqhttp/data/image/6B4DE3DFD1BD271E3297859D41C530F5.jpg` |

## `can_send_image` 检查是否可以发送图片

### 参数

无

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `yes` | boolean | 是或否 |

## `can_send_record` 检查是否可以发送语音

### 参数

无

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `yes` | boolean | 是或否 |

## `get_status` 获取运行状态

### 参数

无

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `online` | boolean | 当前 QQ 在线，`null` 表示无法查询到在线状态 |
| `good` | boolean | CQHTTP 状态符合预期，意味着各模块正常运行、功能正常，且 QQ 在线 |
| …… | - | CQHTTP 实现自行添加的其它内容 |

通常情况下建议只使用 `online` 和 `good` 这两个字段来判断运行状态，因为根据 CQHTTP 实现的不同，其它字段可能完全不同。

## `get_version_info` 获取版本信息

### 参数

无

### 响应数据

| 字段名 | 数据类型 | 说明 |
| ----- | ------- | --- |
| `coolq_directory` | string | （兼容性需求）CKYU 根目录路径 |
| `coolq_edition` | string | （兼容性需求）CKYU 版本，`air` 或 `pro` |
| `plugin_version` | string | CQHTTP 版本，例如 `2.1.3` |
| `plugin_build_number` | number | CQHTTP build 号 |
| `plugin_build_configuration` | string | CQHTTP 编译配置，`debug` 或 `release` |

## `set_restart_plugin` 重启 CQHTTP

由于重启 CQHTTP 同时需要重启 API 服务，这意味着当前的 API 请求会被中断，因此需要异步地重启，接口返回的 `status` 是 `async`。

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `delay` | number | `0` | 要延迟的毫秒数，如果默认情况下无法重启，可以尝试设置延迟为 2000 左右 |

### 响应数据

无

## `clean_data_dir` 清理数据目录

用于清理积攒了太多旧文件的数据目录，如 `image`。

### 参数

| 字段名 | 数据类型 | 默认值 | 说明 |
| ----- | ------- | ----- | --- |
| `data_dir` | string | - | 收到清理的目录名，支持 `image`、`record`、`show`、`bface` |

### 响应数据

无

## `clean_plugin_log` 清理日志

用于清空 CQHTTP 的日志文件。

### 参数

无

### 响应数据

无