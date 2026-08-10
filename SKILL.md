---
name: rainbow-wechat-format
description: 将 Markdown 文章转化为微信公众号彩虹风排版 HTML。采用彩虹渐变头图、彩色圆角卡片、emoji 图标、暖色调（橙/黄/绿/蓝/粉）风格。当用户要求「彩虹风排版」「公众号排版」「微信推文排版」「用上次那个风格排版」或任何需要将文章排版成彩虹风格的场景时使用。也适用于需要将文档转化为精美 HTML 排版的场合。
agent_created: true
---

# 公众号彩虹风排版

将任意 Markdown 文章转化为彩虹风公众号排版 HTML，采用彩虹渐变头图、暖色调、圆角卡片、emoji 图标体系，适配移动端阅读。

## 触发条件

当用户说以下任意表达时使用此技能：
- 「用彩虹风排版」
- 「用上次那个风格排版」
- 「公众号排版」
- 「微信推文排版」
- 「彩虹风排版」
- 「用那个彩虹色排版」

## 工作流程

### 1. 读取输入

从用户提供的文件路径读取 Markdown 内容。如果用户直接粘贴文本而非提供文件路径，则将文本暂存后再处理。

### 2. 读取模板

读取 `assets/template.html` 以了解完整的设计结构和 CSS 类名体系。该模板包含所有视觉组件的标准用法示例。

### 3. 分析文章结构

将 Markdown 内容解析为以下结构：
- 标题（一级标题）→ 文章标题
- 导语段落 → lead 块
- 一级章节标题（`##`）→ section 卡片
- 二级标题（`###`）→ sub-section
- 列表 → checklist / 标签
- 加粗文本 → 重点高亮
- 结论段落 → conclusion 块

### 4. 生成 HTML

按 `assets/template.html` 的设计标准生成 HTML。遵循以下设计规范：

#### 配色体系（CSS 变量）
- `--bg: #FFF9E6` 页面背景
- `--orange: #FF9A56`, `--yellow: #FFD93D` 暖色系
- `--green: #7BC77E`, `--blue: #74C0FC` 清新系
- `--pink: #FF9AA2` 警告/避坑

#### 组件用法
- **彩虹头图**: `<header class="header">` + 渐变背景 + 浮动 emoji 吉祥物
- **章节卡片**: `<section class="section">` + 彩色序号圆形徽章
- **高亮提示**: `<div class="highlight-box">` 用于重点结论
- **公式展示**: `<div class="formula">` 用于需要重点突出的计算/规则
- **避坑列表**: `<div class="pitfalls">` + `<div class="pitfall-item">` 粉色主题
- **时间线**: `<div class="timeline">` + `<div class="timeline-item">` 用于按时间/年级分阶段
- **结论**: `<div class="conclusion">` 渐变橙色收尾
- **标签**: `<span class="tag">` 彩色标签，可选 `.orange/.blue/.pink` 变体

#### 排版规则
1. 小屏幕（<480px）字号自动缩小
2. 链接保留原 href，样式为蓝色虚线下划线
3. 所有引用来源以灰色小字标注在对应段落下方
4. emoji 图标按语义匹配：🏆竞赛、🎤口语、💪体测、⚠️风险、📊数据、🎯目标
5. 章节序号徽章颜色交替：奇数章用橙→黄渐变，偶数章用绿→蓝渐变

### 5. 输出

将生成的 HTML 保存为文件，文件名与输入文件名相同但后缀改为 `.html`，输出到 outputs 目录。使用 present_files 展示结果。

## 模板参考

完整设计模板位于 `assets/template.html`，包含所有组件和 CSS 样式。生成 HTML 时应以该模板的设计标准为准。
