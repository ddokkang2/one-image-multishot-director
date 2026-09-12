---
name: one-image-multishot-director
description: "Use when drafting Seedance 2.5 four-shot prompts."
version: 1.0.0
author: DIO + Hermes
license: MIT
metadata:
  hermes:
    tags: [seedance, video-generation, multishot, image-to-video]
    related_skills: [seedance-clean, seedance-pipeline, seedance-camera]
---

# Seedance 2.5 One-Image Multi-Shot Director

This is an independent Seedance 2.5 directing skill. It is separate from STORM, Notion workflows, and project-specific prompt systems. Do not import STORM structure.

The user provides one reference image, `@image1`, plus a short concept, genre, mood, or action. Turn that input into a 15–30 second short-form mood-film plan and four copy-ready Seedance 2.5 prompts. Explain the direction in Korean; write the prompts in English for direct pasting into Seedance.

## Core principles

### 1. Visual analysis and three-direction onboarding

When the user uploads only an image or gives an unclear concept:

1. Summarize the visible subject, environment, lighting, and optical feeling in two or three Korean lines.
2. Propose three directions with different genres or moods that are likely to work well with the image.
3. Ask the user to choose a number or add an environmental direction such as rain, fog, smoke, neon, golden-hour light, or dust.

Do not write final prompts until the user selects a direction or supplies a sufficiently specific concept.

### 2. Visual Anchor Lock

Extract and preserve these constants across all four shots:

- subject identity and recognizable facial features
- basic hairstyle and wardrobe silhouette
- important colors and visible accessories
- environment geometry and spatial landmarks
- lighting direction and color temperature
- lens feeling and camera distance when visible

Use `@image1` for identity and appearance. Keep the written character description short and action-focused so it does not conflict with the reference image.

### 3. Safe Override Policy

Keep local identity-sensitive details stable. Do not redesign or locally mutate the face, hands, fingers, fine accessories, or wardrobe construction.

Allow overrides at the environment level:

- rain, snow, fog, smoke, dust, haze, or atmospheric particles
- lighting mood such as neon, golden hour, rim light, or moonlight
- background color temperature and exposure mood

State the applied environmental override explicitly. If none is requested, write `None`.

### 4. Four-shot drift defense

Use a default 30-second sequence with four shots:

- Shot 1: 0–5 seconds, atmosphere and establishing frame
- Shot 2: 5–12 seconds, main mood, emotion, or performance
- Shot 3: 12–22 seconds, macro insert detail
- Shot 4: 22–30 seconds, climax and hero ending

Shot 3 must be an insert shot focused on a hand, prop, foot, texture, surface, or environment detail. Keep the face out of the insert whenever possible. This creates a deliberate visual breathing point and helps hide small identity differences between face-led shots.

Use simple physical actions. Prefer one clear action per shot. Avoid intricate finger choreography, complex fights, impossible body movement, and abrupt multi-axis camera movement.

## Situation A: image-only or unclear concept

Return exactly this structure in Korean:

### Step 1: Visual Summary

Summarize the subject and visible wardrobe, background space, lighting and color temperature, and lens or optical feeling. Keep it concise and based only on what is visible.

### Step 2: Three Direction Options

Offer three numbered options. Each option includes a genre or format, mood, visual treatment, and why the reference image is a good fit. Use concrete descriptions rather than vague words such as beautiful, cool, epic, or cinematic.

End with:

> 원하는 번호를 선택하거나, 비·안개·연기·야간 조명처럼 추가하고 싶은 환경 연출을 말씀해주세요.

Do not output final Seedance prompts yet.

## Situation B: genre and concept are defined

Return exactly these three stages.

### Step 1: Visual Anchor & Safe Override

Write in Korean:

- **Subject Anchor:** fixed subject identity, visible appearance, wardrobe silhouette, and action-critical details
- **Environment Anchor:** fixed location geometry, foreground/midground/background, and visible landmarks
- **Lighting Anchor:** fixed source direction, color temperature, and exposure mood
- **Applied Safe Override:** environment or lighting changes; write `None` when unused

### Step 2: Four-Shot Timeline Table

Use a Markdown table with these columns:

| 샷 | 시간 | 샷 유형 | 카메라 무빙 | 화면에서 일어나는 일 | 연출 의도 |
|---|---:|---|---|---|---|

Use the default timing of 0–5s, 5–12s, 12–22s, and 22–30s unless the user requests another duration. Explain the timeline in Korean so a beginner can visualize it. Shot 3 must be a macro or insert detail and should avoid a face-led composition.

### Step 3: Seedance 2.5 Ready-to-Copy Prompts

Output four prompts, one for each shot. Each prompt must be pure English and ready to paste into Seedance 2.5. Put each prompt in its own code block with only the prompt inside.

Use this internal structure:

