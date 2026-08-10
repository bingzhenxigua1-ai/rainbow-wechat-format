# rainbow-wechat-format

> 将 Markdown 文章转化为微信公众号彩虹风排版 HTML。

采用彩虹渐变头图、彩色圆角卡片、emoji 图标、暖色调（橙/黄/绿/蓝/粉）风格，适配移动端阅读。适用于 [WorkBuddy](https://www.codebuddy.cn/) 技能体系。

## 效果预览

生成的 HTML 包含以下视觉组件：

- **彩虹头图** — 渐变背景 + 浮动 emoji 吉祥物
- **章节卡片** — 圆角白底卡片 + 彩色序号徽章（奇数章橙→黄，偶数章绿→蓝）
- **高亮提示框** — 用于重点结论
- **公式展示框** — 用于需要突出的计算/规则
- **避坑列表** — 粉色主题的避坑指南
- **时间线** — 按阶段/年级分步展示
- **彩色标签** — 支持 `.orange` / `.blue` / `.pink` 变体
- **结论块** — 渐变橙色收尾

## 配色体系

| 变量 | 色值 | 用途 |
|------|------|------|
| `--bg` | `#FFF9E6` | 页面背景 |
| `--orange` | `#FF9A56` | 暖色系 |
| `--yellow` | `#FFD93D` | 暖色系 |
| `--green` | `#7BC77E` | 清新系 |
| `--blue` | `#74C0FC` | 清新系 |
| `--pink` | `#FF9AA2` | 警告/避坑 |

## 安装

将本仓库克隆到 WorkBuddy 技能目录：

```bash
git clone https://github.com/bingzhenxigua1-ai/rainbow-wechat-format.git ~/.workbuddy/skills/rainbow-wechat-format
```

## 使用

在 WorkBuddy 对话中触发以下任一表达即可自动调用：

- 「用彩虹风排版」
- 「用上次那个风格排版」
- 「公众号排版」
- 「微信推文排版」
- 「彩虹风排版」
- 「用那个彩虹色排版」

提供一篇 Markdown 文章，技能会读取 `assets/template.html` 模板，解析文章结构（标题、章节、列表、加粗、结论），并按设计规范生成完整的彩虹风 HTML。

## 目录结构

```
rainbow-wechat-format/
├── SKILL.md              # 技能定义（触发条件 + 工作流程 + 设计规范）
├── assets/
│   └── template.html     # 完整设计模板（所有组件 + CSS）
├── references/           # 参考文档（预留）
├── scripts/              # 脚本（预留）
└── README.md
```

## 技术细节

- 纯 HTML + CSS，无外部依赖
- 移动端优先，小屏幕（<480px）字号自动缩小
- 链接保留原 href，样式为蓝色虚线下划线
- emoji 图标按语义匹配：🏆竞赛、🎤口语、💪体测、⚠️风险、📊数据、🎯目标
- 章节序号徽章颜色交替：奇数章橙→黄渐变，偶数章绿→蓝渐变

## License

MIT
