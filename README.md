# Claude Skills 索引

本目录下是一组 **Unity 项目分析技能**,按「项目 → 一级模块 → 子模块 → 核心逻辑 → 流程」逐层下钻,协作生成分层架构文档。

## 🚀 使用工作流（复制到 Unity 项目 + 改规则）

**复制到 Unity 项目**（每个 skill 已自包含,不用带 `_shared`）:
1. 把 `unity-project-overview/`、`unity-module-overview/`、`unity-module-detail/`、（可省）`unitygame-core-flow-doc/` 三个/四个文件夹拷贝到目标 Unity 项目的 `.claude/skills/` 下。
2. 直接调用 skill 即可;各 skill 内联了完整划分规范,复制后无需额外配置。

**修改划分规则**（统一维护入口）:
1. 编辑权威母本 `_shared/module-division-guide.md`。
2. **同步**三个 `unity-` skill 正文里的同段内联副本,保持一致。
3. 若已复制到某项目,把更新后的 SKILL.md 一并拷回项目。

> 规则不在各 SKILL.md 外部依赖中,故复制/修改互不牵连,但改规则时记得「母本 + 内联副本」两处一起改。

> **另有一处需同步的内联副本**：`unity-module-detail` 与 `unitygame-core-flow-doc` 各自内联了一份同源的「一级模块归属判定」规则（决定 `<一级模块名>/<子模块名>` 输出目录）。改动该规则时，这两份也要一起改（同样为保持 skill 自包含，未抽到 `_shared`）。

## 技能一览

| 技能 | 侧重层 | 作用 | 输出 |
|------|------|------|------|
| [unity-project-overview](unity-project-overview/SKILL.md) | 一级模块层 | 列出一级模块 + 模块间**依赖关系** | `项目根/AboutMe/Overview.md` |
| [unity-module-overview](unity-module-overview/SKILL.md) | 子模块层 | 列出某一级模块下的子模块 + 子模块间**依赖关系** | `项目根/AboutMe/<一级模块名>.md` |
| [unity-module-detail](unity-module-detail/SKILL.md) | 核心逻辑层 | 单个子模块的职责/功能/边界 + **按职责功能划分的所有核心逻辑**清单 | `项目根/AboutMe/<一级模块名>/<子模块名>.md` |
| [unitygame-core-flow-doc](unitygame-core-flow-doc/SKILL.md) | 流程层 | 对 detail 产出的核心逻辑**详细解析**（跨模块全链路深挖） | `项目根/AboutMe/<一级模块名>/<子模块名>/<核心流程名>.md` |

**数据流**:项目 → 一级模块 → 子模块 → 核心逻辑 → 流程。上游产出的清单是下游的输入:
- `Overview.md`(一级模块+依赖) → `<一级模块名>.md`(子模块+依赖) → `AboutMe/<一级模块名>/<子模块名>.md`(核心逻辑清单) → `AboutMe/<一级模块名>/<子模块名>/<流程名>.md`(单条核心逻辑的流程详析)。

**目录形状**（清单与流程套嵌,注意二者不是同级）:

```
AboutMe/
  Overview.md                      ← project-overview
  <一级模块名>.md                  ← module-overview（文件）
  <一级模块名>/                    ← 同名目录,与上面的文件共存
    <子模块名>.md                  ← module-detail（清单）
    <子模块名>/                    ← 同名目录,与上面的文件共存
      <核心流程名>.md              ← core-flow-doc（流程详析,无编号前缀）
```

## 共用规范（重要）

三个技能在划分模块/系统、子模块/子系统时的判定规则是**统一**的,集中维护在一份共用规范中:

> 📄 **[《模块/系统划分原则》](_shared/module-division-guide.md)**

**ⓘ 部署说明**：下面这份文件是划分规则的**权威母本**。skill 会被复制到其他 Unity 项目里使用，因此**每个依赖它的 skill 都已内联了完整规则副本**（自包含），复制后即便读不到母本也能正常运行。**修改划分规则时改这一份母本，并同步各 SKILL.md 的内联副本**。

**核心一句话**:模块按**逻辑职责**划分;类名前缀(或命名空间)相同的 一组类属于同一模块,不得拆成多个。

**模块大类**:每个模块除所属领域外,还须标注层面 **B=底层 / F=框架 / A=应用**(理想依赖流向 应用→框架→底层;反向依赖标架构警讯)。