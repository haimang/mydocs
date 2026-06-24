# Nano-Agent 文档模板 · README（项目总结 · 对外报告）

> **模板类型**：`report / project-README`（落 `eval-` 命名空间；借 **eval 共有脊** + **`eval-state-analysis` 对账诚实**，但产出是**对外交付物**而非内部 eval）
> **一句话用途**：为一个项目（新建或既有）产出**单一权威的顶层 `README.md`**——讲清"这是什么、技术底座、模块/目录、第三方集成与 BFF、构建测试部署、安全配置、当前真实状态、已知事项"，供**新贡献者 onboarding / 业主巡检 / 交接人**阅读。
> **何时用**：① 给一个仓库写/重写顶层 `README.md`；② 阶段性"项目总结与汇报"；③ 把分散在多文档的事实收敛成一份对外快照。
> **何时不用**：① 内部"接下来做什么"的提案 → `eval-general-purpose`；② 里程碑后的内部对账/债务盘点 → `eval-state-analysis`；③ 给制品下收口结论 → `closure`；④ 单目录的 ownership/边界规则 → 用本模板**档位 C**（极简），不必整篇。
>
> **档位选择（先选一档，照 `closure.md` 先选档纪律）**：
> - **档 A · 架构 README（默认）**：开发者 / onboarding / 交接向，完整骨架（§0–§13）。对标 `archy-web/README.md`。
> - **档 B · 运营手册**：运营 / 内容编辑向（"改 logo·页脚·精选在哪、缓存怎么刷"）。在档 A 基础上启用**附录 A**，或单独成篇。对标 `aventra-web/README.md`。
> - **档 C · 局部 ownership**：只为**单个目录**写边界/红线规则，极简。用**附录 B**，不展开 §1–§13。对标 `haimang-web/runtime/README.md`。
>
> **使用纪律（共有脊 · 与所有 eval 模板一致 + 本模板特化）**：
> 1. 产出是**对外/onboarding 交付物**，给"第一次读这个仓库的人"看；语气面向读者，不是面向内部决策流。
> 2. **对账诚实红线（继承 `eval-state-analysis §3` · 本模板灵魂）**：README 里每一句 `live / 已落地 / 全绿 / 已接入` 都必须能被**一条 grep / 一次 test / 一个部署链接**坐实；`frozen ≠ live`、占位（placeholder）、未接线、known-bug、占位凭据一律在 **§12 已知事项**点名，**不得粉饰成"已完成"**。每个能力都要带 **§4.7 状态图例**之一。
> 3. **零决策**：README 只**描述**既有事实与既定政策，**不在此新冻结**任何 owner 决策——决策真源仍是 `qna` register，引用时只述结论 + Q 编号。
> 4. **头部 / 性质声明 / TL;DR（一句话定位）/ 输入锚定（技术栈 + 目录锚）/ 修订历史**为共有脊。
> 5. **结构来源（dogfood）**：兄弟项目 README 通用格式（`archy-web` 架构向 + `aventra-web` 运营向 + `haimang-web/runtime` 局部 ownership）+ `eval-state-analysis §3 对账诚实` + eval 共有脊头部。
>
> **占位符约定**：统一 `{UPPER_SNAKE}`，backtick 包裹。`[核心]` = 必填段；`[可选·X]` = 仅当项目具备 X（如多语 / SEO / 营销 / 特色子系统）时启用，否则**整段删除**（不留空壳）。

---

# `{PROJECT_NAME}`

> `{ONE_LINE_POSITIONING}` ——一句话说清**是什么 + 技术底座 + 面向谁 / 覆盖哪些能力面**。
> 例（archy）：「基于 **Astro 5 + Cloudflare Pages** 的建筑可视化工作室官网。面向英/中/印三语，覆盖内容驱动作品集、EDM 落地页、表单/退订 BFF、UE 第三方集成与一套交互工具子系统，配套完整 SEO / i18n。」

> **文档性质**：`report / project-README`（对外交付物；继承 eval 对账诚实，零决策）
> **文档状态**：`draft | reviewed | frozen | superseded`
> **README 档位**：`A 架构 | B 运营手册 | C 局部 ownership`
> **维护者**：`{MAINTAINER}`
> **最后核对（against HEAD）**：`{DATE} @ {COMMIT_OR_BRANCH}` ←（对账诚实锚：README 未对照真实代码复核就会漂成谎；每次发布更新此值）
> **对外地址**：`{LIVE_URL_OR_NA}`
> **总体状态**：`{OVERALL_STATUS}`（如 `站点+退订链路 live；工具子系统已落地`）

