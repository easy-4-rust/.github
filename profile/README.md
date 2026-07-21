# Easy-4-Rust

<p align="center">
  <img alt="Easy-4-Rust" src="./assets/banner.svg" width="800">
</p>

<p align="center">
  <strong>面向 Rust 的易用工具集 —— 将经典 Java 工具库以 idiomatic Rust 重铸，覆盖文档、安全、工具箱等高频场景</strong>
</p>

<p align="center">
  <a href="https://github.com/easy-4-rust"><img alt="Repos" src="https://img.shields.io/badge/Repos-TBD-blue?style=flat-square"></a>
  <a href="https://github.com/easy-4-java"><img alt="Java Counterpart" src="https://img.shields.io/badge/Counterpart-easy--4--java-blue?style=flat-square&logo=openjdk"></a>
  <a href="https://github.com/ddd-4-rust"><img alt="Architecture" src="https://img.shields.io/badge/Architecture-ddd--4--rust-orange?style=flat-square&logo=rust"></a>
  <a href="https://github.com/partme-ai"><img alt="Ecosystem" src="https://img.shields.io/badge/Ecosystem-partme--ai-6366f1?style=flat-square"></a>
  <a href="https://github.com/easy-4-rust/.github/blob/main/profile/LICENSE"><img alt="License" src="https://img.shields.io/badge/License-Apache_2.0-green?style=flat-square"></a>
</p>

---

## 关于我们

**Easy-4-Rust** 是 partme-ai 开源生态旗下的**易用工具集**组织，专注于将 Java 生态的经典工具库（EasyExcel / Hutool / Sa-Token 等）以 idiomatic、production-oriented Rust 重铸。

我们的核心理念是：

> **让 Rust 开发者拥有和 Java 同样"开箱即用"的高频工具体验，同时享受 Rust 的内存安全与零成本抽象。**

### 设计原则

- **🦀 Idiomatic Rust** — 充分利用所有权、错误处理（`Result`）、trait 抽象，不做 Java 直译
- **📦 模块化** — 每个 crate 独立可装，按需引入，无强制依赖
- **⚡ 高性能** — 流式处理、零拷贝优先、async 友好
- **🧪 Production-ready** — 完整测试覆盖、CI / CD、版本化发布
- **🔗 与 Java 兼容** — 输出格式（OFD/PDF/DOCX/Excel）字节级兼容 Java 版本

---

## 工具集矩阵

### 文档处理（Document）

