# Anime Editorial Poster Skill

Reference-driven anime editorial poster skill.

当前版本：**v2.0.0**

## 文件结构

```text
anime-editorial-poster/
├─ SKILL.md        # Skill 主文件，安装时使用
├─ README.md       # 使用与 GitHub 更新说明
├─ CHANGELOG.md    # 版本更新记录
├─ VERSION         # 当前版本号
└─ .gitignore
```

## 安装

### 方式 A：直接安装 SKILL.md

使用仓库根目录中的 `SKILL.md` 作为 Skill 文件。

如果你的 Skill 管理界面支持上传文件：
1. 下载 `SKILL.md`
2. 进入 Skill 安装 / 管理界面
3. 上传 `SKILL.md`
4. Skill 名称应识别为 `anime-editorial-poster`

### 方式 B：从 GitHub 管理

建议 GitHub 仓库名：

```text
anime-editorial-poster
```

仓库根目录必须保留：

```text
SKILL.md
```

这样后续只需要更新该文件即可保持 Skill 本体同步。

## 调用示例

```text
使用 anime-editorial-poster-skill。

图一：版式参考
图二：服装参考
图三：角色参考
姿势：按照图一版式自动设计
文字：结合角色故事背景自动生成
要求：角色必须融入图一的版式设计语言，不是简单换角色
比例：3:4
```

## GitHub 首次发布

在本地创建仓库后：

```bash
git init
git add .
git commit -m "feat: release anime-editorial-poster v2.0.0"
git branch -M main
git remote add origin <你的GitHub仓库地址>
git push -u origin main
```

建议同时创建版本标签：

```bash
git tag -a v2.0.0 -m "anime-editorial-poster v2.0.0"
git push origin v2.0.0
```

## 后续更新 Skill

例如升级到 v2.1.0：

1. 修改 `SKILL.md`
2. 把 frontmatter 中的 `version` 改为 `2.1.0`
3. 把 `VERSION` 改为 `2.1.0`
4. 在 `CHANGELOG.md` 顶部增加 v2.1.0 更新说明
5. 提交并推送：

```bash
git add SKILL.md VERSION CHANGELOG.md README.md
git commit -m "feat: update anime-editorial-poster to v2.1.0"
git push
```

6. 发布版本标签：

```bash
git tag -a v2.1.0 -m "anime-editorial-poster v2.1.0"
git push origin v2.1.0
```

## 推荐版本规则

采用 Semantic Versioning：

```text
MAJOR.MINOR.PATCH
```

- `2.0.1`：修正文案、负面词、轻微规则
- `2.1.0`：增加新的版式分析、角色处理、输出能力
- `3.0.0`：改变核心工作流或参考图职责体系

## 更新原则

每次更新尽量只修改真正需要变化的规则，不要无理由重写整个 Skill。

重点检查：

- Character Reference 是否仍只负责角色
- Outfit Reference 是否仍只负责服装
- Pose Reference 是否出现身份串味
- Layout Reference 是否保持最高视觉系统权重
- 用户当前明确要求是否仍高于默认规则
- 默认白底 / Didone / 低饱和是否只作为 fallback
- Character × Layout Integration 是否仍是核心能力
