# Changelog

所有重要更新记录在此文件。

## [2.0.0] - 2026-08-31

### Added
- Reference Responsibility System：角色 / 服装 / 姿势 / 版式 / 光影职责拆分。
- Layout Analysis Engine：构图、字体、色彩、图形语言、视觉密度分析。
- Layout-Driven Pose Design：无姿势参考时根据版式自动设计动作。
- Character-Driven Copywriting Engine：根据角色故事、性格和冲突生成文案。
- Character × Layout Integration：人物轮廓、头发、服装、文字与图形主动穿插。
- Reference contamination 防串味规则。
- 完整 Quality Assurance Checklist。
- 自动纠错规则。

### Changed
- 版式参考由“辅助参考”升级为完整视觉母系统。
- 固定白 / 暖白背景改为无参考时 fallback。
- 固定 Didone / Bodoni 字体改为无参考时 fallback。
- 固定低饱和色彩改为跟随版式参考。
- 固定硬投影改为跟随版式参考光影系统。
- 文案从泛化时尚词升级为角色专属 Editorial 文案。

### Removed
- 不再强制所有作品使用统一白底高级杂志视觉。
- 不再默认所有角色使用相同 Editorial 文字模板。