> 注：发布到仓库根的 `README.md` 时，上面"文档性质/状态/档位"等**模板内部字段可裁剪**，建议至少保留 *维护者 / 最后核对 / 对外地址 / 总体状态* 四行作为可信元信息。

---

## 1. 项目综述 `[核心]`

> 用途：一段叙述讲清项目本体 + 核心能力 bullet + **当前真实状态**（对账诚实落点之一）。读完这一节，读者应能回答"这仓库是干什么的、跑在哪、现在到哪一步"。

`{PROJECT_NAME}` 是 `{WHAT_IT_IS_NARRATIVE}`。`{HOW_IT_WORKS_HIGH_LEVEL}`（数据来源 / 构建模式 / 渲染方式 / 部署目标 / BFF 承接哪些动态能力）。

**核心能力**：

- **`{CAPABILITY_1}`**：`{ONE_LINE}`
- **`{CAPABILITY_2}`**：`{ONE_LINE}`
- **`{CAPABILITY_N}`**：`{ONE_LINE}`

> **当前状态（对账诚实 · 逐项带状态词 + 证据锚）**：每条能力标注 §4.7 状态词，`live / 已落地` 必须可坐实，占位与未接线显式列出。

| 能力 / 链路 | 状态 | 证据锚（`path:line` / test / 部署链接） |
|------------|------|------------------------------------------|
| `{CAPABILITY}` | `live / 已落地 / 占位 / 计划中 / 已退役` | `{EVIDENCE}` |

---

## 2. 技术栈 `[核心]`

> 用途：一表交代每一层用什么 + 为什么。保留中文表头 + 英文技术名（如 `getStaticProps` / BFF / SSG 不译）。

| 层级 | 技术 / 库 | 说明 |
|------|-----------|------|
| `{LAYER}`（如 框架 / 运行平台 / 语言 / 集成 / 加密 / 测试） | `{TECH}` | `{NOTE}` |

> 依赖面取舍可在此用 `>` 旁注一句（例：「运行依赖刻意极小，未引入前端框架，工具引擎手写」）。

---

## 3. 模块总览 `[核心]`

> 用途：按**层 / 子系统**拆解项目，每层一句话 + 关键文件。这是 §4 目录树的"语义版"。按项目实际层次裁剪小节。

### 3.1 `{LAYER_OR_SUBSYSTEM}`（如 内容层 / 数据层）
`{PATH}`：`{RESPONSIBILITY}`。`{KEY_FILES_AND_ROLE}`。

### 3.2 `{LAYER_OR_SUBSYSTEM}`（如 i18n 层 / 路由·布局·组件 / 状态·缓存）
`{PATH}`：`{RESPONSIBILITY}`。

### 3.3 `{LAYER_OR_SUBSYSTEM}`（如 BFF / API 层）
`{PATH}`：`{RESPONSIBILITY}`（详见 §9）。

### 3.N `{FEATURE_SUBSYSTEM}`（项目特色子系统 → 详见 §8）

---

## 4. 目录结构 `[核心]`

> 用途：一棵**带行内注释**的目录树，让读者按图索骥。只列承载意义的目录/文件，注释写"装什么"。

```text
{PROJECT_ROOT}/
├── {CONFIG_FILE}              # {WHAT}
├── .env.example              # 环境变量模板（构建时 / 运行时见 §11）
├── AGENTS.md                 # 面向 AI agent 的仓库级操作指南（如有）
│
├── {SRC_OR_APP}/             # {WHAT}
│   ├── {CONTENT_OR_DATA}/    # {WHAT}
│   ├── {I18N}/               # {WHAT}（如多语，详见 §5）
│   ├── {ROUTES}/             # {WHAT}
│   └── {COMPONENTS}/         # {WHAT}
│
├── {BFF_DIR}/                # BFF（详见 §9）：第三方密钥只在此后端
│   └── {API_AND_LIB}/        # {WHAT}
│
├── {PUBLIC_OR_STATIC}/       # {WHAT}
├── scripts/                  # {BUILD_OR_OPS_SCRIPTS}
└── tests/                    # {TEST_LAYERS}（详见 §10）
```

---

## 5. 翻译机制 / i18n `[可选·多语]`

