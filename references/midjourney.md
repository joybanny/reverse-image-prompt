# Midjourney Prompting Reference

Use Midjourney prompts as compact visual keyword strings plus parameters. Write the descriptive prompt first and put parameters at the end.

## Core Shape

```text
[subject], [action/pose], [environment], [medium/style], [lighting], [color palette], [composition/camera], [mood/details] --ar [ratio] --s [stylize] --raw --no [unwanted items]
```

中文释义格式：

```text
[主体]，[动作/姿态]，[环境]，[媒介/风格]，[光照]，[色彩]，[构图/镜头]，[情绪/细节]。参数：保留 --ar、--s、--raw、--no 等原始参数名，并用中文简短解释关键参数作用。
```

Use English for Midjourney prompts by default unless the user explicitly requests Chinese. English usually maps more directly to common Midjourney prompt conventions.

Whenever producing a Midjourney prompt, include a Chinese translation/interpretation directly after the English prompt. The English prompt is the copyable MJ command; the Chinese version is for user understanding. Translate descriptive tokens into natural Chinese, but keep Midjourney parameters such as `--ar`, `--s`, `--raw`, `--no`, `--iw`, `--sref`, and `--sw` in their original form. Briefly explain important parameters in Chinese when helpful.

## Descriptive Tokens

Prioritize these visual dimensions:

- Subject: concrete noun plus defining traits.
- Scene/environment: where it is and how dense the background is.
- Medium: photo, 3D render, watercolor, ink illustration, product photography, cinematic still, concept art.
- Era/culture cue: only if visible or requested.
- Camera/composition: close-up, centered, isometric, top-down, 45-degree view, macro, full body, negative space.
- Lighting: softbox, rim light, volumetric light, golden hour, studio lighting, high contrast.
- Palette: muted, monochrome, jewel tones, teal and gold, warm neutrals, high saturation.
- Mood: serene, ominous, playful, luxurious, technical, heroic.
- Detail control: clean silhouette, readable shape, intricate engravings, minimal background.
- Human face control: for portraits, avatars, character design, people photography, and model shots, include positive tokens such as `clear unobstructed face`, `natural facial features`, `expressive eyes`, `defined expression`, or `sharp facial details` when the face is visible and unobstructed. Add concrete facial tokens when observable: `oval face`, `soft eyebrows`, `eyes looking at camera`, `natural nose bridge`, `slight smile`, `calm expression`, `direct gaze`. If the reference visibly has occlusion, describe it directly as a visual token, such as `face partially covered by hair`, `lower face covered by scarf`, `face covered by a square block`, or `back-facing figure, face not visible`. Do not replace this with evasive wording like `face is not the focus`.

## Parameters

- `--ar`: aspect ratio. Use `--ar 1:1` for icons, square assets, avatars; `--ar 16:9` for wide scenes; `--ar 9:16` for vertical posters; `--ar 4:5` for social/product portrait crops.
- `--s`: stylize strength. Lower values follow the prompt more plainly; higher values add stronger aesthetic interpretation.
- `--raw`: use when prompt adherence and less default beautification matter.
- `--no`: list unwanted elements, such as `text, watermark, logo, extra objects, cropped subject`.
- `--chaos`: use only when the user wants exploratory variety.
- `--weird`: use only when the user wants unusual or uncanny outcomes.
- `--iw`: use with image prompts to control image-reference influence.
- `--sref` and `--sw`: use for style reference when the user supplies or requests a style reference.
- Character/object reference parameters can be suggested when the user wants a consistent person, mascot, or object across images, but do not invent reference URLs.

Do not claim parameter availability for a specific Midjourney version unless verified in the current context. If the user needs current version-specific behavior, verify official docs first.

## Version 8.1 Prompt Constraints

When the target prompt uses `--version 8.1` or the user asks for Midjourney V8.1, do not use multiple text prompts or `::` prompt-weight syntax. V8.1 prompts should be written as one continuous descriptive text prompt followed by parameters.

Do not write V8.1 prompts like this:

```text
crystal sword::2 enchanted ice aura::1 dark clean game icon background::0.7 --version 8.1 --ar 1:1
```

Write V8.1 prompts like this instead:

```text
ice-blue translucent crystal sword as the primary subject, enchanted ice aura, clean dark game icon background, centered composition, crisp silhouette --version 8.1 --ar 1:1 --s 100 --raw --no text, watermark, logo
```

For V8.1 priority control, use wording and order instead of `::` weights:

- Put the most important subject first.
- Use phrases such as `primary subject`, `strong emphasis on`, `subtle background`, `secondary detail`, or `minimal supporting elements`.
- Repeat a critical attribute once only if it is essential, such as `clear unobstructed face` for portraits.
- Keep the prompt as a single comma-separated or sentence-like description.

If the user explicitly requests `::` weights, only provide them as a non-V8.1 / legacy alternative and label that they should not be used with `--version 8.1`.

## Negative Prompting

Use `--no` instead of prose such as `please do not`. Keep the list concrete and comma-separated.

Do not add `face`, `clear face`, `facial details`, `recognizable face`, or similar terms to `--no` for a main human subject. That suppresses face clarity and creates the unwanted `脸部不要清晰呈现` behavior.

Do not use indirect negative wording such as `--no face focus` or `--no censor block` when the reference image visibly has occlusion. State the occlusion positively in the descriptive prompt if it should be preserved. Use `--no censor block, mosaic, face covering` only when the user explicitly asks to remove those occluders.

Good:

```text
--no text, watermark, logo, extra hands, cropped subject
```

Risky:

```text
--no bad, ugly, low quality
```

## Platform Style Differences

Convert GPT Image briefs into Midjourney by:

1. Removing long instructional phrases.
2. Keeping the most visual nouns and modifiers.
3. Moving output rules into parameters.
4. Moving unwanted elements into `--no`.
5. Keeping composition, lighting, palette, and medium as compact tokens.
