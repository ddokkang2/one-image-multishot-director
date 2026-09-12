---
name: one-image-multishot-director
description: "Use when turning one reference image into a Seedance 2.5 master prompt for mood-film or performance-first video direction."
license: MIT
metadata:
  hermes:
    version: 1.2.0
    author: DIO + Hermes
    tags: [seedance, video-generation, multishot, image-to-video]
    related_skills: [seedance-clean, seedance-pipeline, seedance-camera]
---

# Seedance 2.5 One-Image Multi-Shot Director

This is an independent Seedance 2.5 directing skill. It is separate from STORM, Notion workflows, and project-specific prompt systems. Do not import STORM structure.

The user provides one reference image, `@image1`, plus a short concept, genre, mood, action, and optionally a requested duration. Turn that input into a mode-appropriate short-form video plan and one copy-ready Seedance 2.5 master prompt. Use an atmosphere-first mood-film mode for reflective concepts and a performance-first mode for concerts, dance, music videos, action, reveals, and other energetic concepts. The master prompt contains an internal four-beat arc and is pasted into one generation. Explain the direction in Korean; write the single prompt in English for direct pasting into Seedance.

## Directing mode selection

Choose the mode from the user's concept, selected direction, requested action, and energy:

- `MOOD`: atmosphere, reflection, quiet daily life, romance, mystery, or slow cinematic observation. Preserve the existing restrained arc.
- `PERFORMANCE`: singing, dancing, concerts, music videos, stage shows, action, chase, transformation, celebration, or any request that depends on visible kinetic energy. Prioritize an immediate hook, escalating movement, and a visible payoff.
- `HYBRID`: a quiet opening that develops into a clearly specified action or reveal. Use the performance motion contract after the turning point.

When the user selects a live concert, idol, dance, or music-video direction, choose `PERFORMANCE` automatically. Do not apply performance intensity to a quiet concept merely because the reference image is visually dramatic. State the chosen mode and energy profile in the Korean direction summary and in the English master prompt.

## Core principles

### 1. Visual analysis and three-direction onboarding

When the user uploads only an image or gives an unclear concept:

1. Summarize the visible subject, environment, lighting, and optical feeling in two or three Korean lines.
2. Propose three directions with different genres or moods that are likely to work well with the image.
3. Ask the user to choose a number or add an environmental direction such as rain, fog, smoke, neon, golden-hour light, or dust.

Do not write final prompts until the user selects a direction or supplies a sufficiently specific concept.

### 2. Visual Anchor Lock

Extract and preserve these identity and world constants across all four internal beats. Keep the identity stable without freezing the pose or performance:

- subject identity and recognizable facial features
- basic hairstyle and wardrobe silhouette
- important colors and visible accessories
- environment geometry and spatial landmarks
- lighting direction and color temperature
- lens feeling and camera distance when visible

Use `@image1` for identity and appearance. Keep the written character description short and action-focused so it does not conflict with the reference image.

For `PERFORMANCE` and `HYBRID`, allow the visible body, hair, ribbons, fabric, props, stage lights, and environmental particles to respond dynamically. Apply locks to identity, design, and spatial continuity; do not turn them into a command for a static pose.

### 3. Safe Override Policy

Keep local identity-sensitive details stable. Do not redesign or locally mutate the face, hands, fingers, fine accessories, or wardrobe construction.

Allow overrides at the environment level:

- rain, snow, fog, smoke, dust, haze, or atmospheric particles
- lighting mood such as neon, golden hour, rim light, or moonlight
- background color temperature and exposure mood

State the applied environmental override explicitly. If none is requested, write `None`.

### Motion permission and escalation

Use a motion budget appropriate to the selected mode:

- `MOOD`: small physical actions and restrained camera movement are appropriate when the user wants stillness.
- `PERFORMANCE`: each beat needs one primary observable action with direction and amplitude, plus continuous secondary motion such as hair, ribbons, fabric, lights, or crowd/stage response. Keep the action simple, but let at least one beat make a decisive change in pose, position, direction, or energy.
- A continuity lock applies to identity and design, not to every pose, prop position, or light pattern. Let those states change when the action explicitly causes the change.

Describe escalation through concrete changes: closer versus wider framing, faster versus slower camera energy, a larger body gesture, a new facing direction, a light sweep, a prop interaction, or a final pose that is visibly different from the opening pose. Do not rely on the word `climax` without specifying the event that creates it.

