---
name: reverse-image-prompt
description: Reverse-engineer image and video-generation prompts from user descriptions, uploaded images, screenshots, drafts, or existing prompts. Use when the user asks to 反推提示词, 看图写提示词, 改写/优化图像或视频 prompt, generate GPT Image, Midjourney, or Seedance prompts, convert between platform prompt styles, or produce prompt variants.
---

# Reverse Image Prompt

## Core Purpose

Turn a visual target into usable image- or video-generation prompts. Support both text-only briefs and image-based reverse prompting. Produce platform-specific outputs for GPT Image, Midjourney, and Seedance while clearly separating visible facts, inferred intent, and optional creative additions.

Do not generate an image unless the user explicitly asks. This skill writes prompts and iteration guidance.

## Input Decision

1. If the user provides an image, inspect the image first. Record only visible facts before making style or intent inferences.
2. If the user provides a text description, extract the target fields from the text before asking questions.
3. If the user provides both image and text, treat the image as the visual reference and the text as the desired change or output intent.
4. If an image path is provided but the environment cannot inspect it, ask the user to upload the image or use an available image-inspection tool before reverse prompting. For Midjourney, if the supplied text already describes the target sufficiently, use that text directly without requiring the inaccessible image; do not infer its unseen contents.
5. If the target platform is missing, default to Seedance for an explicitly video-oriented request; otherwise output both GPT Image and Midjourney versions.

## Conversation Workflow

Use a short, practical dialogue. Avoid interrogating the user when enough information exists to produce a useful first draft.

1. Identify the output target: GPT Image, Midjourney, Seedance, or a requested combination. If the user asks for video, default to Seedance; otherwise, if no target is given, default to GPT Image and Midjourney.
2. Extract or observe the visual core:
   - Subject and key attributes
   - Purpose or image type, such as game icon, ecommerce product, poster, character design, UI asset, concept art, product photography
   - Style, medium, rendering mode, and realism level
   - Composition, camera/view angle, framing, subject scale, crop safety
   - Materials, texture, lighting, color palette
   - Background, environment, mood, era, and visual hierarchy
   - Text/logo/watermark presence and unwanted elements
   - Output ratio, size, quality target, and transparency/background needs
3. Ask at most one focused clarifying question if a missing choice materially changes the prompt. Otherwise make a labeled assumption.
4. Produce a prompt package using the output structure in `references/output-patterns.md`.
5. Offer concise iteration controls: what to change if the result is too busy, too generic, poorly framed, off-style, or contains text/watermarks.

## Image Reverse Prompting Rules

- Separate `可见事实` from `风格推测` and `创作补充`.
- Do not invent hidden details, brands, exact artists, dates, or named IP unless visible or supplied by the user.
- Describe style through visual properties rather than unsupported attribution: lighting, palette, medium, camera, material, brushwork, rendering, layout.
- Preserve important composition facts from the image: subject placement, viewpoint, crop, negative space, background density, relative scale.
- Call out uncertainty with `可能` or `不确定` instead of presenting guesses as facts.
- If the image contains people, avoid identity claims unless the user supplies identity context.
- Do not add constraints such as `脸部不要清晰呈现`, `模糊脸部`, `face not clearly visible`, or `obscured face` by default. Use them only when the user requests anonymity, the person is background-only, or the source image visibly has an obscured/unclear face.
- For portraits, avatars, character design, model shots, and any image where the person is the main subject, preserve or request clear facial structure, natural features, and an intentional expression while still avoiding identity claims. When the face is visible and unobstructed, explicitly describe observable facial features and expression: face shape, eyebrows, eyes, nose bridge, lips/mouth, gaze direction, and expression. If a feature is not visible enough, mark it as `不确定` instead of omitting the whole face description.
- Use positive, literal wording for visible face state. Do not write evasive phrases such as `面部不是画面重点` or `不复现遮挡方块`. If the reference image has occlusion, state the visible fact directly, for example `面部局部被发丝遮挡`, `眼部被阴影遮挡`, `脸部有方块遮挡`, or `人物背对镜头，面部不可见`.
- Treat occlusion as an observed visual fact, not as a negative constraint. Preserve it in the prompt when the user asks to reproduce or reverse-engineer the reference; remove it only when the user explicitly asks to clean up, restore, or make the face unobstructed.
- If the image contains text, transcribe only text that is legible; otherwise say it is illegible or approximate.

## Platform Routing

Load references only as needed:

- Use `references/gpt-image.md` when writing GPT Image prompts or converting to a production-brief style.
- Use `references/midjourney.md` when writing Midjourney prompts or converting to keyword/parameter style. Every Midjourney prompt must be a self-contained text-to-image prompt: translate observed reference features into text, and omit image links, asset placeholders, reference-dependent wording, and image/style/character reference parameters. This also applies when rewriting existing prompts and giving iteration advice.
- Use `references/seedance.md` when writing Seedance video prompts, including reference-material binding, video editing, or extension prompts.
- Use `references/output-patterns.md` for final answer structure and reusable templates.

## Quality Bar

A good result should be immediately copyable, visually specific, and editable. It should include enough constraints to reduce common failures without overloading the model with conflicting style directions.

Before finalizing, check:

- The subject is concrete and visually described.
- The purpose/platform is reflected in the prompt style.
- There is one dominant style direction.
- Composition and subject scale are explicit.
- Lighting, material, palette, and background are not vague filler.
- Negative constraints are specific.
- GPT Image, Midjourney, and Seedance versions are not identical; each follows its platform style.
- For each Midjourney command, verify that it can be used without attaching reference images and that the complete command is at most 900 characters, including spaces, punctuation, and parameters. See `references/midjourney.md` for the length budget and compression priorities.
