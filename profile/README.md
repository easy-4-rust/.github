# Easy-4-Rust

> **🦀 Rust 易用工具集** —— 由 [@hiwepy](https://github.com/hiwepy) 开发与收集
>
> 文档格式、通用工具等高频场景的 idiomatic Rust 工具集

<p align="center">
  <img alt="Easy-4-Rust" src="./assets/banner.svg" width="800">
</p>

<p align="center">
  <a href="https://github.com/easy-4-rust"><img alt="Repos" src="https://img.shields.io/badge/Repos-5-blue?style=flat-square"></a>
  <a href="https://github.com/easy-4-java"><img alt="Java Counterpart" src="https://img.shields.io/badge/Counterpart-easy--4--java-blue?style=flat-square&logo=openjdk"></a>
  <a href="https://github.com/ddd-4-rust"><img alt="Architecture" src="https://img.shields.io/badge/Architecture-ddd--4--rust-orange?style=flat-square&logo=rust"></a>
  <a href="https://github.com/partme-ai"><img alt="Ecosystem" src="https://img.shields.io/badge/Ecosystem-partme--ai-6366f1?style=flat-square"></a>
  <a href="https://github.com/easy-4-rust/.github/blob/main/profile/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache_2.0-green?style=flat-square"></a>
</p>

---

## 关于本组织

**Easy-4-Rust** 是 [partme-ai](https://github.com/partme-ai) 开源生态下的 Rust 工具集组织，专门托管由 [@hiwepy](https://github.com/hiwepy) **原创**和**收集**的 Rust crate —— 面向**文档格式处理**、**通用工具**等高频场景。

> 📌 **重要说明**：本组织**不托管**以下常见开源项目的镜像或 fork：
> - [`easyexcel`](https://github.com/alibaba/easyexcel) —— Alibaba 开源项目，独立维护
> - [`sa-token`](https://github.com/dromara/Sa-Token) —— dromara 开源项目，独立维护
> - [`hutool`](https://github.com/dromara/hutool) —— dromara 开源项目，独立维护
>
> 这些项目都有完整的官方仓库，**请直接使用官方版本**。

---

## 🧰 工具集矩阵

### 文档处理（Document）

| Crate | 说明 | 状态 |
|-------|------|:---:|
| [`easyexcel-rs`](https://github.com/easy-4-rust/easyexcel-rs) | 流式 Excel 框架（独立实现，API 类似 EasyExcel） | ✅ |
| [`easypdf-rs`](https://github.com/easy-4-rust/easypdf-rs) | 简洁 PDF 操作库，纯 Rust，零 unsafe | ✅ |
| [`easyofd-rs`](https://github.com/easy-4-rust/easyofd-rs) | OFD（开放版式文档）操作库 | ✅ |
| [`easydoc-rs`](https://github.com/easy-4-rust/easydoc-rs) | DOCX 模板生成与排版 | ✅ |

### 安全与权限（Security）

| Crate | 说明 | 状态 |
|-------|------|:---:|
| [`sa-token-rs`](https://github.com/easy-4-rust/sa-token-rs) | 认证鉴权框架（独立实现，API 类似 Sa-Token） | ✅ |

### 通用工具（Toolkit）

| Crate | 说明 | 状态 |
|-------|------|:---:|
| [`hitool-rs`](https://github.com/easy-4-rust/hitool-rs) | Hutool 能力模型的 Rust 风格实现（独立原创） | ✅ |

### 不在本组织（保持独立）

| 项目 | 说明 | 维护方 |
|------|------|--------|
| `easyexcel` | 流式 Excel 框架 | [alibaba/easyexcel](https://github.com/alibaba/easyexcel) |
| `sa-token` | 认证鉴权框架（Java） | [dromara/Sa-Token](https://github.com/dromara/Sa-Token) |
| `hutool` | Java 工具箱 | [dromara/hutool](https://github.com/dromara/hutool) |

> 以上 Java 工具**不属于本组织托管**，需要时请直接访问对应官方仓库。

---

## 🏛️ 架构概览

```
┌─────────────────────────────────────────────────────────────┐
│                  easy-4-rust 工具集矩阵                      │
├─────────────────────────────────────────────────────────────┤
│  文档处理   │ easyexcel-rs · easypdf-rs · easyofd-rs ·      │
│            │ easydoc-rs                                    │
├─────────────────────────────────────────────────────────────┤
│  通用工具   │ hitool-rs                                     │
├─────────────────────────────────────────────────────────────┤
│   ↓ 基础设施层（依赖）                                      │
│  ddd-4-rust · rbatis-plus · tokio · serde · ...            │
└─────────────────────────────────────────────────────────────┘
```

---

## 🚀 快速开始

> ⚠️ **尚未发布到 crates.io。** 在发布之前，使用 git 依赖：

```toml
[dependencies]
# 文档处理（任选）
easyexcel-rs = { git = "https://github.com/easy-4-rust/easyexcel-rs" }
easypdf-rs   = { git = "https://github.com/easy-4-rust/easypdf-rs" }
easyofd-rs   = { git = "https://github.com/easy-4-rust/easyofd-rs" }
easydoc-rs   = { git = "https://github.com/easy-4-rust/easydoc-rs" }

# 通用工具
hitool-rs    = { git = "https://github.com/easy-4-rust/hitool-rs" }

# 运行时
tokio = { version = "1", features = ["full"] }
serde = { version = "1", features = ["derive"] }
```

> 各 crate 的具体 API 与使用示例，请直接查看对应仓库的 README。

---

## 📚 相关生态

| 组织 | 说明 |
|------|------|
| 🧰 [easy-4-java](https://github.com/easy-4-java) | Java 镜像组织（筹备中，暂未发布） |
| 🏛️ [ddd-4-rust](https://github.com/ddd-4-rust) | DDD 基础构件 Rust 版 |
| 🏛️ [ddd-4-java](https://github.com/ddd-4-java) | DDD 基础构件 Java 版 |
| 💾 [rbatis-plus](https://github.com/rbatis-plus) | RBatis ORM 增强生态 |
| 🧠 [partme-ai](https://github.com/partme-ai) | 顶层 AI 智能体生态品牌 |

---

## 🤝 贡献指南

欢迎贡献新的工具 crate！

1. **Fork** 目标仓库
2. 创建特性分支
3. 遵循既有 crate 命名与 API 风格
4. 补充单元测试、文档与 CHANGELOG
5. 提交 **Pull Request**

> 新 crate 提案请先在 [Discussions](https://github.com/orgs/easy-4-rust/discussions) 发起 RFC。

---

## 📄 License

本组织下所有 crate 采用 [Apache 2.0](LICENSE) 开源许可证。

---

<div align="center">

**Made with ❤️ by [PartMe AI Team](https://github.com/partme-ai)**

</div>
