---
name: '@0x33a/anti-zh_llm'
description: Eliminate AI-generated UI/UX anti-patterns (AI slop / AI泔水味) and robotic product copywriting (zh_llm flavor) when building, refactoring, or reviewing web and desktop applications. Use whenever the user asks to create, polish, audit, or de-AI-ify frontend interfaces, UI components, layouts, interaction flows, or UI copywriting.
---

# Anti AI Slop UI (去 AI 泔水味前端与交互规范)

Eliminate common AI-generated frontend anti-patterns, fragmented layouts, broken CSS box-models, nonsensical state flows, and robotic UI copywriting (`zh_llm` flavor) to produce cohesive, human-grade interfaces.

## When to Use (适用场景)

* Building or styling web applications, desktop apps (Electron / Tauri / Qt), dashboards, or component libraries

* Auditing, critiquing, or refactoring existing UI/UX to remove "AI slop" or "AI flavor" (去 AI 味 / 去 AI 泔水)

* Rewriting robotic, verbose, or defensive UI copywriting, tooltips, and error messages (`zh_llm` 翻译腔与机器味文案)

* Fixing layout inconsistency, low screen utilization, or broken hover/border-radius states

## Core Rules & Workflow (核心审查与开发规范)

### 1. Purge Robotic Copywriting (剔除 `zh_llm` 机器味与挽尊文案)

Write concise, task-oriented UI text that speaks the user's language rather than exposing internal prompt constraints or system mechanics.

* **Strip defensive or self-justifying explanations (严禁挽尊式/防御性内部解释)**:

  * Never display internal architectural disclaimers in user-facing modals (e.g., explaining why an OAuth client ID was chosen, or promising "will not switch to another client's identity / 不会切换到其他启动器身份").

  * State only what happened and what the user needs to do next.

* **Delete filler slogans and redundant subheaders (删除车轱辘话副标题与空洞口号)**:

  * Remove generic AI-generated taglines under page titles (e.g., "Your workspace, independently managed / 你的游戏，独立管理" or "Changes take effect immediately based on actual return values / 参数修改即时下发，以实际返回结果为准").

  * If a section header is already clear (e.g., "Account Settings"), do not add a subtitle repeating "Manage and configure your accounts here".

* **Make action labels explicit (杜绝无宾语的裸动词按钮)**:

  * Never use bare, ambiguous verbs like `Import (导入)`, `Select (选择)`, or `Manage (管理)` on global toolbars when multiple entity types exist.

  * Specify the target object explicitly (e.g., `Import Modpack / 导入整合包`, `Import Profile / 导入配置`).

* **Use clear subject-verb state labels (杜绝主谓不明的状态缩略词)**:

  * Replace vague passive labels like `Waiting for selection (等待选择)` with explicit status text such as `No instance selected (未选择实例)`.

* **Remove debug and demo artifacts (严禁在正式界面暴露调试/Demo 残留)**:

  * Strip all test toggles, heartbeat log demos (`demo-heartbeat / 演示心跳日志`), and mock items before shipping production views.

### 2. Unify Layout Shells and Information Density (强制布局复用与空间利用率)

Prevent the visual fragmentation that occurs when an LLM generates each page or modal in isolation.

* **Share a single page-header and toolbar component (同级页面强制复用顶栏与布局骨架)**:

  * Peer views (such as different resource tabs, asset managers, or list pages) must reuse the exact same header and filter-bar component.

  * Keep shared actions like `Refresh (刷新列表)`, `Search (搜索)`, and filter controls in identical coordinates across all tabs so buttons never jump around when switching views.

* **Maximize horizontal utilization (提高横向空间利用率，拒绝无脑纵向堆叠)**:

  * Group related search inputs, category pills, sort dropdowns, and refresh buttons onto a single compact toolbar row rather than stacking them vertically across multiple sparse rows.

* **Standardize control heights and spacing (统一同行控件高度与上下间距)**:

  * Enforce a strict height token (e.g., `32px` or `36px`) across all buttons, text inputs, and select dropdowns sitting on the same row.

  * Always apply explicit `gap` tokens (e.g., `gap: 8px` or `12px`) between stacked form controls so adjacent inputs or dropdowns never touch at zero distance ("负距离接触").

* **Demote low-frequency configuration (低频设置收进二级页面，禁止主界面重复入口)**:

  * Move one-time or low-frequency settings (like default download/storage paths) into a dedicated Settings view.

  * Never place multiple redundant entry points (e.g., a path dropdown + a folder manager button + a path settings button) for the same configuration on the primary workspace view.

### 3. Enforce CSS Box-Model, Border-Radius, and Hitbox Integrity (严守盒模型、圆角裁切与热区边界)

