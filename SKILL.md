---
name: anime-editorial-poster
version: 2.0.0
description: Reference-driven anime editorial poster generator. 将角色、服装、姿势、版式、色彩、光影与角色故事文案拆分为独立参考职责，并以版式参考图的视觉系统为核心进行重组。适用于动漫角色时尚海报、角色特刊、服装替换、姿势设计、多参考图融合和系列视觉延展。无版式参考时回退到高级日系 Editorial 默认系统。
---

# Reference-Driven Anime Editorial Poster Skill v2.0.0

## 1. 核心目标

将用户提供的多张参考图拆分为不同职责，再重新编译成一张完整、统一、具有设计逻辑的动漫 Editorial 海报。

本 Skill 不再以“固定白底 + Didone + 硬投影”作为唯一风格，而是：

> **先读取版式参考的设计语言，再让角色、服装、姿势、文案、字体、光影和装饰共同适配该设计系统。**

目标不是简单的：

> “角色立绘 + 模仿几处文字”

而是：

> **角色本身成为版式系统的一部分。**

角色的姿势、轮廓、裁切、视线、服装形状、头发走势、文字层级、装饰线条、图形与留白都应发生关系。

---

## 2. 适用场景

适合：

- 动漫角色 Editorial 海报
- 动漫角色杂志封面
- 角色生日 / 特刊视觉
- 角色主题 KV
- 根据版式参考图重新设计角色海报
- 多参考图分别控制角色 / 服装 / 姿势 / 版式
- 没有姿势图时，根据版式自动设计姿势
- 根据角色故事背景自动生成海报文案
- 同一角色系列视觉延展
- 不同角色共享同一个视觉母版
- 服装替换但保持角色身份
- 参考某张海报的设计语言进行原创重组

不优先用于：

- 复杂群像叙事
- 大型战斗场面
- 高复杂真实环境
- 纯摄影海报
- 电商详情页
- 信息量极大的商业促销海报

---

## 3. 总体工作流程

每次调用必须按以下顺序执行：

1. 解析用户文字要求
2. 识别每张参考图的职责
3. 提取角色身份特征
4. 提取服装结构
5. 提取姿势；若无姿势参考，则进入“版式驱动姿势设计”
6. 深度解析版式参考
7. 判断视觉风格类别
8. 生成角色故事 / 性格相关文案
9. 重新设计人物与版式的融合关系
10. 编译最终生成指令
11. 生成前进行冲突检查
12. 生成后进行版式与角色一致性检查

禁止直接跳到“写 Prompt”。

---

# 4. Reference Responsibility System

## 4.1 参考图职责必须拆分

推荐职责：

### A. Character Reference
只负责：

- 角色身份
- 脸部识别
- 发型
- 发色
- 瞳色
- 固有配饰
- 固有身体特征
- 角色基础气质

不得继承：

- 原图服装（除非用户指定）
- 原图姿势（除非用户指定）
- 原图背景
- 原图版式
- 原图光影

---

### B. Outfit Reference
只负责：

- 服装类别
- 版型
- 材质
- 领口
- 袖型
- 肩带
- 腰线
- 裙摆 / 裤型
- 配饰
- 鞋袜
- 颜色关系
- 局部装饰

不得继承：

- 模特脸部
- 模特发型
- 模特身体身份
- 模特表情
- 原背景

---

### C. Pose Reference
只负责：

- 身体动作
- 肢体关系
- 重心
- 头部角度
- 手部位置
- 镜头角度
- 裁切方式
- 人物占比

不得继承：

- 参考人物身份
- 服装
- 发型
- 表情（除非用户指定）
- 色彩

---

### D. Layout / Editorial Reference
负责整个视觉系统：

- 人物与文字的相对位置
- 主视觉重心
- 人物大小
- 裁切方式
- 留白比例
- 字体类别
- 字号层级
- 字距
- 行距
- 文字方向
- 标题位置
- 编号位置
- 图形装饰
- 色块
- 线条
- 边框
- 图像叠压方式
- 背景结构
- 光影语言
- 视觉密度
- 对称 / 非对称关系
- 视觉动线

**版式参考不只是“字体参考”。**

它是整张海报的视觉母系统。

---

### E. Lighting / Color Reference
若单独提供，负责：

- 主色
- 辅色
- 明度
- 饱和度
- 色温
- 光源方向
- 投影形态
- 反差
- 质感

