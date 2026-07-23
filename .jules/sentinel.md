# Sentinel's Journal - Critical Learnings

## 2024-11-20 - [Telegram Markdown Parsing Failures and Input Validation]
**Vulnerability:** Telegram Bot API sendMessage failure (DoS) due to unescaped markdown special characters (`_`, `*`, `` ` ``, `[`) in user-controlled form inputs when `parse_mode: 'Markdown'` is enabled. Additionally, missing input length constraints on the frontend could lead to database or system exhaustion.
**Learning:** Raw, unescaped user strings passed directly into markdown-formatted templates can break parsing and make the Telegram API reject the entire request. This silently disables notifications for crucial operational events.
**Prevention:** Always run user-submitted content through a proper escaping function (escaping special characters like `_`, `*`, `` ` ``, `[`) before embedding them in a Markdown message. Apply strict `maxlength` attributes to inputs to limit payload sizes on the frontend.