| Crate | 说明 | Java 原型 |
|-------|------|----------|
| [easyexcel-rs](https://github.com/easy-4-rust/easyexcel-rs) | EasyExcel 兼容的流式 Excel 框架 | [EasyExcel](https://github.com/alibaba/easyexcel) |
| [easypdf-rs](https://github.com/easy-4-rust/easypdf-rs) | 简洁 PDF 操作库，零 unsafe 纯 Rust | Apache PDFBox |
| [easyofd-rs](https://github.com/easy-4-rust/easyofd-rs) | OFD（开放版式文档）操作库 | 自研 |
| [easydoc-rs](https://github.com/easy-4-rust/easydoc-rs) | DOCX 模板生成与排版 | docx4j |

### 安全与权限（Security）

| Crate | 说明 | Java 原型 |
|-------|------|----------|
| [sa-token-rs](https://github.com/easy-4-rust/sa-token-rs) | 认证鉴权框架 | [Sa-Token](https://github.com/dromara/Sa-Token) |
| `sa-token-core`（子 crate） | 核心 API | — |
| `sa-token-dao-memory`（子 crate） | 内存 DAO | — |
| `sa-token-derive`（子 crate） | 宏支持 | — |
| `sa-token-test`（子 crate） | 测试辅助 | — |

### 工具箱（Toolkit）

| Crate | 说明 | Java 原型 |
|-------|------|----------|
| [hitool-rs](https://github.com/easy-4-rust/hitool-rs) | Hutool 能力模型 Rust 版 | [Hutool](https://github.com/dromara/hutool) |

---

## 架构概览

```
┌─────────────────────────────────────────────────────────────┐
│                 easy-4-rust 工具集矩阵                       │
├─────────────────────────────────────────────────────────────┤
│  文档处理   │ easyexcel-rs · easypdf-rs · easyofd-rs ·      │
│            │ easydoc-rs                                    │
├─────────────────────────────────────────────────────────────┤
│  安全鉴权   │ sa-token-rs (core / dao / derive / test)      │
├─────────────────────────────────────────────────────────────┤
│  通用工具   │ hitool-rs                                     │
├─────────────────────────────────────────────────────────────┤
│   ↓ 基础设施层（依赖）                                      │
│  ddd-4-rust · rbatis-plus · tokio · serde · ...            │
└─────────────────────────────────────────────────────────────┘
```

---

## 快速开始

### 在 `Cargo.toml` 中添加依赖

```toml
[dependencies]
# 文档处理
easyexcel-rs = "0.1"
easypdf-rs   = "0.1"

# 安全鉴权
sa-token-rs = "0.1"

# 通用工具
hitool-rs = "0.1"

# 运行时
tokio = { version = "1", features = ["full"] }
serde = { version = "1", features = ["derive"] }
```

### 示例：流式导出 Excel

```rust
use easyexcel_rs::prelude::*;

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let mut writer = ExcelWriter::open("users.xlsx").await?;
    writer.write_header(["id", "name", "email"]).await?;

    for user in fetch_users().await? {
        writer.write_row(&[user.id, user.name, user.email]).await?;
    }

    writer.finish().await?;
    Ok(())
}
```

### 示例：Sa-Token 鉴权

```rust
use sa_token_rs::prelude::*;

#[tokio::main]
async fn main() -> Result<(), Box<dyn std::error::Error>> {
    let cfg = SaTokenConfig::builder()
        .token_name("satoken")
        .timeout(7200)
        .build();

    SaTokenManager::init(cfg).await?;
    let token = SaTokenManager::login("user-1001").await?;
    println!("login token: {}", token);
    Ok(())
}
```

---

## 与 Java 版本对齐

| 能力 | Java | Rust | 状态 |
|------|------|------|------|
| 流式 Excel | easyexcel | easyexcel-rs | ✅ |
| PDF 操作 | itextpdf / pdfbox | easypdf-rs | ✅ |
| OFD 版式 | easyofd | easyofd-rs | ✅ |
| DOCX 模板 | docx4j-template | easydoc-rs | ✅ |
| 认证鉴权 | sa-token | sa-token-rs | ✅ |
| 工具箱 | hutool | hitool-rs | ✅ |

> **输出兼容**：所有文档类库与对应 Java 版本**字节级兼容**，可直接替换生产环境中的 Java 模块。

---

## 相关生态

| 组织 | 说明 |
|------|------|
| 🧰 [easy-4-java](https://github.com/easy-4-java) | Java 工具集（一一对应） |
| 🏛️ [ddd-4-rust](https://github.com/ddd-4-rust) | DDD 基础构件 |
| 💾 [rbatis-plus](https://github.com/rbatis-plus) | ORM 生态 |
| 🧠 [partme-ai](https://github.com/partme-ai) | 顶层 AI 智能体生态 |

---

## 贡献指南

欢迎贡献新的工具 crate！

1. **Fork** 目标仓库
2. 创建特性分支
3. 遵循既有 crate 命名与 API 风格
4. 补充单元测试、文档与 CHANGELOG
5. 提交 **Pull Request**

> 新 crate 提案请先在 [Discussions](https://github.com/orgs/easy-4-rust/discussions) 发起 RFC。

---

## 联系我们

- Email: [partmeai@gmail.com](mailto:partmeai@gmail.com)
- GitHub: [github.com/easy-4-rust](https://github.com/easy-4-rust)

---

<div align="center">

**让 Rust 拥有 Java 同样易用的工具体验**

Made with ❤️ by PartMe AI Team

</div>