# master-aesthetics

把任意题材转译成电影大师的视觉美学，产出可以直接交给生图模型的中文画面描述，并给出出图参数建议。

**只写描述，不负责生图。** 生图交给你自己的工具（gpt-image-gen / MiniMax / 即梦 / nano banana 等）。

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

## 六种用法

| 场景 | 说法示例 | 流程 |
|---|---|---|
| 纯生成 | "给我一张胡金铨风格的竹林对峙" | A |
| 风格重构 | "把这张京都竹林的旅行照按胡金铨的美学重做" | B |
| 人物融入 | "把我放进胡金铨的武侠世界里，做成头像" | C |
| **真人照片重拍** | "把孩子们这张合影拍成胡金铨的电影剧照" | **D** |
| 组图 / 分镜 | "出一组四张，讲一个侠客下山的故事" | E（叠加在 A–D 上） |
| 视频镜头 | "让这张图动起来，雾在流、衣带在飘" | F（叠加在 A–D 上） |

**D 流程的第一原则是：人物要像本人。** 脸、姿态、人数都锁住，只允许为了美学改取景（拉宽画面、重新构图、加前景）、服装、场景和光色。另外有三条硬规则：参考图只放原照；人像用高质量档出图；每次都从原照重新生成，不在生成图上接着改。

## 三个风格开关

- **子风格**：胡金铨每部片的世界不一样，按片子选。没指定默认《侠女》。
- **介质**：修复版胶片剧照（默认）、褪色老拷贝、手绘分镜、水墨手卷、手绘电影海报。
- **时代处理**（拿照片或现代题材时）：古装化 / 半转译（保留真实地点）/ 现代保留（只要那个味道）。

## 用途和工具

- **用途**：头像、手机 / 电脑壁纸、海报封面、社媒、横幅头图、产品、旅行照、宠物、情侣、家庭合影、空间情绪板，各自定画幅、主体大小和留白位置。
- **工具**：默认产出中文长句描述（GPT-Image、nano banana、即梦、MiniMax 直接可用），也可改写成 Midjourney、Flux、SD、视频模型的写法。

## 已收录

`king-hu` 胡金铨：武侠、禅意、山水手卷、竹林、客栈、古刹、海岸、边关、志怪、京剧身段、留白

| 子风格 | 参照 | 世界 |
|---|---|---|
| 侠女 · 竹林禅光（默认） | 《侠女》 | 竹林、雾、废墟、逆光僧人 |
| 龙门 · 边关硬光 | 《龙门客栈》 | 烈日荒原、孤客栈、黑衣番子 |
| 大醉侠 · 戏台客栈 | 《大醉侠》 | 棚景、戏曲亮相、色彩最艳 |
| 迎春阁 · 客栈谍影 | 《迎春阁之风波》 | 元末、室内群戏、楼上楼下 |
| 忠烈图 · 海岸阵战 | 《忠烈图》 | 礁石海岸、阵法 |
| 空山灵雨 · 古刹迷宫 | 《空山灵雨》 | 寺院回廊、最素的禅意 |
| 山中传奇 · 手卷幽玄 | 《山中传奇》 | 宋、秋山行旅、志怪 |

## 结构

```
skills/master-aesthetics/
├── SKILL.md                    # 入口：大师索引 + 三个路由 + 三个开关 + 五条铁律
├── references/
│   ├── prompt-grammar.md       # 七段式描述语法（A/B/C 及 E/F 的静帧共用）
│   ├── workflow-generate.md    # A 纯生成
│   ├── workflow-restyle.md     # B 风格重构
│   ├── workflow-portrait.md    # C 人物融入
│   ├── workflow-reshoot.md     # D 真人照片重拍（四块提示词结构）
│   ├── workflow-series.md      # E 组图 / 分镜
│   ├── workflow-video.md       # F 视频镜头
│   ├── use-cases.md            # 用途适配（头像、壁纸、海报、产品……）
│   ├── model-adapters.md       # 下游工具改写（MJ、Flux、SD、视频模型）
│   └── adding-a-master.md      # 扩展指南
└── masters/
    ├── _TEMPLATE/              # 加新大师照抄这个
    └── king-hu/
        ├── profile.md          # 共用底子：意境路由三张表、时刻天气、时代处理、禁忌
        ├── variants.md         # 七种子风格 + 五种介质
        ├── shots.md            # 十一式镜头范式（按人数选式）
        ├── prompt-kit.md       # 词库 + 负向词 + 英文对照
        └── motion.md           # 运动语法（视频用）
```

## 加新大师

读 `skills/master-aesthetics/references/adding-a-master.md`。只需两步：照抄 `_TEMPLATE` 建一个新目录，再在 `SKILL.md` 的索引表里加一行。主流程不用改。
