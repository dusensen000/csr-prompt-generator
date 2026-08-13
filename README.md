# CSR Prompt Generator Skill

[English](#english) | [中文](#中文)

---

## 中文

### 简介

CSR Prompt Generator 是一个用于生成临床试验（Clinical Study Report）章节提示词的 Claude Skill。它能够根据例文自动分析章节类型，选择合适的模板，并生成高质量的提示词。

### 功能特点

- **智能章节类型识别**：自动识别 7 种内容类型（定义型、数据摘要型、数据列举型、设计讨论型、流程型、综合讨论型、简单章节型）
- **动态子章节生成**：支持 TFL 数据驱动和 CSP/SAP 内容驱动的动态子章节
- **多阶段工作流**：支持 CSP/SAP → TFL 的多阶段内容生成
- **通用化处理**：自动将具体数据转换为占位符模板
- **质量控制**：内置数据校验、异常处理和统一写作规则

### 目录结构

```
csr-prompt-generator/
├── SKILL.md                    # 主技能文件
├── README.md                   # 说明文档
├── references/
│   ├── content-types.md        # 内容类型分类
│   ├── prompt-templates.md     # 提示词模板库
│   └── common-rules.md         # 通用规则库
└── evals/
    └── evals.json              # 评估用例
```

### 安装

1. 将此仓库克隆到本地：
```bash
git clone https://github.com/dusensen000/csr-prompt-generator.git
```

2. 将文件夹复制到 Claude Skills 目录：
```bash
# Windows
cp -r csr-prompt-generator C:\Users\你的用户名\.claude\skills\

# macOS/Linux
cp -r csr-prompt-generator ~/.claude/skills/
```

3. 重启 Claude 以加载新 Skill

### 使用方法

#### 基本用法

在 Claude 中输入章节信息，Skill 会自动：

1. 分析例文特征
2. 识别章节类型
3. 选择合适的模板
4. 生成提示词

#### 输入格式

```
使用 csr-prompt-generator，生成下面这个章节的提示词，保存在 ./test 文件夹中

[章节号 章节标题]
例文内容...
```

#### 示例

**输入：**
```
使用 csr-prompt-generator，生成下面这个章节的提示词

[9.7.1.13.1 药物暴露]
金妥昔单抗的平均暴露持续时间为22.21周（SD：22.379）...
```

**输出：**
生成完整的提示词文件，包含任务描述、检索策略、写作规律等

### 支持的章节类型

| 类型 | 说明 | 典型章节 |
|------|------|----------|
| 定义型 | 从 CSP/SAP 提取原文定义 | 9.* 章节 |
| 数据摘要型 | 从 TFL 表格提取汇总数据 | 10.*, 11.2.*, 12.* |
| 数据列举型 | 从 TFL 表格提取详细列表 | 12.2.2, 12.3.* |
| 设计讨论型 | 整合多源信息形成论述 | 9.2, 9.4.4 |
| 流程型 | 描述研究执行流程 | 9.6, 10.2 |
| 综合讨论型 | 整合表格数据和文献引用 | 13.1, 14.1 |
| 简单章节型 | 例文简短，固定格式输出 | 11.4.3-11.4.5 |

### 模板说明

| 模板 | 适用场景 |
|------|----------|
| 模板 A | 定义型（从 CSP/SAP 提取） |
| 模板 B-1/B-2 | 数据摘要型（含/不含占位符） |
| 模板 C-1/C-2 | 数据列举型（含/不含占位符） |
| 模板 D | 设计讨论型 |
| 模板 E | 流程型 |
| 模板 F | TFL 数据驱动型动态子章节 |
| 模板 G | CSP/SAP 内容驱动型动态子章节 |
| 模板 H | 多阶段工作流（CSP/SAP → TFL） |
| 模板 I | 简单章节型 |

### 配置

Skill 会自动从以下位置读取配置：

- **TFL 表格目录**：`folderPath`
- **CSP/SAP 文档路径**：`documentPath`
- **Listing 目录**：`folderPath`（用于生成引用）

### 贡献

欢迎提交 Issue 和 Pull Request！

1. Fork 本仓库
2. 创建特性分支：`git checkout -b feature/amazing-feature`
3. 提交更改：`git commit -m 'Add amazing feature'`
4. 推送到分支：`git push origin feature/amazing-feature`
5. 创建 Pull Request

### 许可证

MIT License

---

## English

### Introduction

CSR Prompt Generator is a Claude Skill for generating Clinical Study Report (CSR) chapter prompts. It automatically analyzes chapter types based on example text, selects appropriate templates, and generates high-quality prompts.

### Features

- **Smart Chapter Type Recognition**: Automatically identifies 7 content types
- **Dynamic Sub-chapter Generation**: Supports TFL data-driven and CSP/SAP content-driven dynamic sub-chapters
- **Multi-phase Workflow**: Supports CSP/SAP → TFL multi-phase content generation
- **Generalization Processing**: Automatically converts specific data to placeholder templates
- **Quality Control**: Built-in data validation, exception handling, and unified writing rules

### Installation

1. Clone this repository:
```bash
git clone https://github.com/dusensen000/csr-prompt-generator.git
```

2. Copy to Claude Skills directory:
```bash
# Windows
cp -r csr-prompt-generator C:\Users\YourUsername\.claude\skills\

# macOS/Linux
cp -r csr-prompt-generator ~/.claude/skills/
```

3. Restart Claude to load the new Skill

### Usage

```
Use csr-prompt-generator to generate a prompt for the following chapter

[Chapter Number Chapter Title]
Example text...
```

### Supported Content Types

| Type | Description | Typical Chapters |
|------|-------------|------------------|
| Definition | Extract from CSP/SAP | 9.* |
| Data Summary | Extract from TFL tables | 10.*, 11.2.*, 12.* |
| Data Enumeration | Extract detailed lists from TFL | 12.2.2, 12.3.* |
| Design Discussion | Integrate multi-source info | 9.2, 9.4.4 |
| Process | Describe research process | 9.6, 10.2 |
| Comprehensive Discussion | Integrate tables and literature | 13.1, 14.1 |
| Simple Chapter | Short example, fixed format | 11.4.3-11.4.5 |

### Contributing

Contributions are welcome! Please feel free to submit Issues and Pull Requests.

### License

MIT License