---

## 4.2 严格禁止参考串味

必须避免：

- 姿势参考人物的脸进入角色
- 服装参考模特的发型进入角色
- 版式参考中的人物身份覆盖角色
- 角色参考中的原服装覆盖用户指定服装
- 参考图中的背景被错误继承
- 一张参考图同时默认承担角色、服装、姿势和版式职责

原则：

> 每张参考图只继承用户赋予它的功能。

---

# 5. Conflict Priority

出现冲突时，优先级如下：

1. 用户当前明确文字要求
2. 用户明确指定的参考图职责
3. 角色身份锁定
4. 服装结构锁定
5. 姿势要求
6. 版式参考的设计系统
7. 角色故事与性格适配
8. 本 Skill 的默认 Editorial 规则
9. 默认值

示例：

- 用户要求“图三是角色” → 图三只负责角色身份。
- 用户要求“图二为服装” → 不能继承角色原服装。
- 用户要求“姿势按照版式设计” → 不需要额外姿势参考，应根据版式空间自动设计。
- 用户要求“角色融入版式设计风格” → 人物不能只是贴在排版上，必须重构轮廓与版式关系。
- 用户要求“文字结合角色故事背景” → 不得只写 GENERIC FASHION / BEAUTY / DREAM 等空泛词。

---

# 6. Layout Analysis Engine

当存在版式参考时，必须先分析以下项目。

## 6.1 Composition Skeleton

识别：

- 主体位于左 / 中 / 右
- 主体是否居中
- 主体是否倾斜
- 人物占画面比例
- 人物头部位置
- 躯干轴线
- 视觉重心
- 主标题位置
- 大字号区域
- 次级文字区域
- 空白区
- 装饰区
- 视觉动线

输出一个抽象骨架，而不是逐元素复制。

---

## 6.2 Typography System

识别：

- Serif / Sans / Grotesk / Condensed / Display / Handwritten / Blackletter / Y2K 等
- 字重
- 字宽
- 大小写
- 是否窄长
- 是否压缩
- 字距
- 行距
- 大标题比例
- 数字比例
- 竖排 / 横排 / 旋转文字
- 是否文字穿插人物
- 是否标题在人物前 / 后
- 是否有超大单字
- 是否有编号系统
- 是否有信息块

禁止固定使用 Didone。

**字体必须跟随版式参考。**

---

## 6.3 Color System

提取：

- 背景主色
- 人物主色
- 文字主色
- 装饰色
- 强调色
- 明度关系
- 饱和度关系

有参考图时：

> 不强制低饱和。

如果参考图是高饱和红黑、复古黄绿、Y2K 银蓝、黑白高反差等，应跟随参考建立同源色彩系统。

---

## 6.4 Graphic Language

识别是否存在：

- 大色块
- 几何形
- 细线
- 网格
- 边框
- 扫描纹理
- 半透明蒙版
- 粗颗粒
- 印刷错位
- 拼贴
- 撕纸
- 图章
- 编号
- 信息标签
- 大投影
- 装饰符号
- 图像遮罩

只有参考图存在时才继承。

不得为了“高级感”自动加不存在的元素。

---

## 6.5 Visual Density

将版式划分为：

- Low Density：极简、高留白
- Medium Density：杂志 Editorial
- High Density：拼贴 / Y2K / 视觉实验

最终输出必须接近参考图的信息密度。

---

# 7. Reference-Driven Style Classification

根据版式参考自动判断主要类别，例如：

- Minimal Fashion Editorial
- Japanese Magazine
- Neo-Retro
- Y2K Editorial
- Punk / Grunge
- Luxury Fashion
- Swiss / Grid
- Experimental Typography
- Gothic Editorial
- Pop Graphic
- Monochrome Editorial
- Collage Poster
- Art Book Cover
- Music Editorial

分类只是帮助理解，不应强行覆盖参考图本身。

---

# 8. Character Identity Lock

角色参考必须优先保持：

- 脸型
- 五官比例
- 发型轮廓
- 发色
- 瞳色
- 固有发饰
- 固有标志物

若角色属于已有动漫 / 游戏作品：

- 不擅自改变角色身份
- 不因为服装参考而换脸
- 不因为版式参考而修改角色种族 / 年龄感 / 发型
- 可以在保持身份的前提下做时装化绘制

如果用户要求“保持原作感”：

> 角色识别度 > Editorial 风格化。

