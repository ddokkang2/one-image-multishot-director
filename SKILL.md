---
name: one-image-multishot-director
description: "Use when turning one image into a Seedance 2.5 master prompt."
version: 1.1.0
author: DIO + Hermes
license: MIT
metadata:
  hermes:
    tags: [seedance, video-generation, multishot, image-to-video]
    related_skills: [seedance-clean, seedance-pipeline, seedance-camera]
---

# Seedance 2.5 One-Image Multi-Shot Director

This is an independent Seedance 2.5 directing skill. It is separate from STORM, Notion workflows, and project-specific prompt systems. Do not import STORM structure.

The user provides one reference image, `@image1`, plus a short concept, genre, mood, action, and optionally a requested duration. Turn that input into a short-form mood-film plan and one copy-ready Seedance 2.5 master prompt. The master prompt contains an internal four-beat arc and is pasted into one generation. Explain the direction in Korean; write the single prompt in English for direct pasting into Seedance.

## Core principles

### 1. Visual analysis and three-direction onboarding

When the user uploads only an image or gives an unclear concept:

1. Summarize the visible subject, environment, lighting, and optical feeling in two or three Korean lines.
2. Propose three directions with different genres or moods that are likely to work well with the image.
3. Ask the user to choose a number or add an environmental direction such as rain, fog, smoke, neon, golden-hour light, or dust.

Do not write final prompts until the user selects a direction or supplies a sufficiently specific concept.

### 2. Visual Anchor Lock

Extract and preserve these constants across all four internal beats:

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

### 4. Single-generation four-beat arc

Use one generation and one master prompt by default. Inside that prompt, design four timed beats:

- Beat 1: atmosphere and establishing frame
- Beat 2: main mood, emotion, or performance
- Beat 3: macro insert detail
- Beat 4: climax and hero ending

For a 30-second default, use 0–5s, 5–12s, 12–22s, and 22–30s. For another duration, redistribute the same dramatic arc into explicit timecodes. The four beats are internal sections of one prompt, not four separate prompts or four required uploads.

Beat 3 must be an insert focused on a hand, prop, foot, texture, surface, or environment detail. Keep the face out of the insert whenever possible. This creates a deliberate visual breathing point and helps hide small identity differences between face-led beats.

Use simple physical actions. Prefer one clear action per beat. Avoid intricate finger choreography, complex fights, impossible body movement, and abrupt multi-axis camera movement.

Never split the result into four prompts unless the user explicitly asks for separate clips, retries, or edit-ready assets.

## Duration selection gate

Before writing the final master prompt, resolve the requested total duration:

- If the user states a duration, use it exactly.
- If the user has selected a mood but has not stated a duration, ask them to choose: `1) 15초  2) 20초  3) 30초  4) 직접 입력`.
- If the user provides a custom duration, calculate explicit internal timecodes for the four beats and state the total duration at the top of the timeline.
- Use 30 seconds as the default only when the user says to use the default or gives no duration preference after being asked.
- Do not return the final prompt while the duration is unresolved.

Reference timing templates:

- 15 seconds: 0–2.5s / 2.5–5.5s / 5.5–10.5s / 10.5–15s
- 20 seconds: 0–3s / 3–7s / 7–14s / 14–20s
- 30 seconds: 0–5s / 5–12s / 12–22s / 22–30s

These are one-generation time ranges. They do not imply separate clips.

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

### Step 2: Duration-specific timeline table

Use a Markdown table with these columns:

| 구간 | 시간 | 화면 구간 | 카메라 무빙 | 화면에서 일어나는 일 | 연출 의도 |
|---|---:|---|---|---|---|

Use the user's selected duration and write explicit timecodes for all four internal beats. Explain in Korean so a beginner can visualize that the four beats occur inside one generation. Beat 3 must be a macro or insert detail and should avoid a face-led composition.

### Step 3: Seedance 2.5 single master prompt

Output exactly one English prompt in one code block. It must be ready to paste into one Seedance 2.5 generation. Do not output four separate prompts unless the user explicitly asks for them.

