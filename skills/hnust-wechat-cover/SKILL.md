---
name: hnust-wechat-cover
agent_created: true
description: 当用户需要生成校园新媒体风格的微信公众号封面、首图、小封面、兼顾大小封面或校园新媒体配图时使用。触发词：公众号封面、校园封面、高校公众号封面。
---

# 公众号封面生成器

## 概览

按校园新媒体公众号的年轻化、校园化视觉风格生成封面图。支持公众号首图（900×383）、小封面（383×383）以及兼顾大小封面（1283×383）三种常用尺寸。

该风格特征鲜明：高频使用品牌字母、校徽蓝、校园红砖建筑与湖景，风格横跨活泼拼贴、手绘插画、实景新闻、清新扁平插画和城市旅行拼贴五大方向。

## 触发条件

在以下任一情况触发本 skill：

- 用户提到"公众号封面""校园封面""高校公众号封面"
- 用户上传公众号封面截图并要求模仿风格
- 用户希望生成"校园新媒体风""高校公众号风"封面

## 尺寸判断

| 图片类型 | 尺寸 | 使用场景 |
|---|---|---|
| 公众号首图 / 大封面 | 900 × 383 | 单篇文章首图 |
| 公众号小封面 | 383 × 383 | 小图展示区的方形裁切区 |
| 兼顾大小封面 | 1283 × 383 | 同时满足大封面与小封面展示 |
| 公众号次图 | 200 × 200 | 多图文次条封面 |

用户只说"封面"或"公众号封面"时，优先建议兼顾大小封面 `1283 × 383`。

## 风格选择

根据用户主题推荐以下五种公众号常见风格之一。如用户未指定风格，给出 2-3 个建议并等待选择。

| 风格 | 关键词 | 适用主题 |
|---|---|---|
| 活泼拼贴风 | 彩虹背景、表情包、生活贴纸、品牌字母 | 开学、社团、美食、轻松话题 |
| 手绘插画风 | 卡通人物、对话框、暖橙色、手写体 | 迎新、交友、心理、校园活动 |
| 实景新闻风 | 校园实景、红色遮罩、粗黑标题 | 通知、权威发布、招生、重要新闻 |
| 清新扁平插画风 | 扁平建筑、湖水倒影、柔和渐变 | 校园风光、节气、招生宣传 |
| 城市旅行拼贴风 | 高铁、地标、贴纸白边、蓝天 | 假期、旅行、返乡、城市主题 |

详细视觉规范见 `references/style-guide.md`。

## 工作流程

### 步骤 1：提取需求

从用户请求中提取以下信息：

1. 图片类型（首图 / 小封面 / 兼顾大小封面 / 次图）
2. 文章主题或内容摘要
3. 主标题和辅助文案（如无，根据主题给出 2-3 个建议）
4. 风格偏好（活泼拼贴 / 手绘插画 / 实景新闻 / 清新扁平 / 城市旅行）
5. 必须出现的元素（如品牌字母、校徽、特定建筑、特定配色）
6. 需要避免的内容

信息不足时，先整理已知信息，给出合理建议，再追问最关键的一个缺口。不要一次性抛出所有问题。

### 步骤 2：确认生成信息

调用图片生成工具前，向用户汇总最终生图信息并等待明确确认。确认格式：

```
我先汇总一下生图信息：
- 图片类型与尺寸：【类型】，【宽】×【高】 px
- 主题内容：【摘要】
- 文案：【主文案 / 辅助文案 / 无文字】
- 风格：【五种风格之一】
- 画面元素：【必须出现的元素】
- 避免内容：【限制或无】
- 生成方式：【如为兼顾大小封面，写明先生成 900×383 和 383×383，再拼接为 1283×383】

确认后我再开始生成。这样可以吗？
```

用户回复"确认""可以""开始生成""就这样""OK"等同意表达后，再调用图片生成工具。

### 步骤 3：生成图片

#### 3.1 生成 900×383 首图

使用图片生成工具，提示词结构：

```
生成一张微信公众号首图，尺寸为 900 × 383 像素。
主题和文案：【内容摘要】。
视觉风格：公众号【风格名称】，【风格描述】。
画面元素：必须包含品牌字母、【其他元素】。
色彩：【配色描述】。
避免内容：【限制或无】。
确保手机端阅读清晰，关键文字留出安全边距，不要使用过小细节。
```

#### 3.2 生成 383×383 小封面（仅兼顾大小封面需要）

```
生成一张微信公众号小封面裁切区图片，尺寸为 383 × 383 像素。
主题和文案：【短文案或无文字】。
视觉风格必须与左侧大封面统一，为公众号【风格名称】。
画面元素：【核心主体、品牌字母、校徽图形或图标】。
避免内容：【限制或无】。
小封面必须单独成立，不依赖大封面文字；不要放过长文字。
```

#### 3.3 拼接为 1283×383（仅兼顾大小封面需要）

分别生成左右两区后，使用脚本拼接：

```bash
python3 scripts/stitch_compatible_cover.py left.png right.png --output final.png
```

拼接后验证最终尺寸为 `1283 × 383`。

## 提示词模板

### 活泼拼贴风

```
A vibrant WeChat official account cover, 900x383 px. 
Theme: 【主题】. 
Style: colorful collage with rainbow spiral background, cute stickers, meme doge faces, bubble tea, watermelon, books, playful elements. 
Big bold decorative text or brand letters somewhere prominent. 
Bright saturated colors, fun and youthful campus vibe. 
Clean composition, mobile-friendly text layout.
```

### 手绘插画风

```
A hand-drawn illustration style WeChat cover, 900x383 px. 
Theme: 【主题】. 
Style: cute chibi students, speech bubbles, warm orange background, doodle rainbows, friendly campus atmosphere. 
Decorative brand letters integrated into illustration. 
Soft but readable, mobile-friendly.
```

### 实景新闻风

```
A cinematic campus photo WeChat cover, 900x383 px. 
Theme: 【主题】. 
Style: real campus building or lake view at dusk, with a bold red transparent overlay strip across the middle. 
Large white Chinese headline "【标题】". 
Subtle brand watermark. 
Official news style, high contrast, authoritative.
```

### 清新扁平插画风

```
A flat vector illustration WeChat cover, 900x383 px. 
Theme: 【主题】. 
Style: clean flat campus buildings by the lake, soft pastel gradient sky, reflection in water, trees and bridge. 
Outline brand letters in light color. 
Minimal, fresh, modern campus aesthetic.
```

### 城市旅行拼贴风

```
A travel collage WeChat cover, 900x383 px. 
Theme: 【主题】. 
Style: blue sky with sun rays, high-speed train, city landmarks, ancient and modern buildings, sticker cutout white borders. 
Colorful hand-lettered brand text. 
Energetic holiday vibe.
```

## 常见错误

- 不要将"封面"默认理解为 `900 × 383` 首图；优先建议兼顾大小封面 `1283 × 383`。
- 不要直接生成 `1283 × 383` 整图；必须先生成 `900 × 383` 和 `383 × 383` 两张分区图，再拼接。
- 小封面裁切区不要放过长文字，必须能独立成立。
- 关键标题不要跨越左右区域边界。
- 不要在用户确认前调用图片生成工具。
- 不要混淆"小封面（383×383）"和"次图（200×200）"。

## 资源

- `references/style-guide.md`：公众号封面详细风格指南，含配色、字体、构图、五种风格变体。
- `scripts/stitch_compatible_cover.py`：将 900×383 大封面与 383×383 小封面拼接为 1283×383 兼顾大小封面。
