# City Photo Editorial Poster

将真实城市或风景照片制作成 **上下分区、安静诗意的高级编辑海报** 的 Hermes Agent 技能包。

- **上半部分**：忠实保留原图构图与真实摄影质感，仅做克制的低饱和电影感调色。
- **下半部分**：以水粉、干刷、水彩透明度与纸张纹理，将同一场景抽象为当代艺术书式插画。
- **版式**：竖版 2:3 倾向，温暖米白留白，底部左对齐英文标题与副标题。

## 文件结构

```text
city-photo-editorial-poster/
├── SKILL.md                 # Hermes 技能主体
├── README.md                # 本说明
├── LICENSE                  # MIT 许可
└── prompts/
    └── base-prompt.txt      # 可直接用于图生图的英文提示词模板
```

## 使用方式

### 在 Hermes 中安装

将整个 `city-photo-editorial-poster` 文件夹复制到 Hermes 用户技能目录下的 `creative` 分类中，然后开启一个新会话以刷新技能索引。

Windows 常见位置：

```text
%LOCALAPPDATA%\hermes\skills\creative\city-photo-editorial-poster
```

安装后，向 Hermes 提供一张真实城市或风景照片，并说明希望制作“上下分区高级艺术海报”。技能会要求先识别原照片的不可丢失元素，再进行图生图编辑与成品核验。

### 手动使用提示词

1. 打开 `prompts/base-prompt.txt`。
2. 将 `[landmark/building/skyline]` 替换为从照片中确认的主体；无法确认地名时保持泛称。
3. 将照片作为图生图工具的参考图输入。
4. 选择竖版画幅；若工具支持，优先使用精确 2:3。
5. 若模型生成文字不清晰，请先生成无文字海报底图，再在设计软件中叠加英文字标。

## 视觉原则

| 项目 | 要求 |
|---|---|
| 风格 | Scandinavian minimalism、Japanese editorial design、contemporary art book |
| 色彩 | warm ivory、muted navy、blue grey、smoky grey、warm ochre、mustard yellow |
| 插画材质 | soft gouache、dry brush、watercolor-like opacity、subtle paper grain |
| 禁止项 | HDR、过度锐化、赛博朋克、3D、卡通描边、矢量图标感、广告式大字 |
| 图文关系 | 下方插画应当一眼可看出源自上方照片，但绝不逐像素复刻 |

## 验收标准

- 原图的核心建筑、天空、云、月亮、灯光、空间关系与视角在上方摄影区保留。
- 下方为可辨识的抽象提炼，建筑是柔和几何色块、云是横向笔触、灯光只少量暖黄点缀。
- 画面留白充分、低饱和、安静，有哑光印刷和纸张质感。
- 没有商业广告感与明显 AI 重绘感。

## 许可

本包采用 [MIT License](LICENSE)。
