# Ian Xiaohei Illustrations

> 把中文文章里的判断、流程、状态和隐喻，变成一张张白底、手绘、怪诞但清爽的正文配图。
>
> 16:9 横版 | 小黑 IP | 纯白手绘 | 少量红橙蓝中文批注 | Codex Skill

---

## 这个仓库是什么

Ian Xiaohei Illustrations 是一个 Codex Skill，用来指导 AI Agent 为中文文章、帖子、博客、Notion 文档和方法论内容生成正文配图。

它不是通用插画 prompt，也不是 PPT 信息图模板。它的核心目标是：先理解文章里的认知锚点，再把其中一个判断、流程、结构、状态或隐喻，变成一张有记忆点的 16:9 手绘解释图。

默认视觉 IP 是"小黑"：一个黑色实心、白点眼、细腿、空表情的小角色。小黑不是吉祥物，不是贴纸，也不是站在角落里的装饰物，而是正在认真参与系统运转的荒诞工作者。

一句话：**让 AI 不只是"配一张图"，而是把文章里的一个关键认知动作画出来。**

---

## 适合谁用

特别适合：
- 写中文文章，需要正文配图和文章插图的人
- 做知识型内容、方法论内容、AI 工作流内容的人
- 想把抽象判断画成具体隐喻的人
- 想要一种比 PPT 信息图更轻、更怪、更有个人识别度的配图风格的人
- 用 Codex 做内容生产，希望稳定复用一套视觉语言的人

不适合：
- 想要商业插画、品牌 KV 或精致扁平插画的人
- 想要传统 PPT 信息图、复杂架构图或流程图的人
- 想要儿童卡通、可爱 IP、表情包风格的人
- 想把大量正文、长段解释或完整课程页塞进一张图里的人
- 需要严格可编辑矢量源文件的人

---

## 视觉风格

- 纯白背景，不要纸纹、米色、阴影、渐变
- 黑色手绘线稿，细线，轻微抖动
- 大量留白，主体只占画面约 40%-60%
- 少量红色、橙色、蓝色中文手写批注
- 一张图只表达一个核心动作、结构、状态或隐喻
- 小黑必须参与核心动作，不能只是装饰
- 怪诞、有创意、清爽，但不幼稚、不卖萌

---

## 工作流程

1. 读取文章、Markdown、Notion 内容、截图或用户给的主题
2. 提炼核心观点、认知转折、流程结构和适合视觉化的段落
3. 先输出 shot list：每张图只选一个认知锚点
4. 为每张图选择结构类型：Workflow、系统局部、前后对比、角色状态、概念隐喻、方法分层、地图路线或小漫画分镜
5. 重新发明一个低科技、怪诞但成立的物理隐喻
6. 让小黑承担核心动作
7. 每张图单独调用图像模型生成
8. 按 QA checklist 检查：白底、留白、小黑动作、中文标注、非 PPT 感、非旧案例复刻
9. 保存最终 PNG，并报告用途和路径

---

## 目录结构

```
.
├── README.md
├── LICENSE
├── NOTICE.md
├── assets/
│   └── ian-wechat-qr.jpg
├── examples/
│   ├── images/
│   │   ├── 01-two-breakpoints.png
│   │   ├── 02-sort-by-purpose.png
│   │   └── ...
│   └── prompts.md
└── ian-xiaohei-illustrations/
    ├── SKILL.md
    ├── agents/
    │   └── openai.yaml
    ├── assets/
    │   └── examples/
    └── references/
        ├── style-dna.md
        ├── xiaohei-ip.md
        ├── composition-patterns.md
        ├── prompt-template.md
        └── qa-checklist.md
```

真正需要安装到 Codex 的是子目录：`ian-xiaohei-illustrations/`

---

## 小黑 IP 定义

- 黑色实心小怪物
- 白色圆点眼睛
- 细腿，偶尔有细胳膊
- 身体可以是圆柱、黑豆、黑盒、漏斗、影子、洞口、机器内部黑块
- 轮廓略微不规则，有手绘感
- 表情空、呆、冷静、认真

**常见职责：** 搬运素材、拉线汇聚信息源、卡在断点里、在机器里操作"判断"杆、变成筛选漏斗、切开"素材鱼"、盖章承接话术、牵着承接路径、举警告牌看坑、从洞里伸手但接不住内容、在旁边搬砖/搭桥/开门/分拣/记录。

**禁止：** 过度可爱吉祥物、儿童卡通角色、复杂服装/表情包/闪亮眼睛、小黑只是站在角落里看。

---

## 八种构图模式

1. **Workflow 流程** — 输入->处理->输出，左侧输入/中间处理/右侧输出/橙色箭头
2. **系统局部** — 只画 3-5 个核心模块，小黑参与其中一个关键动作
3. **前后对比** — 左混乱右稳定，中间橙色箭头
4. **角色状态** — 2-4 个小状态，每个状态一个短标注
5. **概念隐喻** — 一个大的怪物件或机器，少量输入一个输出
6. **方法分层** — 一层层盒子，小黑在旁边搬砖或搭建
7. **地图路线** — 弯曲路径，少量节点，小黑牵线或走路
8. **小漫画分镜** — 2-4 个小场景，每格只表达一个动作

---

## 相关项目

- [Ian Handdrawn PPT](https://github.com/helloianneo/ian-handdrawn-ppt) — 中文手绘技术 PPT-style 页面图生成 Skill
- [Awesome Claude Code Skills](https://github.com/helloianneo/awesome-claude-code-skills) — Claude Code Skills / Agents / Plugins 精选合集
- [Obsidian + Claude AI Second Brain](https://github.com/helloianneo/obsidian-ai-second-brain) — Obsidian + Claude AI 个人知识库搭建指南

---

## 关于作者

**Ian (伊恩)** — 产品设计师 / 一人公司实践者 / AI Builder

- GitHub: [helloianneo](https://github.com/helloianneo)
- X/Twitter: [@ianneo_ai](https://x.com/ianneo_ai)
- 网站: [www.ianneo.xyz](https://www.ianneo.xyz)
- 微信: `ianneoxyz`
- 邮箱: hello.neoc@gmail.com

---

## 基础信息

- Stars: 9,582
- Forks: 1,208
- License: MIT
- Created: 2026-05-27
- Updated: 2026-08-19
- GitHub: https://github.com/helloianneo/ian-xiaohei-illustrations
- Homepage: https://www.ianneo.xyz
