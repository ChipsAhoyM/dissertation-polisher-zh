# Dissertation Polisher ZH: 中文计算机科学博士学位论文润色工具

> **来源与致谢：**
> - **基础框架**：改造自 [humanizer-zh](https://github.com/op7418/Humanizer-zh)（基于 [blader/humanizer](https://github.com/blader/humanizer)）
> - **AI 写作特征**：[Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)，WikiProject AI Cleanup 维护
> - **写作规范**：北大CameraLab的博士论文写作指导
> - **参考范文**：北大 CS 博士论文
> - **审稿案例**：来自导师对实际论文的评审反馈

---

## 项目简介

Dissertation Polisher ZH 是一个专门面向**计算机科学博士学位论文**的中文润色工具。它能够：

- **读取长文档**：支持 PDF、DOCX、LaTeX 文件路径输入，自动分批读取全文（120+ 页博士论文）
- 检测并去除论文中的 AI 写作痕迹
- 检查论文格式和写作规范（"我们"残留、"本X"作用域、图表引用、参考文献格式等）
- 逐章分析 + 跨章一致性检查（术语、符号、参考文献格式）
- **输出 MD 审阅报告文件**：逐章组织的详细修改意见，每个问题附精确引文、完整改写建议和原因说明

**与通用 humanizer 的核心区别：** 本工具不追求"让文本像人随意写的"，而是确保文本符合正式学术论文规范。

## 功能概览

### 支持的输入格式

| 格式 | 读取方式 | 备注 |
|------|---------|------|
| PDF | `Read` 工具 + `pages` 参数，每次 20 页分批读取 | 自动定位目录、按章节边界读取 |
| DOCX | `textutil` 转 txt 后读取 | macOS 原生支持 |
| LaTeX 单文件 | 直接读取 `.tex` | |
| LaTeX 多文件 | 自动发现主文件，解析 `\input`/`\include` 顺序 | |
| 文本粘贴 | 用户直接粘贴（向后兼容） | 简化为单章分析 |

### 处理流程

1. **文档摄入** — 根据文件类型自动选择读取策略
2. **结构图构建** — 从目录提取章节结构，向用户确认
3. **逐章分析** — 37 个 AI 模式 + 8 条核心规则 + 各章类型专项规则（只报告确实存在具体违规的问题，不输出空洞警告）
4. **跨章一致性检查** — 术语、符号、"本X"作用域、参考文献、图表编号、章节衔接
5. **生成 MD 审阅报告** — 写入 `{输入文件名}_审阅报告.md`

### 八条核心规则
1. 消灭"我们" — 零容忍
2. 删除 AI 填充词
3. 校准"本X"作用域
4. 打破 AI 公式结构
5. 确保章节衔接
6. 术语一致性
7. 精确动词
8. 量化表述

### AI 模式检测
- **8 个改造自 humanizer-zh 的模式**（针对学术语境重新校准）
- **29 个新增论文专用模式**（涵盖"我们"残留、作用域错误、翻译痕迹、图表规范、参考文献格式等）

### 审阅报告输出

报告为 MD 文件，结构如下：
- **概览评估** — 总体评价 + 7 维度质量评分简表（总分 70）
- **逐章审阅** — 每章按 Critical/Warning/Suggestion 分级，每个问题含精确引文 + 完整改写建议 + 原因说明，章末附修改要点总结
- **跨章节一致性检查** — 术语对照表、符号一致性、参考文献格式、章节衔接
- **快速检查清单** — 14 项逐项 ✅/❌
- **修改优先级建议** — 分三轮：必须修改 → 建议修改 → 锦上添花

## 安装

### 方法一：通过 npx 一键安装（推荐）

```bash
npx skills add https://github.com/ChipsAhoyM/dissertation-polisher-zh.git
```

### 方法二：通过 Git 克隆

```bash
git clone https://github.com/ChipsAhoyM/dissertation-polisher-zh.git ~/.claude/skills/dissertation-polisher-zh
```

### 方法三：手动安装

1. 下载本项目
2. 将文件夹复制到 Claude Code 的 skills 目录：
   - **macOS/Linux**: `~/.claude/skills/`
   - **Windows**: `%USERPROFILE%\.claude\skills\`

3. 确保文件夹结构如下：
   ```
   ~/.claude/skills/dissertation-polisher-zh/
   ├── SKILL.md       # 技能定义文件
   └── README.md      # 说明文档
   ```

## 使用

### 场景 1：审阅完整论文（推荐）

```
/dissertation-polisher-zh 请审阅我的博士论文：/path/to/thesis.pdf
```

工具会自动读取 PDF、定位目录、按章节分批分析，最终在同目录输出 `thesis_审阅报告.md`。

### 场景 2：审阅 DOCX 格式论文

```
/dissertation-polisher-zh 请审阅：~/Documents/博士论文终稿.docx
```

### 场景 3：审阅 LaTeX 项目

```
/dissertation-polisher-zh 请审阅：~/thesis/main.tex
```

自动发现项目中所有 `.tex` 文件，按 `\input`/`\include` 顺序读取。

### 场景 4：粘贴文本片段（向后兼容）

```
/dissertation-polisher-zh 请润色以下博士论文摘要：

[粘贴论文文本]
```

直接在聊天中输出单章审阅结果。

## 检测的问题类型

### Critical（严重问题 — 必须修改）
- "我们"残留（B1）
- "本X"作用域错误（B2）
- 论文拼接痕迹（B3）
- 缺少章节衔接段（B5）
- 贡献表述不当（B6）
- 图表引用不规范（B7）
- 英文术语翻译不一致（B8）
- 四级标题（B9）
- 参考文献格式不一致（B10）
- 第一章缺少框架图（B11）
- 英文缩略语管理不当（B21）
- 章节称谓不规范（B25）
- 小论文翻译痕迹（B27）
- 绪论篇幅不足（B28）
- 结论展望不足（B29）

### Warning（警告 — 建议修改）
- 口语化/GPT 风格表达（B4）
- 第二章缺少相关工作梳理图（B12）
- 目录标题不当（B15）
- 表格/插图索引中出现来源标注（B17）
- 废话/凑字数（B18）
- 夸大贡献（B20）
- 公式标点不统一（B22）
- 图中英文未汉化（B23）
- 图片字体不统一（B24）
- 概念引入位置不当（B26）

### Suggestion（建议 — 可选改进）
- 正文章节缺少与第一章呼应的插图（B13）
- 页面大面积空白（B14）
- 图片风格不统一（B16）
- 已发表方法过时未讨论（B19）

## 文件说明

- **`SKILL.md`** — 技能定义文件（完整规则和检测模式）
- **`README.md`** — 本说明文档

## 参考资源

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) — AI 写作特征指南
- [blader/humanizer](https://github.com/blader/humanizer) — 原始英文版项目
- [op7418/Humanizer-zh](https://github.com/op7418/Humanizer-zh) — 原始中文版项目

## 许可

本项目遵循原项目的许可协议。

---

**提示：** 本工具面向正式学术论文润色，不适用于博客、营销文案等非学术文本。如需通用去 AI 化处理，请使用原版 [humanizer-zh](https://github.com/op7418/Humanizer-zh)。