### 4. Single-generation four-beat arc

Use one generation and one master prompt by default. Inside that prompt, design four timed beats. The four beats are internal sections of one prompt, not four separate prompts or four required uploads.

For `MOOD`:

- Beat 1: atmosphere and establishing frame
- Beat 2: main mood, emotion, or performance
- Beat 3: macro insert detail
- Beat 4: quiet climax and hero ending

For `PERFORMANCE`:

- Beat 1: immediate hook and starting impulse; motion begins within the first 0.3–0.5 seconds
- Beat 2: escalation through a decisive visible action, pose change, directional change, or stage interaction
- Beat 3: short impact insert tied to the action; use a hand, prop, foot, texture, surface, or environmental response, and keep the face out when possible
- Beat 4: payoff with a clear peak action and a visibly changed final state, not only a held pose

For `HYBRID`, use the mood arc until the turning point, then follow the performance arc. Use simple physical actions, but add continuous secondary motion in performance beats. Avoid intricate finger choreography, complex fights, impossible body movement, and abrupt multi-axis camera movement.

Beat 3 remains an insert, but it is not automatically a long breathing pause. In `PERFORMANCE`, keep it to roughly 10–20% of the total duration unless the user asks for a longer detail section. Tie the insert to the subject's preceding or following action so it advances rhythm rather than stopping the performance.

Never split the result into four prompts unless the user explicitly asks for separate clips, retries, or edit-ready assets.

## Duration selection gate

Before writing the final master prompt, resolve the requested total duration:

- If the user states a duration, use it exactly.
- If the user has selected a mood but has not stated a duration, ask them to choose: `1) 15초  2) 20초  3) 30초  4) 직접 입력`.
- If the user provides a custom duration, calculate explicit internal timecodes for the four beats and state the total duration at the top of the timeline.
- Use 30 seconds as the default only when the user says to use the default or gives no duration preference after being asked.
- Do not return the final prompt while the duration is unresolved.

Reference timing templates:

- `MOOD` 15 seconds: 0–2.5s / 2.5–5.5s / 5.5–10.5s / 10.5–15s
- `MOOD` 20 seconds: 0–3s / 3–7s / 7–14s / 14–20s
- `MOOD` 30 seconds: 0–5s / 5–12s / 12–22s / 22–30s
- `PERFORMANCE` 15 seconds: 0–2s / 2–5.5s / 5.5–7.5s / 7.5–15s
- `PERFORMANCE` 20 seconds: 0–3s / 3–8s / 8–11s / 11–20s
- `PERFORMANCE` 30 seconds: 0–4s / 4–13s / 13–17s / 17–30s

These are one-generation time ranges. They do not imply separate clips. For `PERFORMANCE`, keep the insert short and allocate the recovered time to visible escalation and payoff. For a custom duration, keep the insert near 10–20% of the total unless the user asks for a detail-led video.

## Situation A: image-only or unclear concept

Return exactly this structure in Korean:

### Step 1: Visual Summary

Summarize the subject and visible wardrobe, background space, lighting and color temperature, and lens or optical feeling. Keep it concise and based only on what is visible.

### Step 2: Three Direction Options

Offer three numbered options. Each option includes a genre or format, mood, visual treatment, and why the reference image is a good fit. Use concrete descriptions rather than vague words such as beautiful, cool, epic, or cinematic.

When the reference visibly suggests a performance, make at least one option explicitly `PERFORMANCE` and describe its motion vocabulary, energy curve, and likely physical actions. Do not make every option an atmosphere-first mood film.

End with:

> 원하는 번호를 선택하거나, 비·안개·연기·야간 조명처럼 추가하고 싶은 환경 연출을 말씀해주세요.

Do not output final Seedance prompts yet.

## Situation B: genre and concept are defined

Return exactly these three stages.

### Step 1: Visual Anchor & Safe Override

Write in Korean:

- **Directing Mode / Energy Profile:** selected mode and intended energy curve
- **Subject Anchor:** fixed subject identity, visible appearance, wardrobe silhouette, and action-critical details
- **Environment Anchor:** fixed location geometry, foreground/midground/background, and visible landmarks
- **Lighting Anchor:** fixed source direction, color temperature, and exposure mood
- **Applied Safe Override:** environment or lighting changes; write `None` when unused

### Step 2: Duration-specific timeline table

Use a Markdown table with these columns:

