# Chat 模块设计

## 职责

处理用户与 AI 的对话流程，包括消息发送、流式接收、历史管理。

## 类设计

```
ChatManager
├── sendMessage(content: string) → void
├── stopGeneration() → void
├── clearHistory() → void
└── loadSession(sessionId: string) → void

MessageModel
├── messages: list<Message>
├── append(message: Message) → void
└── updateLast(chunk: string) → void
```

## 状态机

```
Idle → Sending → Streaming → Idle
                           ↘ Error
```

## 关键流程

1. 用户输入消息
2. 构建请求（注入记忆 + 历史上下文）
3. 调用 Claude API（流式）
4. 逐 token 更新 UI
5. 完成后持久化消息

## 依赖

- `MemoryManager`：获取相关记忆
- `StorageService`：持久化消息
- `ClaudeApiClient`：HTTP 请求
