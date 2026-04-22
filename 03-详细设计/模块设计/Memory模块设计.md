# Memory 模块设计

## 职责

管理用户的持久记忆，支持记忆的存储、检索、更新和删除。

## 记忆类型

| 类型 | 描述 | 示例 |
|------|------|------|
| 用户信息 | 基本偏好与背景 | 职业、兴趣 |
| 事件记忆 | 重要对话事件 | 决定、约定 |
| 知识记忆 | 共同建立的知识 | 专有名词定义 |

## 类设计

```
MemoryManager
├── addMemory(content: string, tags: list) → Memory
├── searchMemories(query: string) → list<Memory>
├── deleteMemory(id: string) → void
└── getRelevantMemories(context: string) → list<Memory>
```

## 记忆检索策略

1. **关键词匹配**：基于标签的快速过滤
2. **语义检索**（可选）：向量相似度

## 记忆注入时机

- 每次新对话开始时，注入 Top-N 条相关记忆
- 对话中用户明确提及时，动态补充

## 自动记忆提取

对话结束后，可选触发摘要提取新记忆。
