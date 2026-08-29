---
title: Anatomy Atelier
author: thebuggeddev
created: 2026-08-29
updated: 2026-08-29
type: entity
tags: [open-source, product, creative, design, multimodal]
sources: [raw/articles/anatomy-README.md]
---

# Anatomy Atelier

Anatomy Atelier 是 `thebuggeddev/anatomy` 项目中的交互式 3D 人体解剖学习器：用 Three.js 展示器官模型、热点标注、对比和标注测验，把医学知识做成偏艺术化的学习体验。GitHub 在 2026-08-29 的快照为 2,760 stars、769 forks。

- **GitHub**: https://github.com/thebuggeddev/anatomy
- **官网**: https://anatomyatelier.vercel.app
- **语言**: TypeScript | **许可证**: GitHub 元数据未声明
- **技术栈**: React 19、Next.js 16/vinext、Three.js、GSAP、Vite
- **运行要求**: Node.js `>=22.13.0`

## 核心能力

| 特性 | 说明 |
|------|------|
| 3D 器官查看器 | GLB 模型、OrbitControls 旋转/缩放、自动旋转、重置、隔离、图层/剖面工具 |
| 热点标注 | 点击模型上的结构热点，查看部位名称与功能说明 |
| 器官库 | 覆盖心脏、大脑、肺、肝脏、肾脏、眼球、肠道、胰腺、皮肤 |
| 学习辅助 | Guided lesson、显微视图、功能动画、临床笔记、常见疾病和身体系统卡片 |
| 标注测验 | 乱序询问每个热点；错误后标出正确位置，最终给出得分 |
| 对比模式 | 将当前器官与参考器官并列，展示主要功能和尺度 |
| 多语言 | 英/西/印地/中/阿/葡/法/德/日/俄/印尼/韩 12 种 locale |

## 实现要点

项目将稳定的解剖结构与翻译内容分离：`app/lib/anatomy-data.ts` 只保存器官 ID、模型路径、颜色、拉丁学名和热点坐标；`app/i18n/organs/*.ts` 保存器官名称、事实、医学说明和热点文案。这种设计让新增语言不必复制 3D 场景数据。

`AnatomyViewer` 采用 Three.js 渲染器、环境光/方向光/点光源和预烘焙接触阴影；代码显式关闭实时 shadow mapping，以降低每帧成本。它还通过 `IntersectionObserver`、页面可见性和 dirty 标记控制渲染，只有场景变化时才绘制。React 层通过 ref 把长期存活的 Three.js 回调连接到当前测验状态，避免回调捕获旧状态。

仓库 README 仍主要是通用的 `vinext-starter` 说明，包含 Cloudflare D1/Drizzle、workspace auth headers 和可选 Sign in with ChatGPT 的文档；实际 `app/` 代码则实现了上述 Anatomy Atelier 产品界面。

## 与 [[ui-ux-pro-max]]、[[gsap-skills]] 的关系

- **[[ui-ux-pro-max]]**：同样关注 AI 生成产品的视觉系统和交互质量；Anatomy Atelier 是一个具体的设计型教育产品实例，而不是通用设计规则库。
- **[[gsap-skills]]**：项目直接使用 GSAP 做内容 reveal/fade 动画；与 GSAP 技能页形成“库的使用方法—实际产品案例”的关联。
- **[[mano-p]]**：都涉及 3D/视觉交互，但 Mano-P 面向 GUI-VLA 端侧智能体，Anatomy Atelier 面向人体解剖教育，二者不是直接竞品。

## 适用场景

- 医学或生物学入门学习的交互式演示
- 设计型教育产品、数字展品和作品集项目
- 研究 Three.js 模型加载、热点标注与 WebGL 性能优化
- 观察多语言内容模型与 locale-independent 数据结构如何协作

## 局限性

- GitHub 元数据未声明开源许可证，不能默认推断可自由复用模型或素材。
- README 与实际产品代码存在明显错位，项目定位和部署说明需要使用者自行核对。
- 页面文案虽然包含医学事实和疾病列表，但仓库没有说明医学专家审核或参考文献体系，不应当替代医学教材或临床资料。
- 3D 模型、图像和 WebGL 渲染带来较大的资源体积与设备性能要求；低性能设备会采用较低像素比和关闭抗锯齿等降级策略。

## 相关页面

- [[ui-ux-pro-max]] — AI 编程中的界面设计系统与行业规则
- [[gsap-skills]] — GSAP 动画库的 Agent 使用技能
- [[mano-p]] — 另一类 3D/视觉交互项目，但定位是 GUI 智能体