如果用户要求“更时尚、更成熟”：

> 可以调整绘制语言和姿态，但不得失去角色识别。

---

# 9. Outfit Transfer System

服装参考需要先拆解再移植。

必须读取：

- silhouette
- neckline
- shoulder structure
- sleeve
- waist
- hem
- fabric
- transparency
- pattern
- accessories
- footwear
- jewelry
- layering
- key construction details

重点：

> 复制的是“服装结构”，不是“模特本人”。

当服装与角色发型 / 身体结构冲突时：

- 优先保持角色身份
- 再合理适配服装结构
- 不得无故删掉服装关键设计

---

# 10. Layout-Driven Pose Design

当用户没有姿势参考，或明确要求：

> “姿势按照版式设计”

必须根据版式自动设计人物姿势。

## 10.1 姿势设计依据

读取版式中的：

- 空白位置
- 标题位置
- 主视觉方向
- 文字轴线
- 大色块轮廓
- 画面重心
- 人物预留区域
- 裁切边界

---

## 10.2 姿势目标

人物轮廓应：

- 顺着版式视觉动线
- 为主标题让出空间
- 与大字号形成遮挡关系
- 用头发 / 手臂 / 腿部建立视觉连线
- 避免压住关键文字
- 避免普通站桩
- 避免为了露全身而把人物缩小

---

## 10.3 常用策略

### Vertical Layout
适合：

- 站姿
- 侧身
- 拉长躯干
- 一手抬起
- S 型身体轴

### Horizontal Typography
适合：

- 坐姿
- 半蹲
- 俯身
- 横向手臂
- 头部穿入标题区域

### Diagonal Composition
适合：

- 侧倚
- 扭腰
- 单膝抬高
- 斜向身体轴

### Large Empty Corner
可让：

- 视线朝向空白
- 手势指向空白
- 头发走势导向空白

让空白成为版式的一部分。

---

# 11. Character-Driven Copywriting Engine

当用户要求：

> “文字结合角色故事背景生成”

必须先提炼角色信息，再写文案。

## 11.1 信息来源优先级

1. 用户明确提供的角色设定
2. 已知且可靠的角色背景
3. 角色性格、身份、矛盾、舞台关系
4. 无法确认剧情事实时，使用不伪造事实的抽象文案

禁止：

- 编造官方台词
- 把不存在的剧情当成事实
- 写与角色无关的泛化时尚句
- 所有角色都使用 FREEDOM / DREAM / NIGHT / BEAUTY 等模板词

---

## 11.2 文案层级

每张海报可生成：

### Level 1 — Main Title
1–4 个词。

用于视觉识别。

可以来自：

- 角色名
- 角色姓氏
- 代号
- 与角色核心矛盾相关的概念

---

### Level 2 — Character Statement
约 3–10 个英文词，或一句极短中文。

表达：

- 性格
- 选择
- 矛盾
- 舞台状态
- 角色变化

---

### Level 3 — Editorial Microcopy
用于边角小字：

- Issue
- Archive
- Character File
- Stage Note
- Chapter
- Profile
- Date
- Number
- Fictional editorial metadata

---

### Level 4 — Decorative Copy
只服务排版。

必须短。

可使用：

- 罗马字
- 英文
- 日文角色名
- 编号
- 日期
- 单词碎片

---

## 11.3 文案风格必须跟随版式

极简版式：

- 文案少
- 主标题强
- 小字极少

高密度版式：

- 可以增加编号、栏目、短句、标签

朋克 / 拼贴：

- 可以断句
- 大小写混合
- 碎片化短句

高级时尚：

- 冷静、简洁、克制

---

# 12. Character × Layout Integration

这是 v2.0 的核心。

禁止：

> “先画完整人物，再把字贴上去”。

必须设计以下关系：

## 12.1 Occlusion

可以让：

- 标题在人物后
- 部分字被头发遮挡
- 数字穿过人物边缘
- 小字贴近轮廓

但：

- 不遮住眼睛
- 不遮住关键五官
- 不造成阅读崩坏

---

## 12.2 Silhouette Matching

人物轮廓应与版式发生对应。

例如：

- 圆形构图 → 身体或头发形成圆弧
- 斜线版式 → 人物轴线呼应斜线
- 左重右空 → 人物集中左侧
- 中心大字 → 人物前后穿插标题

---

## 12.3 Hair as Graphic Element

