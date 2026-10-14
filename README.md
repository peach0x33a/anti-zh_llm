# @0x33a/anti-zh_llm

去除前端 UI/UX 和中文产品文案中的 AI 味。适用于开发、重构和审查网页、桌面应用及交互文案。

完整规范见 [SKILL.md](SKILL.md)，包括：

- 删除防御性解释、空洞副标题和含糊的操作文案。
- 复用页面布局，统一控件尺寸与间距。
- 修复圆角裁切、盒模型和交互热区。
- 理顺前置条件、加载状态、通知与错误处理。

## 全局安装

对于支持 `~/.agents/skills` 的工具：

```bash
git clone https://github.com/peach0x33a/anti-zh_llm.git ~/.agents/skills/@0x33a/anti-zh_llm
```

也可以直接安装到 Codex 的全局 skills 目录：

```bash
git clone https://github.com/peach0x33a/anti-zh_llm.git ~/.codex/skills/@0x33a/anti-zh_llm
```

选择一种安装方式即可。下一轮对话可使用 `@0x33a/anti-zh_llm`，或直接提出适用的界面与文案任务。
