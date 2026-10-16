# Midjourney Prompting Reference

Use Midjourney prompts as self-contained text-to-image descriptions plus necessary parameters. Write concrete visual phrases or short sentences, then put parameters at the end.

## Standalone Text-to-Image

An image may be inspected to understand the visual target, but the resulting Midjourney command must describe that target in words and work without any attached image.

- Describe the subject, defining visible traits, pose, framing, composition, medium, lighting, palette, and relevant background directly. Do not write `as in the reference image`, `same character as image 1`, `参考图片1`, or similar dependencies.
- Do not include image URLs, local image paths, attachment/asset IDs, or image placeholders in the copyable command.
- Do not emit image/style/character/object reference controls, including `--iw`, `--sref`, `--sw`, `--sv`, `--cref`, `--cw`, `--oref`, `--ow`, or `--edit`. This is a restriction of this skill's output mode, not a claim that Midjourney lacks these features.
- When rewriting an existing prompt, remove reference links and reference controls even if they are already present. Preserve visual information stated in the text or actually observed; never invent what an inaccessible reference contains.
- If the needed visual information exists only in an image that cannot be inspected, request the image or a description before reverse prompting. If the supplied text already specifies the target sufficiently, use it without requiring that image.
- Keep later variants and iteration suggestions in the same standalone mode. Improve resemblance through concrete visual descriptions, not by recommending image upload or stronger reference weights.

## Length Budget

These are this skill's editing limits, not an official Midjourney maximum or a proven optimal prompt length for every version.

- Aim for 60-120 English words in the descriptive body; a complex visual target may use up to about 150 words. These are flexible planning ranges: do not pad a simple prompt to reach a minimum or delete essential details merely to hit a word target.
- The hard limit is **900 characters for the complete copyable Midjourney command**, including spaces, punctuation, and every parameter/value. It applies to every variant and every iteration. Keep the command on one line. An `/imagine` prefix, if requested, counts too.
- Count body words by whitespace-separated tokens before the first parameter; a hyphenated expression counts as one token. Parameters are excluded from this approximate word count, but included in the character limit.
- Chinese explanations, translations, headings, and length notes stay outside the command and are not counted. When the user requests a Chinese command, the 900-character limit still applies to that command.
- Draft the complete command, count it, and compress before returning it if it exceeds 900 characters. Use an available string-length check when needed; do not call a prompt compliant based only on its approximate word count.

Compress in this order:

1. Delete filler, quality slogans, repeated synonyms, duplicated face/style instructions, and nonvisual storytelling.
2. Combine related details into short phrases or sentences. Keep attributes next to the subject they describe.
3. Remove optional secondary decoration and unnecessary parameters; keep `--no` lists short and specific.
4. Preserve the user's essential subject/count, visible defining traits, pose, framing, spatial relationships, focal point, medium, key material, lighting, and palette. Preserve intentional crop or occlusion instead of adding contradictory completeness rules.

Do not cut off the tail of a prompt to meet the limit. If all user-mandated details cannot fit after compression, state the conflict briefly outside the command and ask which details to prioritize; do not silently drop them or claim full fidelity.

Research basis checked on 2026-10-13: [Prompt Basics](https://docs.midjourney.com/hc/en-us/articles/32023408776205-Prompt-Basics) advises concise, specific descriptions and explains that fewer details reduce control. [Describe](https://docs.midjourney.com/hc/en-us/articles/32497889043981-Describe) explicitly supports longer, more detailed prompts for V8.1/V8.2. The word ranges and 900-character budget above are local output rules, not numbers prescribed by those pages.

## Core Shape

```text
[subject], [action/pose], [environment], [medium/style], [lighting], [color palette], [composition/camera], [mood/details] --ar [ratio] --s [stylize] --raw --no [unwanted items]
```

中文释义格式：

```text
[主体]，[动作/姿态]，[环境]，[媒介/风格]，[光照]，[色彩]，[构图/镜头]，[情绪/细节]。参数：保留 --ar、--s、--raw、--no 等原始参数名，并用中文简短解释关键参数作用。
```

Use English for Midjourney prompts by default unless the user explicitly requests Chinese. English usually maps more directly to common Midjourney prompt conventions.

By default, include a Chinese translation/interpretation directly after the English prompt, unless the user requests English only or no explanation. The English prompt is the copyable MJ command; the Chinese version is for understanding and stays outside that command. Translate descriptive phrases into natural Chinese, keep emitted parameters such as `--ar`, `--s`, `--raw`, and `--no` in their original form, and briefly explain important parameters when helpful. Translate the final compressed prompt without reintroducing removed references or details.

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
- Use only parameters that do not require external reference material. For visual consistency, repeat stable descriptive traits in words; follow the standalone rules above in the prompt, translation, and iteration advice.

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
5. Keeping composition, lighting, palette, and medium as compact phrases or short sentences.
6. Replacing reference-dependent instructions with observed or supplied visual descriptions and removing all reference links and controls.
7. Counting the final complete command and compressing it to 900 characters or fewer.