头发可以作为：

- 引导线
- 大面积色块边缘
- 文字遮挡层
- 视觉框架

但不能为了版式改变角色核心发型。

---

## 12.4 Clothing as Graphic Element

服装可与：

- 色块
- 标题
- 背景
- 装饰线
- 几何图形

建立同色或反差关系。

---

# 13. Default Editorial System

只有在以下情况才使用默认系统：

- 用户没有提供版式参考
- 用户只提供角色
- 用户只要求“高级动漫时尚杂志海报”

默认：

- refined Japanese anime illustration
- semi-cel + restrained painterly rendering
- large subject
- 75%–90% frame occupancy
- clean editorial composition
- neutral / off-white background
- strong serif or modern editorial typography
- restrained graphic shadow
- limited palette
- asymmetric fashion layout

注意：

> 这些是 fallback，不是强制 Style DNA。

---

# 14. Prompt Compiler v2

最终 Prompt 应按以下顺序组织。

## Segment 1 — Reference Mapping

明确：

- Reference A = Character only
- Reference B = Outfit only
- Reference C = Pose only
- Reference D = Layout / Editorial system
- Reference E = Color / Lighting only

并写明各自“不继承什么”。

---

## Segment 2 — Character Lock

包括：

- 角色名
- 身份
- 发型
- 发色
- 瞳色
- 配饰
- 气质
- identity lock

---

## Segment 3 — Outfit Transfer

包括：

- 版型
- 材质
- 颜色
- 结构
- 配饰
- 必须保留局部

---

## Segment 4 — Layout Extraction

描述：

- 主体位置
- 人物比例
- 裁切
- 标题区域
- 数字区域
- 文字密度
- 图形语言
- 背景
- 色彩
- 光影

---

## Segment 5 — Pose

若有姿势参考：

> 继承姿势参考。

若没有：

> 根据 Segment 4 的版式自动设计。

---

## Segment 6 — Character / Layout Integration

必须写出：

- 人物如何穿插标题
- 哪些部位遮挡文字
- 哪些留白必须保留
- 头发 / 手 / 腿如何配合视觉动线
- 人物轮廓如何适配图形

---

## Segment 7 — Typography

不再固定 Didone。

必须跟随版式参考描述：

- 字体类别
- 字重
- 字宽
- 字距
- 标题比例
- 编号
- 信息层级
- 排列方向

---

## Segment 8 — Copy

加入：

- Main Title
- Character Statement
- Microcopy
- Issue / Number

要求：

- 与角色故事相关
- 不伪造官方台词

---

## Segment 9 — Lighting / Color

优先继承参考。

无参考再使用默认 Editorial 光影。

---

## Segment 10 — Constraints

明确：

- identity lock
- outfit lock
- layout hierarchy lock
- no reference contamination
- readable typography zones
- correct anatomy
- no random text
- no unnecessary background elements

---

# 15. Generic Prompt Skeleton

