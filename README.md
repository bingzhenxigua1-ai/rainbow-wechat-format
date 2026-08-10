# WorkBuddy Skills

> 个人 WorkBuddy 技能合集，持续更新。

本仓库统一管理多个 [WorkBuddy](https://www.codebuddy.cn/) 技能（Skill），每个技能存放在 `skills/` 下的独立子目录中。

## 技能列表

| 技能 | 说明 | 目录 |
|------|------|------|
| rainbow-wechat-format | 将 Markdown 文章转化为微信公众号彩虹风排版 HTML | [`skills/rainbow-wechat-format`](skills/rainbow-wechat-format) |

## 目录结构

```
.
├── README.md                           # 本文件（技能索引）
├── LICENSE                             # MIT
├── .gitignore
└── skills/                             # 所有技能存放于此
    └── rainbow-wechat-format/          # 单个技能目录
        ├── SKILL.md                    # 技能定义（触发条件 + 工作流程）
        ├── README.md                   # 技能详细文档
        ├── assets/                     # 模板、图片等静态资源
        ├── references/                 # 参考文档
        └── scripts/                    # 辅助脚本
```

## 安装单个技能

```bash
# 克隆仓库
git clone https://github.com/bingzhenxigua1-ai/rainbow-wechat-format.git /tmp/wb-skills

# 将需要的技能复制到 WorkBuddy 技能目录
cp -r /tmp/wb-skills/skills/rainbow-wechat-format ~/.workbuddy/skills/
```

## 安装全部技能

```bash
cp -r /tmp/wb-skills/skills/* ~/.workbuddy/skills/
```

## 添加新技能

1. 在 `skills/` 下创建新目录，命名为技能名
2. 目录内至少包含 `SKILL.md`（技能定义文件）
3. 可选添加 `assets/`、`references/`、`scripts/` 等子目录
4. 更新本 README 的技能列表表格
5. 提交并推送

## License

MIT
