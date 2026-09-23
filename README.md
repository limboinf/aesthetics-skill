# master-aesthetics

把任意题材转译成电影大师的视觉美学，产出可以直接交给生图模型的中文画面描述，并给出出图参数建议。

**只写描述，不负责生图。** 生图交给你自己的工具（apimart-image-gen / baoyu-image-gen / MiniMax / 即梦 / nano banana 等）。

## 安装

用 [skills CLI](https://github.com/vercel-labs/skills)（支持 Claude Code、Codex、Cursor 等主流 agent）：

```bash
npx skills add limboinf/aesthetics-skill
```

只装给 Claude Code，装到用户级目录，跳过确认：

```bash
npx skills add limboinf/aesthetics-skill --skill master-aesthetics -g -a claude-code -y
```

先看看仓库里有哪些 skill：

```bash
npx skills add limboinf/aesthetics-skill --list
```

手动安装：把 `skills/master-aesthetics/` 复制或软链到 `~/.claude/skills/`（用户级）或 `.claude/skills/`（项目级）。

## 四种用法

| 场景 | 说法示例 | 流程 |
|---|---|---|
| 纯生成 | "给我一张胡金铨风格的竹林对峙" | A |
| 风格重构 | "把这张风景照按胡金铨的美学重做" | B |
| 人物融入 | "把我放进胡金铨的武侠世界里" | C |
| **真人照片重拍** | "把孩子们这张合影拍成胡金铨的电影剧照" | **D** |

**D 流程的第一原则是：人物要像本人。** 脸、姿态、人数都锁住，只允许为了美学改取景（拉宽画面、重新构图、加前景）、服装、场景和光色。另外有三条硬规则：参考图只放原照；人像用高质量档出图；每次都从原照重新生成，不在生成图上接着改。

## 已收录

- `king-hu` 胡金铨：武侠、禅意、山水手卷、竹林、客栈、明代考据、京剧身段、留白

## 结构

```
skills/master-aesthetics/
├── SKILL.md                    # 入口：大师索引 + 工作流路由 + 五条铁律
├── references/
│   ├── prompt-grammar.md       # 七段式描述语法（A/B/C 共用）
│   ├── workflow-generate.md    # A 纯生成
│   ├── workflow-restyle.md     # B 风格重构
│   ├── workflow-portrait.md    # C 人物融入
│   ├── workflow-reshoot.md     # D 真人照片重拍（四块提示词结构）
│   └── adding-a-master.md      # 扩展指南
└── masters/
    ├── _TEMPLATE/              # 加新大师照抄这个
    └── king-hu/
        ├── profile.md          # 风格档案（含禁忌清单）
        ├── shots.md            # 七式镜头范式 + 现成模板
        ├── prompt-kit.md       # 词库 + 负向词 + 完整范例
        └── gallery/            # 参考图 + 索引
samples/                        # 实跑记录：每轮踩的坑和对应写回 skill 的改动
```

## 加新大师

读 `skills/master-aesthetics/references/adding-a-master.md`。只需两步：照抄 `_TEMPLATE` 建一个新目录，再在 `SKILL.md` 的索引表里加一行。主流程不用改。