```text
Create a reference-driven anime editorial poster.

REFERENCE ROLE MAPPING:
[CHARACTER_REF] = character identity only. Preserve face, hairstyle, hair color, eye color, signature accessories and recognizable character traits. Do not inherit outfit, pose, background or layout unless explicitly requested.

[OUTFIT_REF] = outfit only. Transfer clothing silhouette, fabric, construction, neckline, sleeve structure, waist, hem, accessories and styling. Do not inherit the model's face, hairstyle, body identity, pose or background.

[POSE_REF] = pose only, if provided. Transfer body gesture, limb placement, center of gravity, head angle, camera angle and crop only. Do not inherit identity, outfit or expression unless explicitly requested.

[LAYOUT_REF] = complete editorial layout system. Analyze and inherit the composition skeleton, figure scale, crop logic, negative space, typography family, font proportion, title scale, number placement, text direction, graphic shapes, color relationships, lighting language, visual density and image-text overlap.

MAIN CHARACTER:
[CHARACTER_DESCRIPTION]
Strict character identity lock.

OUTFIT:
[OUTFIT_DESCRIPTION]
Strict outfit structure lock while adapting naturally to the character.

POSE:
[POSE_DESCRIPTION]
If no pose reference is provided, design the pose from the layout: use the body silhouette, head direction, arm placement, hair flow and crop to support the layout's visual movement and preserve key negative space.

LAYOUT:
Reconstruct the design language of [LAYOUT_REF] without treating the character as a pasted standalone illustration.
The character must become part of the graphic composition.
Match the reference's hierarchy, visual density, asymmetry, title-to-character scale, spacing rhythm, foreground/background text overlap, graphic geometry and overall design tension.

CHARACTER × TYPOGRAPHY INTEGRATION:
Use intentional overlap between character silhouette and typography.
Allow hair, shoulders, arms or clothing edges to partially cover selected letters where compositionally appropriate.
Never obscure the eyes or essential facial features.
Use the character silhouette to reinforce the reference layout's directional flow.

TYPOGRAPHY:
[TYPOGRAPHY_SYSTEM]
Do not force Didone or serif typography unless the reference uses it.
Match the reference's font category, width, weight, spacing, hierarchy and directional arrangement.

COPY:
Main title: [MAIN_TITLE]
Character statement: [CHARACTER_STATEMENT]
Microcopy: [MICROCOPY]
Issue / number: [ISSUE]

Copy must connect to the character's personality, narrative tension, role or story background.
Do not fabricate official dialogue.
Avoid generic fashion filler words when character-specific language is possible.

COLOR & LIGHT:
[COLOR_LIGHT_SYSTEM]
Follow the reference layout's palette and contrast.
Do not automatically force a white background, muted palette or hard cast shadow unless those qualities exist in the layout reference.

RENDERING:
Refined Japanese anime illustration with clean controlled linework and polished rendering.
Preserve recognizable character identity.
Rendering style should harmonize with the layout reference rather than overpower it.

FINAL GOAL:
The result must feel like one intentionally art-directed editorial poster.
Not a character illustration with typography added afterward.
Character, pose, typography, graphics, negative space, color and lighting must belong to the same visual system.

Aspect ratio: [ASPECT_RATIO].
```

---

# 16. Negative / Anti-Failure Rules

默认避免：

```text
reference contamination,
wrong character identity,
outfit inherited from wrong reference,
pose reference face contamination,
layout reference character contamination,
generic standing pose,
tiny character,
character pasted on top of layout,
typography added as an afterthought,
random serif font,
forced Didone typography,
forced white background,
forced low saturation,
forced hard shadow,
unrelated generic fashion words,
fake official quotes,
unreadable random text,
excessive decorative text,
busy composition when reference is minimal,
empty composition when reference is dense,
wrong visual hierarchy,
important text covering eyes,
face covered by typography,
deformed hands,
extra fingers,
fused fingers,
broken wrists,
duplicated limbs,
bad anatomy,
distorted facial features,
incorrect hairstyle,
incorrect eye color,
random accessories,
watermark,
random logo
```

注意：

不能把“高饱和”“复杂背景”“无衬线字体”“软光”等本身列为负面词，因为它们可能正是版式参考的核心视觉。

---

# 17. Typography Reality Check

AI 图像模型对精确文字可能不稳定。

因此区分两个模式：

## Concept Mode
优先保证：

- 字体气质
- 字号层级
- 文字位置
- 遮挡关系
- 信息密度
- 版式结构

允许个别小字不完全准确。

## Production Mode
若用户要求商业级准确文字：

建议工作流：

1. 先生成完整人物 + 版式视觉底稿
2. 保留明确文字区域
3. 再在设计软件中完成准确文字排版

---

# 18. Auto-Correction Rules

## Problem: 人物像贴上去

追加：

`character silhouette must structurally interact with typography and graphic layout, intentional image-text overlap, pose designed from negative space, integrated editorial composition`

---

## Problem: 版式参考不明显

追加：

`strongly preserve the layout reference's hierarchy, figure placement, title scale, visual density, spacing rhythm, graphic geometry and negative-space proportions`

---

## Problem: 又变成白底 Didone

追加：

`do not default to white background or Didone typography; derive background, typography, color and lighting directly from the layout reference`

---

## Problem: 人物太小

追加：

`increase character scale while preserving the reference layout hierarchy; character must remain a dominant compositional element`

---

## Problem: 姿势普通

追加：

`redesign pose according to the layout's directional flow, typography zones and negative-space structure; avoid generic upright standing pose`

---

## Problem: 文案太泛

重新生成：

- 提取角色核心性格
- 提取故事矛盾
- 提取舞台 / 身份 / 关系
- 生成 1 个概念标题
- 1 句角色陈述
- 2–4 个短小编辑信息

---

## Problem: 参考串味

重新声明：

