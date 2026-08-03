# Seedance Prompting Reference

Use Seedance prompts as clear Chinese directing instructions. The target is a video, so describe both the spatial layer (subject, setting, visual style) and the temporal layer (what changes, in what order, and how the camera follows it).

This reference follows the Doubao Seedance 2.0 official prompting guide (updated 2026-06-08): https://www.volcengine.com/docs/82379/2222480

## Choose the Task Type

Select one task type before drafting. Do not blur task types in the opening sentence.

- Reference generation: extract selected elements from supplied material and generate a new video. Write `参考图片1中的[主体/风格]，生成……`, `参考视频1中的[动作/运镜/音效]，生成……`, or `参考音频1中的音色，生成……`.
- Video editing: modify an existing video while preserving unspecified content. Write `严格编辑视频1，将其中的[原特征]修改为[新特征]`.
- Video extension: continue an existing video. Write `向前/向后延长视频1，生成……`.
- Combined task: write `参考图片1中的[参考维度]，严格编辑视频1，[具体编辑内容]`.

For editing and extension, refer to the source as `视频N`, never `参考视频N`; the latter may be interpreted as a reference-generation task.

## Core Formula

```text
精准主体 + 动作细节 + 场景环境 + 光影色调 + 镜头运镜 + 视觉风格 + 画质 + 约束条件
```

For multi-shot video, build the prompt in chronological order. Each shot should normally contain one camera movement only.

```text
镜头1：[景别/运镜]，[主体]在[场景]中[具体连续动作]，[表情或空间变化]，<音效>。
镜头2：……
整体：[风格、色调、画质]；[稳定性与排除项]。
```

Do not force exact durations such as `0-3 秒`; describe shot order and let the model determine a natural rhythm.

## Reference Binding

- Name the material precisely: `图片1`、`视频1`、`音频1`.
- If several subjects appear, define them with 2-3 stable visual features: `将图片1中穿红色连衣裙、戴草帽的女人定义为主角`.
- Continue using the same defined label. For a simple undefined subject, bind it to the source each time: `女孩@图片1`.
- Do not replace `图片N/视频N` with an Asset ID in the text prompt.
- Prefer a small, purposeful material set: 1-2 character images, 1 environment image, 1 camera-reference video, and optionally 1 audio reference. Too many materials can create priority conflicts.

## Actions, Camera, Audio, and Text

- Describe actions with body part, magnitude, speed, and transition: `缓慢抬手，借着转身惯性顺势把手抬至胸前`.
- Prefer continuous, controllable motion over violent, high-amplitude action when stability matters.
- Externalize emotion through visible behavior rather than abstract labels: write `肩膀微颤、眼眶泛红、攥紧衣角`, not only `很悲伤`.
- Use standard camera terms directly: `全景缓慢推近`、`中景平稳跟拍`、`固定机位`、`特写`、`平稳横移`.
- Mark music with `（）`, sound effects with `<>`, dialogue with `{}`, and subtitles with `【】`.
- Keep dialogue in one language except for proper nouns. For non-Chinese/non-English dialogue, state the language before the braces.

## Constraints and Reliability

Place quality, style, and exclusions in a final overall sentence:

```text
整体为[主视觉风格]，[色调与光影]，高清电影质感；人物面部稳定不变形，动作自然流畅，无卡顿无闪烁；保持无字幕，不要生成任何文字、Logo或水印。
```

- If text is wanted, give its exact content, timing, position, appearance method, and visual style.
- Use `保持无字幕` / `避免生成任何文字或字幕` only when text is unwanted.
- State a desired 2D/3D/realistic style explicitly to reduce style drift.
- For character identity stability, use a clean face close-up and a separate full-body image; make the face reference appear first in the prompt.
- If more than four referenced people are needed, generate grouped images first, then use those images as video references.

## Output Template

```text
[任务类型与素材引用]
将图片1中[稳定视觉特征]的[人物/物体]定义为[主体名称]。
镜头1：[景别/运镜]，[主体名称]在[场景]中[具体动作、表情、空间变化]，<音效>。
镜头2：[景别/运镜]，[后续动作与叙事变化]，{台词}。
整体为[风格]，[色调与光影]，高清电影质感；[角色/动作稳定性约束]；[无字幕/无文字/无Logo/无水印等约束]。
```
