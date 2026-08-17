---
name: city-photo-editorial-poster
description: 将城市照片转为上下分区诗意编辑海报。
version: 0.1.0
author: User, Hermes Agent
license: MIT
platforms: [linux, macos, windows]
metadata:
  hermes:
    tags: [image-editing, cityscape, poster, editorial, photography]
    related_skills: []
---

# 城市照片上下分区编辑海报

将用户提供的真实城市或风景照片，转换为 2:3 竖版、上下分区的高级艺术海报。上半部分必须保留照片的真实感与原始构图；下半部分必须是对上半部分视觉元素的抽象绘画式提炼，而非第二张独立风景图。

## When to Use

- 用户要求把真实城市、建筑、旅行或风景照片制作成高级艺术书/杂志内页风格海报。
- 用户强调“上方保留摄影、下方转为插画”“安静、克制、诗意、留白”。
- 不适用于需要商业促销感、密集信息排版、赛博朋克或逐像素照片临摹的设计。

## Prerequisites

- 必须有用户提供的原始照片路径或 URL。没有照片时，请用户上传，不要凭空声称保留原始构图。
- 使用 `vision_analyze` 识别照片中的地标、景别、天际线、云、月亮、灯光及主色，再使用 `image_generate` 的 `image_url` 进行图生图编辑。
- 默认比例：`portrait`（16:9 竖幅）。若工具支持精确 2:3，应优先使用 2:3；当前 `image_generate` 仅支持 portrait，需在提示词中明确 `vertical 2:3 poster composition`。

## Procedure

1. **分析原图**
   - 用 `vision_analyze` 提取不可丢失的主体、构图关系、色彩、天气与时间氛围。
   - 完成标准：写出一条简短的“必须保留元素”清单；不要把不确定的地标名称写进生成提示词。

2. **构建编辑提示词**
   - 将图片作为 `image_url` 传给 `image_generate`，明确它是上半部的摄影锚点。
   - 明确要求：上半部分保持原照片的建筑、天空、云层、月亮、灯光与构图，只做低饱和、轻微电影感调色；禁止 HDR、强锐化、AI 重绘感。
   - 明确要求：下半部分从同一照片提炼可识别元素——建筑为柔和几何色块，远景为细小矩形剪影，云为横向干刷笔触，月亮为小新月，灯光仅用少许暖黄点缀。
   - 明确版式：底部左对齐的英文字标，包含根据实际图像内容生成的主标题与斜体副标题；主标题为经典衬线、深蓝灰，副标题为细腻 editorial italic，文字克制且留足呼吸空间。

3. **生成**
   - 调用 `image_generate`，设置 `aspect_ratio="portrait"` 和原图 `image_url`。
   - 使用 `prompts/base-prompt.txt` 作为提示词底稿，并以实际照片主体替换方括号内容。
   - 完成标准：输出为竖版海报，上下两区明确，且下半部能一眼辨认出是在提炼上半部场景。

4. **检查成品**
   - 用 `vision_analyze` 检查：上半部是否仍是现实摄影、下半部是否和上图对应、文字是否为英文且左对齐、是否保留大量米白留白。
   - 若文字乱码或不可读，优先生成无文字版本，再使用合适的排版/图像编辑工具叠加可控文本；不要把乱码版本交付给用户。

## Design Guardrails

- 调色：warm ivory、muted navy、blue grey、smoky grey、warm ochre、mustard yellow、soft beige；整体低饱和。
- 质感：纸张颗粒、哑光印刷、透明水彩与干刷；不使用厚重油画肌理。
- 视觉层级：摄影真实感优先，插画是“提炼”和“回应”，不可喧宾夺主。
- 排版：避免大字号广告口号、居中营销排版、复杂边框、装饰图标。

## Pitfalls

- 图生图模型可能重绘上半部。若真实照片被明显改写，降低风格化描述，重复强调“literal photographic preservation in top half”。
- 生成模型常无法可靠拼写小字号文字。文字准确性是硬要求时，先出无字底图再叠字。
- 不要凭空杜撰地名；从画面无法确认地点时，用氛围型标题，例如 `After the Rain`、`A Quiet Horizon`。
- 不要让下半部分变成扁平矢量插画；必须保留 gouache、dry brush、watercolor opacity 和纸张印刷纹理。

## Verification

交付前逐项确认：

- [ ] 竖版、明确的上下分区构图。
- [ ] 上半部分保留原图的核心构图与真实摄影质感。
- [ ] 下半部分抽象但可辨识地呼应上半部分。
- [ ] 存在温暖米白留白与低饱和蓝灰/暖黄配色。
- [ ] 没有 HDR、赛博朋克、3D、卡通描边或廉价广告感。
- [ ] 英文标题、副标题与实际画面相符；若无法保证文字清晰，采用无字底图并另行排版。