The prompt must state the total duration and use a timed multishot structure inside one generation. Include explicit `HARD CUT` points only when internal cuts improve the concept; otherwise describe the four beats as one continuous camera path. Lock that cuts occur only at the specified points and the camera does not add its own cuts.

Use this internal structure:

```text
SCENE CONTEXT
[What happens across the complete requested duration.]

ACTIVE REFERENCES
[Referenced from @image1 + minimal identity anchor.]

LOCATION MAP
[Foreground, midground, background, light source, movement paths.]

FIRST FRAME / BLOCKING
[The exact opening composition.]

FORMAT MODE
[Total duration; timed internal beats or one continuous take; cut behavior.]

OPTICS
[Shot size and FOV per beat; one primary camera move per beat; no drift mid-segment.]

CAMERA
[Camera behavior and transitions between beats.]

ACTION
[Explicit timed subject actions and observable emotion.]

PERFORMANCE / PHYSICS / LIGHTING / COLOR GRADE / WARDROBE
[Only the blocks this concept needs.]

STYLE / OUTPUT SETTINGS
[Visual finish, aspect ratio when known, grain, and requested duration.]

POSITIVE LOCKS
[Stable identity, environment geometry, wardrobe, prop state, and continuity.]
```

The single prompt should contain the requested duration, `referenced from @image1`, one clear action per beat, fixed identity and environment anchors, lighting and color treatment, lens feeling, film grain and depth of field when useful, positive continuity locks, `photorealistic, high fidelity` when photorealism is appropriate, and `clean frame, readable composition` when useful.

Use positive phrasing. Prefer `stable facial identity`, `clean wardrobe silhouette`, `stable geometry`, and `controlled hand position` over long negative lists. Use `no text` or `no captions` only when the user did not request text and the absence of text materially protects the shot. If the shot requires visible text, preserve the exact text supplied by the user and state it verbatim.

## Prompting rules

- Write what is visible, measurable, and physically observable.
- Replace mood-only words with actions, light behavior, posture, gaze, texture, and camera behavior.
- Keep one primary camera movement per internal beat.
- State the first-frame composition clearly.
- Keep foreground, midground, and background distinct.
- Describe emotion through facial muscle movement, eye-line, breath, posture, and timing.
- Keep the original reference image as the identity anchor for the entire generation.
- Use the same wardrobe, lighting direction, environment geometry, and prop state across the timeline.
- Use an insert beat to reduce face exposure and create rhythm, not as an accidental workaround.
- If the user specifies a different total duration, redistribute the four beats and write explicit timecodes.
- Deliver one master prompt by default; split only when the user explicitly requests separate clips.
- If the user asks for a single continuous take, remove internal cuts and write one continuous camera path.

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
4. Choose the total duration: 15, 20, 30 seconds, or enter a custom duration.
5. Receive the Korean anchor summary, duration-specific timeline, and one English master prompt.
6. Paste the single master prompt into one Seedance 2.5 generation using the original `@image1` reference.

### Step 3: Render one master generation

Use the original high-quality `@image1` as the reference for the entire selected duration. Paste the one master prompt into one Seedance 2.5 generation. Do not use a previous generated clip's last frame as the next identity reference. Reusing compressed generated frames can accumulate blur and identity drift.

The four beats, including the insert beat, are internal timecoded sections of this one generation. The selected duration controls the complete output length.

### Step 4: Optional finishing edit

Use an editor such as CapCut only for optional music, color finishing, trimming, or captions. If the master generation already contains the intended internal cuts, do not split it into four clips unless a specific repair or alternate edit is needed. Align any music accents to the internal cuts, keep one consistent film-grain and color treatment, and export at the intended aspect ratio and selected duration.

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
- Situation B: Korean anchor summary, Korean duration-specific timeline table, then exactly one copy-ready English master prompt.
- If duration is missing, ask for duration selection before producing the master prompt.
- Keep the skill independent from STORM and Notion.
- Never claim that audio, video, or current tool behavior was analyzed unless it was actually supplied.
- Use `@image1` consistently unless the user explicitly provides another tag.