Validate every interactive container so child states never break parent geometry.

* **Clip child backgrounds and active indicator bars (防止子元素或左边框把圆角捅成直角)**:

  * When adding a left accent bar, badge, or `:hover` background inside a rounded card or pill, apply `overflow: hidden` on the parent container or match the child's `border-top-left-radius` and `border-bottom-left-radius` so rounded corners never turn into sharp right angles on hover.

* **Prevent card border clipping (防止外层容器裁切卡片圆角与边框)**:

  * Ensure scrollable list containers have sufficient padding (`padding: 2px` or `4px`) or proper box-sizing so child card borders and rounded corners are not sliced off at the edges.

* **Keep child controls inside row hover bounds (行内按钮严禁溢出 Hover 热区)**:

  * Ensure action buttons (`...`), pills, and switches inside table rows or list cards have heights and margins that fit strictly inside the parent row's `:hover` highlight box without overflowing top, bottom, or side borders.

* **Never mix native OS controls with custom themed UI (严禁混用未修饰的系统原生下拉框)**:

  * Do not leave unstyled native `<select>` elements inside a custom-styled dark or glassmorphism interface. Use a unified custom select component across all views.

* **Avoid cliché AI status pills (拒绝无实质意义的发光状态胶囊)**:

  * Do not clutter sidebars or bottom bars with glowing dot "All systems operational / 全部系统运行正常" status widgets unless the app genuinely monitors live background services and provides an anchored diagnostic breakdown on click.

### 4. Rationalize Interaction Flows, State Transitions, and Error Handling (理顺交互流转、缓存过渡与异常处理)

Design state transitions around user intent rather than lazy state bindings.

* **Gate unavailable actions contextually (缺失前置条件时做引导或隐藏，而非摆设无用按钮)**:

  * When a prerequisite is missing (e.g., no user account exists), show a single primary CTA to resolve it (`Add Account / 添加账号`) instead of rendering secondary action buttons that cannot function.

  * When an instance or item type does not support extensions (e.g., a pure Vanilla instance without a mod/shader loader), hide or disable the extension management cards or guide the user to install a loader first, rather than showing active management cards as if extensions are already supported.

* **Separate user validation from system crashes (严禁把普通前端校验包装成系统崩溃)**:

  * Missing user input (such as clicking "Start" before selecting an account) is a normal validation state, not a runtime exception. Guide the user inline or open the account selector directly.

  * Never pop up a failure dialog offering to `Export Error Log (导出错误日志)` for a simple missing selection.

* **Avoid redundant dual-control logic (杜绝“复选框 + 反向默认值下拉框”的左右脑互搏)**:

  * Never pair a boolean checkbox (`[x] Also install optional component / 同时安装某模组`) with an immediately adjacent dropdown whose default option is `Do not install component (不安装该模组)`.

  * Use a single control (either a single dropdown with `None` + options, or a checkbox that conditionally renders the version/mode selector only when checked).

* **Anchor popovers to their trigger and sync error logs (浮层就近锚定，异常必须与通知队列同步)**:

  * Clicking a status indicator in the bottom-left corner must not open an unanchored notification drawer in the top-right corner.

  * Never position two different floating panels (such as `Notifications / 通知` and `Update History / 更新历史`) at the exact same screen coordinates where they overlap.

  * If an indicator claims `Recent error occurred (最近出现异常)` and opens a notification drawer on click, ensure the error handler actually pushes the error record into that notification list.

* **Use clean loading transitions (切页与筛选过渡严禁残留不可点的旧列表)**:

  * When switching tabs or updating filter criteria, either swap immediately once ready or display a clean skeleton/spinner over the container.

  * Never leave the previous tab's stale DOM items visible and unclickable (`pointer-events: none`) underneath a text banner saying `Updating conditions, temporarily showing previous results... (正在更新条件，暂时显示上次结果...)`.


## Quick Audit Checklist (快速自检清单)

* \[ \] **Copywriting**: Are there any defensive explanations, redundant subtitles, bare "Import/Select" buttons, or leaked debug items?

* \[ \] **Layout Reuse**: Do all peer list/resource pages share one header component with the "Refresh" button in the exact same spot?

* \[ \] **Spacing & Alignment**: Do all controls on the same row have the exact same pixel height, and do all stacked controls have a non-zero `gap`?

* \[ \] **Border-Radius & Hitboxes**: Does hovering any item keep its rounded corners intact (`overflow: hidden`) and keep child buttons inside the hover highlight box?

* \[ \] **State & Errors**: Are missing prerequisites handled via inline guidance rather than crash logs, and do tab switches clear stale unclickable content cleanly?