`inherit only the assigned reference role; explicitly reject identity, outfit, pose, expression, background and palette from references that are not responsible for those attributes`

---

# 19. Quality Assurance Checklist

## A. Reference Mapping
- [ ] 每张参考图职责是否明确
- [ ] 是否存在参考串味
- [ ] 用户当前文字要求是否最高优先级

## B. Character
- [ ] 角色脸型正确
- [ ] 发型正确
- [ ] 发色正确
- [ ] 瞳色正确
- [ ] 固有配饰正确
- [ ] 角色仍可识别

## C. Outfit
- [ ] 服装版型正确
- [ ] 领口 / 肩带 / 袖型正确
- [ ] 腰线正确
- [ ] 材质逻辑正确
- [ ] 关键配饰未丢失

## D. Pose
- [ ] 姿势是否服务版式
- [ ] 是否避免站桩
- [ ] 肢体是否自然
- [ ] 手部是否正确
- [ ] 裁切是否合理

## E. Layout
- [ ] 主视觉位置是否接近参考逻辑
- [ ] 主标题比例是否正确
- [ ] 留白比例是否正确
- [ ] 视觉密度是否一致
- [ ] 大小层级是否清楚
- [ ] 图形语言是否同源

## F. Typography
- [ ] 字体类别是否跟随参考
- [ ] 是否错误强制 Serif / Didone
- [ ] 主标题够不够强
- [ ] 次级文字有没有抢主体
- [ ] 是否出现无意义乱码堆积

## G. Color
- [ ] 是否读取参考配色
- [ ] 是否错误强制低饱和
- [ ] 色彩关系是否统一
- [ ] 人物是否融入整体色系

## H. Integration
- [ ] 人物和文字是否真正发生遮挡关系
- [ ] 人物轮廓是否参与构图
- [ ] 角色是不是看起来“贴上去”
- [ ] 去掉任何单独一层后，设计是否仍有逻辑

---

# 20. Output Format

调用本 Skill 后，默认输出：

### A. Reference Mapping
简洁说明每张图负责什么。

### B. Layout Analysis
用短句概括：

- 构图
- 人物位置
- 字体
- 色彩
- 图形
- 视觉密度

### C. Character Copy
自动给出：

- Main Title
- Character Statement
- Microcopy
- Issue / Number

### D. Final Generation Prompt
输出可直接用于生图的完整 Prompt。

### E. Locked Constraints
列出：

- 角色锁定
- 服装锁定
- 版式锁定
- 不继承项

如果用户直接说：

> “使用 anime-editorial-poster-skill 生成图片”

则可以完成内部分析后直接进入生成，不必把所有中间分析都展示给用户。

---

# 21. Recommended Invocation Pattern

示例：

```text
使用 anime-editorial-poster-skill。

图一：版式参考
图二：服装参考
图三：角色参考，角色为安和昴
姿势：按照图一版式自动设计
文字：结合角色故事背景自动生成
要求：角色必须融入图一的版式设计语言，不是简单换角色
比例：3:4
```

内部映射：

```text
REF 1 = Layout
REF 2 = Outfit
REF 3 = Character
POSE = Layout-driven auto pose
COPY = Character-driven
```

最终目标：

> 保持角色身份 + 精确移植服装 + 根据版式重新设计姿势 + 继承版式的完整视觉系统 + 自动生成角色专属 Editorial 文案。

---

# 22. One-Line Style Definition

**Reference-driven anime editorial art direction × strict multi-reference role separation × character identity lock × layout-designed pose × character-specific narrative typography × integrated image-text composition.**

---

# 23. v2.0 与 v1.0 的关键区别

| v1.0 | v2.0 |
|---|---|
| 固定白 / 暖白背景 | 背景跟随版式参考 |
| 固定 Didone / Bodoni | 字体类别跟随版式参考 |
| 固定低饱和 | 色彩跟随版式参考 |
| 固定硬投影 | 光影跟随版式参考 |
| 偏固定高级杂志模板 | 参考图驱动 |
| 姿势主要来自用户 / 姿势图 | 可根据版式自动设计姿势 |
| 文案偏抽象词 | 结合角色故事背景生成 |
| 版式主要是文字位置参考 | 版式成为完整视觉母系统 |
| 人物 + 字体叠加 | 人物主动参与版式结构 |
| 默认统一风格 | 可适配多种 Editorial 风格 |
