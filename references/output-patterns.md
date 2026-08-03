# Output Patterns

Use these patterns when responding to users. Keep the answer copyable and compact.

## Full Prompt Package

```markdown
**视觉拆解**
可见事实：[only visible or supplied facts]
风格推测：[labeled inferences]
关键缺口：[missing choices or assumptions]

**GPT Image 版**
```text
[production-brief prompt]
```

**Midjourney 版**
```text
[keyword prompt + parameters]
```

**Midjourney 中文释义**
```text
[MJ 描述性提示词的中文翻译/释义。保留 --ar、--s、--raw、--no 等参数原文，并用中文简短解释关键参数作用。]
```

**Seedance 版**
```text
[按镜头时序组织的中文视频提示词；如有素材，明确使用图片1/视频1/音频1指代。]
```

**可调方向**
- 更接近原图：[one concrete edit]
- 更适合生成：[one concrete edit]
- 常见失败限制：[negative constraints]
```

## Minimal Answer

Use when the user asks for direct prompt only:

```markdown
**GPT Image**
```text
...
```

**Midjourney**
```text
...
```

**Midjourney 中文释义**
```text
...
```

**Seedance**
```text
...
```
```

## If Information Is Missing

Ask one question only when needed:

```text
你希望这张图主要用于哪个场景：游戏图标、电商产品图、海报、角色设定，还是只做风格参考？
```

If the answer is not required, proceed with an assumption:

```text
我先按“游戏图标”处理，因为画面主体居中、背景干净、强调轮廓可读性。
```

## Iteration Advice

Map output problems to prompt edits:

- 主体太小: increase subject scale, centered composition, safe margin only.
- 主体被裁切: add complete subject visible, uncropped, full silhouette.
- 画面太乱: simplify background, remove extra props, clean silhouette.
- 风格跑偏: reduce secondary styles, name one dominant medium.
- 文字乱码: add no text/watermark/logo; for Midjourney use `--no text, letters, watermark, logo`.
- 细节过密: reduce ornaments, prioritize readable shape.
- 不像参考图: increase preservation language for GPT Image, or suggest image prompt/reference influence for Midjourney.

## Example: Game Icon

**GPT Image**
```text
任务：生成一张 1024x1024 游戏道具图标。
主体：一把冰蓝色半透明水晶长剑，银色护手，剑身边缘有冷色微光。
风格：高清 3D 游戏图标。
构图：主体严格居中，占画面约 80%，完整显示，不裁切，四周保留安全边距。
材质与细节：水晶材质通透，金属护手有细密雕纹，边缘清晰。
光照与色彩：冷色轮廓光，蓝白主色，轻微高光。
背景：深色干净背景，突出主体。
限制：不要文字，不要水印，不要其他武器，不要复杂场景。
输出：1:1 方图，高精度，适合游戏背包图标。
```

**Midjourney**
```text
ice-blue translucent crystal longsword, silver engraved guard, glowing cold edges, centered game item icon, clean dark background, high-detail 3D render, crisp silhouette, rim lighting, readable shape --ar 1:1 --s 100 --raw --no text, watermark, logo, extra weapons, cropped subject
```

**Midjourney 中文释义**
```text
冰蓝色半透明水晶长剑，银色雕纹护手，剑身边缘带冷色微光，居中的游戏道具图标，深色干净背景，高细节 3D 渲染，轮廓清晰，轮廓光，可读性强。参数：--ar 1:1 为方图，--s 100 为中等风格化，--raw 强化提示词遵循，--no 排除文字、水印、logo、额外武器和主体裁切。
```
