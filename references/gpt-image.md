# GPT Image Prompting Reference

Use GPT Image prompts as production briefs. Write clear instructions in natural language with explicit task, subject, visual details, constraints, and output requirements.

## Field Order

Use this order unless the user asks for a different format:

1. 任务: what image to generate or edit, and what it is for.
2. 主体: the main object/person/scene and its defining visual traits.
3. 风格: one dominant style or rendering mode.
4. 构图: framing, view angle, placement, subject scale, crop safety, negative space.
5. 材质与细节: materials, texture, surface details, decorations, wear, sharpness.
6. 光照与色彩: lighting setup, contrast, palette, mood.
7. 背景: background type and complexity.
8. 限制: concrete unwanted items.
9. 输出: aspect ratio, size, transparency/background needs, quality target.

## Writing Principles

- Prefer precise visual language over vague adjectives such as `高级`, `好看`, `酷`.
- Translate abstract goals into visible causes: premium because of clean lighting, refined materials, balanced spacing, controlled palette.
- Keep one main style direction. Add secondary modifiers only if they support the main direction.
- For production assets, specify completeness and crop safety: `主体完整显示`, `不裁切`, `四周保留安全边距`.
- For icons, specify centered composition and subject scale, often 70%-85% of canvas unless the user says otherwise.
- For ecommerce/product images, prioritize accurate product shape, clean background, realistic lighting, and no extra props unless requested.
- For posters, reserve readable negative space for later typography instead of asking the model to generate uncontrolled text.
- For edits, clearly separate `保留` and `修改`.
- For clean, readable, production-oriented GPT Image prompts, include this sentence verbatim as a complete output requirement instead of splitting it into separate negative constraints: `整体画面必须干净、平滑、统一，强调大色块叙事与整体轮廓，不要细碎噪点，不要高频纹理，不要脏污颗粒，不要密集小装饰，边缘清晰利落，表面干净，画面呼吸感强，一目了然。`
- For portraits, avatars, character design, people photography, and model shots, default to `面部清晰`, `五官自然`, `表情明确`, and `眼神自然` unless the user asks for anonymity or the source image visibly shows occlusion. When the face is visible and unobstructed, describe facial details concretely in `主体`: face shape, eyebrow shape, eye shape or gaze, nose bridge, mouth/lip state, expression, and gaze direction. Example: `面部无遮挡，椭圆脸，眉形柔和，眼睛看向镜头，鼻梁自然，嘴角轻微上扬，表情平静自然`.
- If the reference image visibly shows face occlusion, describe it as a positive visual fact in `主体` or `构图`, such as `面部局部被发丝遮挡`, `下半张脸被围巾遮挡`, or `脸部有方块遮挡`. Do not convert it into `不要复现遮挡方块` or `面部不是画面重点`.
- Preserve visible occlusion when reverse-engineering a reference image. Move it to `修改` or `限制` only when the user explicitly asks to remove, restore, clean up, or make the face unobstructed.
- Do not soften privacy risk by adding `脸部不要清晰呈现` or similar face-obscuring language unless it is part of the user's intent.

## Negative Constraints

Use natural-language constraints:

- 不要文字
- 不要水印
- 不要 logo
- 不要多余物体
- 不要裁切主体
- 不要复杂背景
- 不要低清晰度
- 不要变形

Do not include `不要清晰呈现脸部`, `模糊面部`, `不要可辨认五官`, `面部不是画面重点`, `不复现遮挡方块`, or similar indirect face/occlusion wording for a main human subject unless explicitly requested.

If the reference image has a visible face occluder, write it directly as an observed feature (`脸部有方块遮挡`, `面部被手部遮挡`) instead of turning it into a negative constraint. If the user wants the occluder removed, write a clear edit instruction: `移除遮挡物，使面部完整清晰可见`.

Avoid broad constraints such as `不要丑`; convert them to visible failures.

## Output Template

```text
任务：生成一张用于[用途]的图像。
主体：[主体和关键特征]
风格：[一个主风格]
构图：[主体位置、视角、占比、裁切、安全边距]
材质与细节：[材质、纹理、装饰、清晰度]
光照与色彩：[光照、对比、色彩]
背景：[背景复杂度和类型]
整体要求：整体画面必须干净、平滑、统一，强调大色块叙事与整体轮廓，不要细碎噪点，不要高频纹理，不要脏污颗粒，不要密集小装饰，边缘清晰利落，表面干净，画面呼吸感强，一目了然。
限制：不要[文字/水印/logo/多余元素/裁切/变形]。
输出：[比例/尺寸/背景/质量目标]
```

## Edit Template

```text
基于参考图进行编辑。
保留：[主体形状、姿态、构图、关键身份特征或产品特征]
修改：[背景、材质、颜色、光照、风格、服装或局部元素]
风格目标：[目标风格]
结果要求：整体自然一致，看不出明显拼接。
限制：不要改变[必须保留项]，不要添加无关元素，不要文字或水印。
```
