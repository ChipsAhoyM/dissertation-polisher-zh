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

- 检测并去除论文中的 AI 写作痕迹
- 检查论文格式和写作规范（"我们"残留、"本X"作用域、图表引用、参考文献格式等）
- 润色学术表达，确保正式学术语体
- 生成结构化的合规性检查报告

**与通用 humanizer 的核心区别：** 本工具不追求"让文本像人随意写的"，而是确保文本符合正式学术论文规范。

## 功能概览

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

### 合规性报告
自动生成包含 Critical / Warning / Suggestion 三级分类的结构化报告。

### 质量评分
7 维度评分体系（总分 70）：规范合规、AI 痕迹、学术表达、章节衔接、术语一致、逻辑连贯、技术准确。

## 安装

### 方法一：通过 npx 一键安装（推荐）

```bash
npx skills add https://github.com/op7418/Humanizer-zh.git
```

### 方法二：通过 Git 克隆

```bash
git clone https://github.com/op7418/Humanizer-zh.git ~/.claude/skills/dissertation-polisher-zh
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

### 基础用法

```
/dissertation-polisher-zh 请润色以下博士论文摘要：

[粘贴论文文本]
```

### 使用场景示例

#### 场景 1：润色论文摘要

**输入：**
```
请润色以下博士论文摘要：

此外，我们提出了一种新颖的图像增强方法。值得注意的是，该方法不仅具有高效性，而且具有鲁棒性和通用性。
```

**输出包含：**
1. 润色后文本（附行内修改说明）
2. 合规性检查报告（Critical/Warning/Suggestion 分级）
3. 质量评分（7 维度）

#### 场景 2：审阅正文章节

```
请审阅第三章（3.1-3.4节）的正文，检查规范合规性：

[粘贴章节内容]
```

#### 场景 3：检查参考文献格式

```
请检查以下参考文献列表的格式一致性：

[粘贴参考文献]
```

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