> 用途：仅多语项目启用。讲清 locale 集、URL 策略、翻译数据模型、回退规则、UI 文案、SEO 多语言、**新增语言的步骤**。单语项目整段删除。

### 5.1 Locale 与 URL 策略
- 语言集：`{LOCALES}`（默认 `{DEFAULT_LOCALE}`）。
- 策略：`{URL_STRATEGY}`（前缀 / 重写 / fallback 规则，如 `prefixDefaultLocale:false` + `fallbackType:'rewrite'`）。

### 5.2 翻译数据模型
`{TRANSLATION_MODEL}`（如单文件多语言 `Translatable` leaf；或 `next-i18next` ns 字典；或 API-field 由后端返回）。

```json
{ "title": { "{DEFAULT_LOCALE}": "...", "{LOCALE_2}": "...", "{LOCALE_N}": "..." } }
```

- 回退规则：`{FALLBACK_RULE}`（字段级回退，缺失不整页 404）。
- 不参与翻译的：`{NON_TRANSLATABLE}`（URL / ID / 图片引用 / 数字）。

### 5.3 解析机制与 UI 文案
- 内容解析：`{RESOLVER}`（`path:line`）。
- UI chrome 文案：`{UI_DICT}`（`path:line`）。

### 5.4 SEO 多语言 / Sitemap
`{HREFLANG_CANONICAL_SITEMAP_NOTES}`（hreflang + `x-default`；sitemap 是否需 `customPages` 显式枚举非默认 locale）。

### 5.5 新增语言步骤
`{STEPS_TO_ADD_LOCALE}`（按顺序：locale 常量 → 配置 → UI 字典 → 内容补 leaf →（字体）→ sitemap → smoke → build/check）。

---

## 6. SEO `[可选]`

> 用途：集中说明 SEO 出口（title/description/canonical/OG/Twitter/JSON-LD/robots）由谁统一输出，以及安全/缓存响应头。

- 集中出口：`{SEO_COMPONENT}`（`path`）输出 `{SEO_FIELDS}`。
- 结构化数据：`{JSONLD_BUILDERS}`。
- 响应头：`{HEADERS_FILE}` 配 CSP / HSTS / X-Frame-Options 等；`connect-src` 白名单 = `{CSP_CONNECT_SRC}`。

---

## 7. 内容 / 营销子系统 `[可选·可重复]`

> 用途：仅当项目有 EDM / 内容精选（curation）/ 落地页等内容运营子系统时启用。可按子系统重复本节。对标 archy §7（EDM）与 aventra §5（curation）。

### 7.1 架构与数据源
`{SUBSYSTEM_ARCHITECTURE}`（如 EDM 三层：邮件源 → 静态落地页 → 退订 BFF；或 curation 白名单 JSON → BFF 过滤 → 公开排序）。

### 7.2 配置 / Manifest
| 字段 | 作用 |
|------|------|
| `{FIELD}` | `{WHAT}` |

### 7.3 新增 / 运营流程
`{HOW_TO_ADD_OR_OPERATE}` + **投递/上线前 checklist**（合规、禁外链、占位符替换等，如有）。

> ⚠️ 若存在**投递前必修**项（如邮件源退订占位符未替换、硬编码链接），在此用 `>` 显式警告并交 §12。

---

## 8. 特色能力子系统 `[可选·可重复]`

> 用途：项目独有的、值得深讲的能力（如 archy 的 ColorSnap 交互工具）。讲清"它做什么 / 核心不变量 / 数据模型 / 客户端引擎 / 鉴权签名 / 页面装配 / 如何扩展"。无特色子系统则整段删除。

### 8.1 它做什么
`{WHAT_IT_DOES}`。

### 8.2 核心不变量 / 数据模型
`{CORE_INVARIANTS_AND_MODEL}`（点名"绝不能破"的不变量）。

### 8.3 鉴权 / 信任边界（如涉及）
`{AUTH_AND_TRUST_BOUNDARY}`（能力式 / token / 签名 / 服务端独立校验；写接口 Origin 门；密钥缺失失败关闭）。

### 8.4 如何新增 / 扩展
`{HOW_TO_EXTEND}`。

---

## 9. BFF 层与第三方集成 `[核心]`

> 用途：几乎所有兄弟项目的共性核心——前端只触达 `/api/*`，第三方 `appid/appSecret/token/scene` 与签名密钥只存在于后端。讲清隔离、路由、中间件/CORS、token、缓存、配置。第三方常为 **UE（UnifyEstate）**。