```text
[Shot type and camera movement], referenced from @image1. [Main subject motion and observable emotion]. [Key visual anchor elements]. [Lighting and color grade]. [Lens, film grain, and depth of field]. [Positive continuity locks].
```

Each prompt should contain a shot size and one primary camera movement, `referenced from @image1`, one clear subject action, fixed identity and environment anchors, lighting and color treatment, lens feeling, film grain and depth of field when useful, a positive continuity lock, `photorealistic, high fidelity` when photorealism is appropriate, and `clean frame, readable composition` when useful.

Use positive phrasing. Prefer `empty hands`, `stable facial identity`, `clean wardrobe silhouette`, and `stable geometry` over long negative lists. Use `no text` or `no captions` only when the user did not request text and the absence of text materially protects the shot. If the shot requires visible text, preserve the exact text supplied by the user and state it verbatim.

## Prompting rules

- Write what is visible, measurable, and physically observable.
- Replace mood-only words with actions, light behavior, posture, gaze, texture, and camera behavior.
- Keep one primary camera movement per shot.
- State the first-frame composition clearly.
- Keep foreground, midground, and background distinct.
- Describe emotion through facial muscle movement, eye-line, breath, posture, and timing.
- Keep the original reference image as the identity anchor for every shot.
- Use the same wardrobe, lighting direction, environment geometry, and prop state across the sequence.
- Use an insert shot to reduce face exposure and create rhythm, not as an accidental workaround.
- If the user specifies a different total duration, redistribute the four shots while preserving the same dramatic arc.
- If the user asks for a single continuous take instead of four shots, explain the trade-off and rewrite the timeline as one continuous shot.

## User manual

### Step 1: Choose a strong reference image

Recommend an image with:

- bust or medium framing, from chest or thighs upward
- at least 30% visible environment around the subject
- readable side light or rim light
- stable face, hair, and wardrobe
- simple hand position and uncluttered silhouette

Explain that extreme selfie close-ups, tangled fingers, flat fluorescent light, and cluttered backgrounds reduce motion and identity stability.

### Step 2: Use the onboarding flow

1. Upload one high-quality reference image as `@image1`.
2. Add a short concept, or ask for mood recommendations.
3. When the director proposes three directions, choose one and add any desired environmental override.
4. Receive the Korean anchor summary, four-shot timeline, and four English prompts.
5. Paste each shot prompt into Seedance 2.5 using the same original `@image1` reference.

### Step 3: Render each shot

Use the original high-quality reference image for every shot. Do not use a previous generated clip's last frame as the next shot's identity reference. Reusing compressed generated frames accumulates blur and identity drift.

Recommended render roles:

| 샷 | 추천 시간 | 이미지 설정 | 핵심 역할 |
|---|---:|---|---|
| Shot 1 | 5초 | 원본 `@image1` | 공간과 분위기 소개 |
| Shot 2 | 7–10초 | 원본 `@image1` | 표정·시선·주요 퍼포먼스 |
| Shot 3 | 7–10초 | 원본 `@image1` | 손·소품·발·질감·환경 인서트 |
| Shot 4 | 5–8초 | 원본 `@image1` | 클라이맥스와 아웃트로 |

### Step 4: Assemble the final short

Use an editor such as CapCut to place the four clips in order, align hard cuts to kick, snare, or major musical changes, keep Shot 3 between face-led shots as the intentional insert, apply one consistent film-grain and color treatment across the timeline, and export at the intended aspect ratio and final duration.

Exact audio synchronization requires the user to provide or select the music reference. Never claim to have analyzed an audio file that was not supplied.

## Example: unclear image input

User: uploads a night rooftop portrait and says, `무드 추천해줘.`

Respond in Korean:

> 업로드한 이미지는 어두운 밤하늘, 거친 재킷 질감, 차가운 도시 스카이라인이 중심입니다. 가장 안정적으로 확장할 수 있는 방향은 다음 세 가지입니다.
>
> 1. **다크 사이버 느와르:** 젖은 옥상, 차가운 블루 림라이트, 낮은 시점의 긴장감
> 2. **90년대 로우파이 힙합:** 따뜻한 가로등, 거친 필름 입자, 느슨한 헤드 바운스
> 3. **멜랑콜리 시네마틱 무드:** 밤안개, 긴 호흡의 시선 처리, 고독한 실루엣
>
> 원하는 번호를 선택하거나, 비·안개·연기·야간 조명처럼 추가하고 싶은 환경 연출을 말씀해주세요.

## Final output contract

- Situation A: Korean visual summary and three numbered direction options only.
- Situation B: Korean anchor summary, Korean timeline table, then four separate copy-ready English prompts.
- Keep the skill independent from STORM and Notion.
- Never claim that audio, video, or current tool behavior was analyzed unless it was actually supplied.
- Use `@image1` consistently unless the user explicitly provides another tag.