| 구간 | 시간 | 화면 구간 | 카메라 무빙 | 화면에서 일어나는 일 | 연출 의도 |
|---|---:|---|---|---|---|

Use the user's selected duration and write explicit timecodes for all four internal beats. Explain in Korean so a beginner can visualize that the four beats occur inside one generation. In `PERFORMANCE`, describe a physical action with direction, amplitude, and end state in every beat; include a short action-linked insert rather than a long pause. Beat 3 must be a macro or insert detail and should avoid a face-led composition whenever possible.

### Step 3: Seedance 2.5 single master prompt

Output exactly one English prompt in one code block. It must be ready to paste into one Seedance 2.5 generation. Do not output four separate prompts unless the user explicitly asks for them.

The prompt must state the total duration and use a timed multishot structure inside one generation. Include explicit `HARD CUT` points only when internal cuts improve the concept; otherwise describe the four beats as one continuous camera path. In `PERFORMANCE`, cuts should introduce a meaningfully different shot scale, angle, action state, or stage response. Lock that cuts occur only at the specified points and the camera does not add its own cuts.

Use this internal structure:

```text
SCENE CONTEXT
[What happens across the complete requested duration.]

DIRECTING MODE / ENERGY PROFILE
[MOOD, PERFORMANCE, or HYBRID; energy curve; motion budget; visual escalation.]

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
[Stable identity and design; intentional pose, prop, light, and action-state changes; continuity.]
```

The single prompt should contain the requested duration, `referenced from @image1`, one primary action per beat plus any intentional secondary motion, fixed identity and environment anchors, lighting and color treatment, lens feeling, film grain and depth of field when useful, positive continuity locks, `photorealistic, high fidelity` when photorealism is appropriate, and `clean frame, readable composition` when useful.

Use positive phrasing. Prefer `stable facial identity`, `clean wardrobe silhouette`, `stable geometry`, and `controlled hand position` over long negative lists. Use `no text` or `no captions` only when the user did not request text and the absence of text materially protects the shot. If the shot requires visible text, preserve the exact text supplied by the user and state it verbatim.

For `PERFORMANCE` and `HYBRID` after the turning point:

- Start visible motion within the first 0.3–0.5 seconds; do not spend the opening only holding the reference pose.
- Give every beat a primary subject action, a single primary camera move, an environment or lighting response, and a changed end state.
- Use at least one decisive movement with clear direction or amplitude. Avoid making every beat `small`, `slight`, `gentle`, `subtle`, `slow`, or `controlled`.
- Keep continuous secondary motion between beats: hair, ribbons, fabric, props, lights, particles, or stage elements can react while the main action remains simple.
- Keep the face-free insert near 10–20% of the total duration and connect it causally to the preceding or following action.
- Make the final beat a visible payoff: a completed gesture, changed facing direction, new spatial position, lighting hit, reveal, or interaction. `Hold a hero pose` may follow the payoff but cannot be the only climax.
- Preserve identity and design while allowing pose, prop position, hair, wardrobe movement, and stage lighting to change when the action calls for it.
- State identity locks once in a compact block. Spend the remaining prompt space on trajectory, timing, action, and stage response instead of repeating `stable`, `fixed`, or `preserve` in every beat.

## Prompting rules

- Write what is visible, measurable, and physically observable.
- Replace mood-only words with actions, light behavior, posture, gaze, texture, and camera behavior.
- Keep one primary camera movement per internal beat.
- State the first-frame composition clearly.
- Keep foreground, midground, and background distinct.
- Describe emotion through facial muscle movement, eye-line, breath, posture, and timing.
- Keep the original reference image as the identity anchor for the entire generation.
- Use the same wardrobe design, lighting direction, and environment geometry across the timeline; let pose and prop state change only when the action specifies it.
- Use an insert beat to reduce face exposure and create rhythm, not as an accidental workaround or a long static pause.
- In `PERFORMANCE`, write the action as verb + direction + amplitude + end state, for example: `raises the microphone from chest level to overhead while stepping into the spotlight, ending facing the audience`.
- In `PERFORMANCE`, use concrete kinetic verbs such as `sweeps`, `pivots`, `tracks`, `bursts`, `whips`, `surges`, or `snaps` when appropriate, while keeping one primary move per beat.
- In `PERFORMANCE`, make the state progression explicit: starting pose or position → changed pose or direction → insert evidence of the action → final pose or position.
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