### 9.1 定位与隔离边界
`{BFF_RUNTIME}`（Cloudflare Pages Functions / Express / Next API routes）作 BFF：浏览器**不直接请求** `{THIRD_PARTY}`；`{SECRETS_LIST}` 只在 `context.env` / 服务端。

### 9.2 API 路由表
| 路由 | 方法 | 说明 |
|------|------|------|
| `{ROUTE}` | `{METHOD}` | `{WHAT}` |

### 9.3 中间件与 CORS
`{MIDDLEWARE}`：`{OPTIONS_CORS_ORIGIN_RULES}`（同源/localhost 放行规则；写接口 Origin 门）。

### 9.4 第三方配置 / token / 客户端 / 缓存
- 配置（`{CONFIG_FILE}` + `{ENV_SOURCE}`）：`{UE_CONFIG_KEYS}`（`{THIRD_PARTY}_BASE_URL` / `APP_ID` / `APP_SECRET` / `SCENE` / `TOKEN_TTL` / `MOCK_FALLBACK` …）。
- token（`{TOKEN_MANAGER}`）：`{TOKEN_STRATEGY}`（模块级缓存、提前刷新窗、防并发重复刷新）。
- 客户端（`{CLIENT}`）：`{CLIENT_NOTES}`（自动注入 scene/token、超时、授权失败重试一次）。
- 缓存（如有，`{CACHE_DIR_OR_LAYER}`）：`{CACHE_TTL_AND_REFRESH}`（默认 TTL；token 刷新触发预拉取；手动刷新接口见附录 A / aventra §7）。

### 9.5 第三方接口配置表
| 变量 | 当前值 | 含义 |
|------|--------|------|
| `{ENV_VAR}` | `{VALUE_OR_PLACEHOLDER}` | `{MEANING}` |

> 占位凭据（`{PLACEHOLDER_SECRETS}`）须在正式启用前由业主替换为真值——列入 §12。

---

## 10. 构建、测试与部署 `[核心]`

> 用途：可复制的命令 + 构建产物特性 + 测试分层 + 部署口径。

### 10.1 命令
```bash
{INSTALL_CMD}            # 安装依赖
{DEV_CMD}               # 本地开发
{BUILD_CMD}             # 构建
{CHECK_OR_LINT_CMD}     # 类型 / lint 校验
{TEST_CMD}              # 测试
{PREVIEW_CMD}           # 预览构建产物
{DEPLOY_CMD}            # 部署
```

> 若 dev/preview 需**同时起前端 + BFF**（如 aventra `5010`/`5011`），在此点明端口与"preview 不替代 BFF"的坑。

### 10.2 构建产物特性
`{BUILD_OUTPUT_NOTES}`（SSG 路由形态 / locale 镜像与 prune / 重写规则等）。

### 10.3 测试分层
| 套件 / 层 | 跑法 | 覆盖 |
|-----------|------|------|
| `{TEST_SUITE}` | `{CMD}` | `{WHAT_IT_COVERS}` |

> **对账诚实**：此处声明"全绿"的套件，§12 不得同时挂着该套件的 known-fail；BFF/Functions 若不在某 preview 下运行需点明（手测口径）。

### 10.4 部署
`{DEPLOY_FLOW}`（build → deploy 目标）。发布后**提取并明确报告**生产/部署主地址，保留预览/别名。

---

## 11. 安全与配置策略 `[核心]`

> 用途：环境变量"构建时 vs 运行时"分野、密钥政策、BFF 隔离、响应头。

### 11.1 环境变量：构建时 vs 运行时
| 变量 | 时机 | 暴露面 | 说明 |
|------|------|--------|------|
| `{VAR}` | `构建时 / 运行时` | `import.meta.env / context.env / 仅服务端` | `{NOTE}` |

### 11.2 密钥政策
`{SECRETS_POLICY}`（存哪（`wrangler.toml [vars]` / Secrets / `.env`）、谁的既定政策、来源文件、是否迁移、占位值替换要求）——引用 owner 决策只述结论 + 来源（如 `qna` Q 编号 / 日期）。

### 11.3 BFF 隔离与接口防护
`{BFF_HARDENING}`（第三方密钥/签名密钥仅后端；写接口 Origin 门 + token；密钥缺失失败关闭；smoke 断言页面不泄露后端串）。

