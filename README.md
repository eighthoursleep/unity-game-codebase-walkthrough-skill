# Unity 客户端文档 Skills（Claude Code）

本仓库是一组面向 **Unity 游戏客户端项目** 的 Claude Code 技能，解决同一件事的三个层次：**看懂一个既有工程，并把它沉淀成文档**——先出一页项目总览，再按层盘点模块清单，最后把单个模块写成由浅入深的教学系列。

所有产出为中文 markdown，统一落在目标工程的 `AboutMe/` 目录下。

## 技能一览

| 技能 | 粒度 | 作用 | 产出 |
|------|------|------|------|
| [unity-client-overview](unity-client-overview/SKILL.md) | 整个项目 | 架构总览：引言元信息块 + 项目概述 + 分层目录速查 + 启动流程 + 开发约定与风险（60–110 行） | `AboutMe/Overview.md` |
| [unity-module-overview](unity-module-overview/SKILL.md) | 某一层 | 模块清单：编号表格（序号｜模块｜路径｜职责说明），回填已有模块文档链接 | `AboutMe/<层名>/README.md` |
| [unity-teach-module](unity-teach-module/SKILL.md) | 单个模块 | 教学文档系列：总览 README + 编号章节，每份 ≤300 行，由浅入深 | `AboutMe/<层名>/<模块名>/README.md` + `01-*.md` |

三者的关系是**由粗到细**，但彼此独立，可按需单独使用：

```
unity-client-overview          unity-module-overview        unity-teach-module
  整个项目骨架         ──▶        某一层的模块清单    ──▶      某个模块怎么运转
  AboutMe/Overview.md            AboutMe/<层>/README.md       AboutMe/<层>/<模块>/*.md
```

- `unity-client-overview` 建立全局认知，回答"这是什么项目、怎么分层、怎么启动"。
- `unity-module-overview` 只做清单，不做模块内部内容分析。
- `unity-teach-module` 深挖单个模块，收尾时会在 `AboutMe/Overview.md` 里登记新系列链接（因此它假定总览已存在，但缺失时也能跑）。

## 使用方式

**复制到 Unity 项目**：把需要的 skill 目录整个拷到目标工程的 `.claude/skills/` 下即可，例如：

```
<Unity 项目>/.claude/skills/unity-client-overview/SKILL.md
<Unity 项目>/.claude/skills/unity-module-overview/SKILL.md
<Unity 项目>/.claude/skills/unity-teach-module/SKILL.md
```

每个 skill **自包含**：划分口径、格式规范、模板全部内联在各自的 SKILL.md 里，不依赖任何共享文件，也不需要额外配置。用哪个拷哪个。

**触发**：各 SKILL.md 的 `description` 已写明触发场景，直接自然语言描述需求即可命中（"给这个项目生成 Overview""更新一下 C#功能层的模块清单""把战斗模块写成由浅入深的系列文档"），也可以用 `/unity-client-overview` 之类显式调用。

## 仓库结构

```
ClaudeSkills/
├── README.md
├── unity-client-overview/
│   ├── SKILL.md
│   └── evals/evals.json          ← 该 skill 的评测用例
├── unity-module-overview/
│   └── SKILL.md
└── unity-teach-module/
    └── SKILL.md
```

## 共同约定

- 产出全部落在目标工程的 `AboutMe/` 下，三个 skill 的落点互不覆盖（`Overview.md` / `<层名>/README.md` / `<层名>/<模块名>/`）。
- 各 skill 均假定 `AboutMe/` **未纳入版本控制**：删除或覆盖既有文档前会先报告并要求确认，不做静默删除。
- 一律不修改业务代码，只读代码、写文档。
