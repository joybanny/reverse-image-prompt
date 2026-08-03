# Reverse Image Prompt

从图片或文字描述反推图像/视频生成提示词，输出 GPT Image、Midjourney、Seedance 三个平台版本。可用于看图写提示词、改写/优化图像或视频 prompt、跨平台风格转换、生成 prompt 变体。

## 功能 / Features

- **双输入模式**：图片输入先记录可见事实，再做风格与意图推测；文字描述直接提取目标字段
- **平台化输出**：GPT Image 生产级指令式 prompt、Midjourney 关键词 + 参数式 prompt、Seedance 视频 prompt（参考生成 / 编辑 / 延展）
- **事实分层**：严格区分「可见事实 / 风格推测 / 创作补充」，不编造不可见细节、品牌、艺术家、日期或 IP
- **人脸处理**：肖像等主画面默认保留清晰五官与自然表情，不做模糊脸部等回避式约束
- **迭代控制**：内置过满、过泛、构图不佳、风格偏移、文字/水印等问题的调整建议
- **可复制输出**：按 `references/output-patterns.md` 模板输出，答案可直接复制使用

## 结构 / Structure

| 文件 | 作用 |
| --- | --- |
| `SKILL.md` | 技能主入口：输入决策、对话流程、平台路由、质量检查 |
| `agents/openai.yaml` | Codex agent 界面配置（显示名、默认提示词） |
| `references/gpt-image.md` | GPT Image 生产简报风格 prompt 写法 |
| `references/midjourney.md` | Midjourney 关键词与参数风格写法 |
| `references/seedance.md` | Seedance 视频 prompt（参考生成 / 编辑 / 延展） |
| `references/output-patterns.md` | 最终答案结构与可复用模板 |

## 使用 / Usage

作为 Codex skill 安装后，当用户请求「反推提示词 / 看图写提示词 / 改写优化图像或视频 prompt / 生成 GPT Image、Midjourney 或 Seedance 提示词」时自动触发。本技能只写提示词与迭代指导，不主动生成图片。

## 默认规则 / Defaults

- 未指定目标平台时：视频类需求默认 Seedance，其他默认同时输出 GPT Image 与 Midjourney 版本
- 图片与文字同时提供时：图片作为视觉参考，文字作为期望变更或输出意图
- 环境无法查看图片时：先请用户上传图片或使用可用的图片检查工具，再开始反推