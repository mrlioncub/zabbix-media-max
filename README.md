# Zabbix Media Type — MAX

Send Zabbix notifications to [MAX](https://max.ru) messenger via Webhook.

> REDME [Russian](https://github.com/noakky/zabbix-media-max/blob/main/README.ru.md)
---

## Requirements

- Zabbix 7.0+
- A bot on the MAX platform

---

## Getting the Bot Token

1. Open [business.max.ru](https://business.max.ru/self)
2. Navigate to: **Chat-bots → Integration → Get token**
3. Enable **"Allow adding to group chats"** if you need to send to group chats

---

## Installation

### 1. Import the media type

`Administration → Media types → Import` — upload the `zbx_export_mediatypes.yaml` file

### 2. Configure the media type

Open the imported **MAX** media type and fill in the parameters:

| Parameter | Value | Required |
|-----------|-------|:---:|
| `Token` | MAX bot token | ✅ |
| `UserId` | MAX user ID | ⚠️ |
| `ChatId` | MAX group chat ID | ⚠️ |
| `Format` | `html` or `markdown` | — |

> ⚠️ Specify **only one** of: `UserId` **or** `ChatId`. Providing both will result in an error.

### 3. Configure user media

`Administration → Users → <user> → Media → Add`

- **Type**: `MAX`
- **Send to**: user ID or chat ID

#### How to get a chat ID

Add the bot to the chat, then run:

```bash
curl -X GET "https://platform-api.max.ru/chats" \
  -H "Authorization: <token>"
```

Find the target chat in the response and copy the `chat_id` value.

---

## Message Formatting

The `Format` parameter supports two modes:

**HTML**: `<b>bold</b>`, `<i>italic</i>`, `<code>code</code>`, `<a href="...">link</a>`

**Markdown**: `**bold**`, `*italic*`, `` `code` ``, `[link](url)`