### 11.4 响应头
`{RESPONSE_HEADERS}`（CSP / HSTS / X-Frame-Options …）。

---

## 12. 已知事项与设计取舍 `[核心 · 对账诚实落点]`

> 用途：本模板与"普通 README 指南"的分水岭。**设计亮点**给读者价值地图；**待办/需复核**把占位、未接线、known-bug、投递前必修、占位凭据**全部摊开**——这是 §1 当前状态承诺的兑现处。

### 设计亮点
- **`{HIGHLIGHT_1}`**：`{WHY_GOOD}`
- **`{HIGHLIGHT_N}`**：`{WHY_GOOD}`

### 待办 / 需复核
| 编号 | 事项 | 严重 / 时机 | reopen / 修复触发器 |
|------|------|-------------|----------------------|
| 1 | `{TODO_OR_KNOWN_ISSUE}`（如"占位凭据未替换""投递前必修""组件体系未接入"） | `投递前必修 / 上线前 / 长期` | `{TRIGGER}` |

> **诚实闸**：凡 §1/§10 标了 `live / 全绿` 的，若此处仍有对应未闭合项，必须在两处口径一致（不得一处报喜、一处藏雷）。

---

## 13. 总体评价 `[核心]`

> 用途：一段收尾。架构画像 + 适配性 + 上线前需优先处理的 1–2 个点（呼应 §12）。

`{OVERALL_ASSESSMENT_PARAGRAPH}`

---

## 附录

### A. `[档位 B · 可选]` 运营 / 编辑手册

> 用途：面向**网站运营者 / 内容编辑**（非开发者）。对标 `aventra-web/README.md`。可启用为本附录，或单独成篇 README。

#### A.1 改品牌 / logo / 站点名 / 页脚在哪
路径：`{BRAND_CONFIG_PATH}`。生效字段：

| 字段 | 作用 |
|------|------|
| `{FIELD}` | `{WHAT}` |

#### A.2 内容精选 / 展示范围控制
路径：`{CURATION_PATH}`。

| 文件 | 控制什么 | 页面影响 |
|------|----------|----------|
| `{FILE}` | `{WHAT}` | `{PAGES}` |

排序/上下架/置顶规则：`{CURATION_RULES}`。

#### A.3 缓存与手动刷新
- 缓存目录（运行时产物，**勿手改**）：`{CACHE_DIR}`，默认 TTL `{TTL}`。
- 手动刷新：
```bash
{CACHE_REFRESH_CMD}   # 需 {REFRESH_SECRET_ENV}，勿泄露
```
- 什么时候**该**刷新 vs **刷新也没用**（改的是配置/代码 → 需重启或重建重发）：`{WHEN_TO_REFRESH}`。

#### A.4 配置类型总表（"什么改哪里"）
| 类型 | 路径 | 面向谁 | 用途 | 运营可直接改？ |
|------|------|--------|------|----------------|
| `{TYPE}` | `{PATH}` | `{AUDIENCE}` | `{PURPOSE}` | `是 / 谨慎 / 否` |

#### A.5 常用命令速查 & 改完之后要做什么
```bash
{COMMON_COMMANDS}
```
改 `{REPO_CONFIG}` 后：本地重启 / 重建重发；改 `{UPSTREAM_DATA}` 后：刷新缓存。**最后记住**：`{TOP_3_REMINDERS}`。

---

### B. `[档位 C · 可选]` 局部目录 ownership 规则

> 用途：当 README 只为**单个目录**定边界/红线（不展开 §1–§13）。对标 `haimang-web/runtime/README.md`。极简：目录布局 + 编号 hard gates。

**目录布局**
- `{DIR}/{SUBDIR_A}/` — `{RESPONSIBILITY}`。`{ALLOWED_IMPORTS}`。
- `{DIR}/{SUBDIR_B}/` — `{RESPONSIBILITY}`。`{FORBIDDEN_IMPORTS}`。

**Hard gates**
1. `{GATE_1}`（如 `A/**` 不得 import `B/**`）。
2. `{GATE_2}`（含合法例外的边界，如 SSR 函数内 `await import(...)`）。
3. `{GATE_N}`。

---

### C. 修订历史

| 版本 | 日期 | 作者 | 主要变更 |
|------|------|------|----------|
| v0.1 | `{DATE}` | `{AUTHOR}` | 初稿 |
