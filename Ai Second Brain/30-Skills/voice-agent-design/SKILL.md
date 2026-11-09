---
name: voice-agent-design
description: Design a realtime speech-to-speech agent: choose the right voice shape, handle turn-taking and barge-in, budget latency by measuring it, and keep a text fallback — with consent and disclosure handled before anyone speaks to it. Use when a product needs live voice conversation, not just a transcript of a recording.
---

# Voice Agent Design

## Outcome

A voice agent design that a builder can implement without guessing at the shape: the voice shape is named, the speech services and their migration dates are stated, turn-taking and interruption behaviour is specified, latency is measured rather than assumed, and consent, disclosure, and a text fallback are in place before the first real conversation.

## Supporting skills

Load only what the gap requires:

- [AI Feature Architecture](../ai-feature-architecture/SKILL.md) for deciding whether voice is the right interface at all, and for model and provider selection.
- [Retrieval Grounding Design](../retrieval-grounding-design/SKILL.md) when the voice agent must answer from retrieved documents rather than from the model alone.
- [AI Evaluation Engineering](../ai-evaluation-engineering/SKILL.md) for building the eval set that proves the voice agent works on real calls, not just in a demo.

## Alpha status

The voice services this skill describes change between releases: model names, shutdown dates, and session limits are a snapshot checked 2026-11-07. Re-check the provider's own documentation before relying on any model name, date, limit, or capability stated here. Nothing in this skill is a promise that a particular model, voice, or session behaviour exists, works, or stays the same.

## Name the shape first: three kinds of voice AI

Voice AI is three different shapes that are often conflated. Name the shape before choosing any service, because the shape decides the architecture:

- **File / batch STT** — upload a finished recording, get a transcript back. The right shape for recordings: meetings, interviews, voicemail, dictated notes. Latency per turn does not matter; accuracy and speaker labelling do.
- **Live transcription** — stream audio as it arrives, get partial transcripts while the speaker is still talking. The right shape for captioning, live note-taking, and monitoring a call in progress.
- **Speech-to-speech (voice agent)** — one session takes audio in and returns audio out, with tool use in between. The right shape only when live conversation is the product: a spoken assistant, a phone agent, a hands-free interface.

The older chained pipeline is STT → LLM (text) → TTS: three separate services in sequence. The newer speech-to-speech path collapses that into a single model over one persistent connection, which removes the handoffs between services. That is a structural difference, not a guarantee of any particular response time — measure the latency of the shape you actually build.

Do not build a speech-to-speech agent when file transcription would do. A recording does not need a live session, and a live session adds failure modes (turn-taking, interruption, session limits) that a batch job never has.

## STT and TTS choices, with the published shutdown dates

### File transcription

The current recommended hosted file-transcription model on the OpenAI API is `gpt-transcribe`. It accepts a `prompt` (unstructured context), `keywords` (literal terms expected), and `languages` (expected input languages) to improve recognition of domain terms. Keywords are hints, not required output, and can cause unspoken terms to appear in the transcript — evaluate any keyword use against the original audio.

The models it replaces are deprecated with a published shutdown date:

- `whisper-1`, `gpt-4o-transcribe`, `gpt-4o-mini-transcribe`, `gpt-4o-transcribe-diarize`, and the `/v1/audio/translations` endpoint shut down **2027-02-26**.

Migration risks to plan for, not discover in production:

- File limit is **25 MB**; accepted formats are `mp3, mp4, mpeg, mpga, m4a, wav, webm`. For larger recordings, compress or split into chunks of 25 MB or less, and avoid splitting mid-sentence.
- Word-level timestamps are documented only for `whisper-1`. A subtitle or caption pipeline that depends on word-level timestamps needs a new plan before migrating.
- Speaker labelling (diarization) is available only through the file endpoint with the deprecated `gpt-4o-transcribe-diarize` model, and is not supported in Realtime transcription sessions.
- `whisper-1` prompts are capped at **224 tokens**, and Whisper does not follow instructions like a general-purpose text model. A text model can post-process a transcript for spelling of product names, but check corrections against the original audio.
- File transcription can stream partial text without a Realtime session; `whisper-1` does not support this. For live microphone or call audio, use Realtime transcription instead.

The open Whisper model itself (code and weights, MIT licence) is a separate thing from the hosted `whisper-1` API model: the hosted endpoint is what shuts down on 2027-02-26. A locally run Whisper model is an alternative migration path, with its own hardware and accuracy trade-offs — and its own widely reported limitation: Whisper can hallucinate fabricated text, especially during silent or low-speech audio. Treat any transcript of silence, music, or long pauses as suspect and verify it against the audio.

### Text-to-speech

The file-based OpenAI Speech API is also deprecated:

- `tts-1`, `tts-1-hd`, and `gpt-4o-mini-tts` shut down **2027-01-06**. OpenAI directs new integrations to a Realtime model via the Realtime API — a change of workflow, not a drop-in model swap, since the Realtime model is not a supported model for the file speech endpoint.

Facts about the deprecated endpoint that matter for migration planning: the speech endpoint takes model + text + voice, with an input limit of **4,096 characters** per request; output formats include `mp3` (default), `opus`, `aac`, `flac`, `wav`, and `pcm`, with `wav` or `pcm` recommended for fastest response; streaming lets audio play before the full file is generated. `gpt-4o-mini-tts` accepts an `instructions` prompt controlling accent, emotional range, intonation, impressions, speed, tone, and whispering. The built-in voices are `alloy, ash, ballad, coral, echo, fable, nova, onyx, sage, shimmer, verse, marin, cedar`, with `marin` or `cedar` recommended for best quality; the voices are optimised for English.

Do not plan new work on either deprecated surface. Pin the migration dates in any plan that touches them, and re-check the provider's docs on the day of the migration — model names in this area change fast.

## Realtime speech-to-speech sessions

A Realtime session is a stateful session over WebRTC (browsers) or WebSocket (servers). A Realtime model has speech-to-speech conversations without an intermediate text-to-speech or speech-to-text step, which gives the model more data about the tone and inflection of voice input.

Session facts to design around:

- Maximum session duration is **60 minutes**. Plan what happens at the limit: a clean handover, a summary carried into a new session, or a graceful close — not a silent drop.
- Most session properties can be updated mid-session via `session.update`, **except the voice after the model has responded with audio once**. Choose the voice before the first response, because it cannot be changed after.
- Audio over WebSocket is base64-encoded chunks sent with `input_audio_buffer.append`, each chunk at most 15 MB, in PCM format at 24 kHz mono. WebRTC handles much of the media plumbing via the peer connection.
- The Realtime conversations guide also covers image input alongside audio and text generation and function calling, so a voice agent can see as well as hear — but the vision limits in [Multimodal Input Verification](../multimodal-input-verification/SKILL.md) still apply to anything it reads from an image.

Realtime prompting, per the provider's own voice-prompting guidance: start with low reasoning effort; use short spoken preambles ("I'll check that order now") — preambles are not hidden chain-of-thought; reason before acting only for multi-step, tool, or escalation tasks, and answer directly for simple lookups; do not do extended reasoning when the audio is unclear — ask for clarification instead. Keep answers direct: one or two short sentences, one clarifying question at a time, summarise tool results first, then the next useful action.

## VAD and turn-taking

Voice activity detection (VAD) is enabled by default in speech-to-speech sessions, is optional, and can be turned off. Two modes:

- `server_vad` (default): chunks audio on silence. Tunable: `threshold` (0–1; higher means louder audio is needed, and may perform better in noisy environments), `silence_duration_ms`, `prefix_padding_ms`, `create_response`, `interrupt_response`, `idle_timeout_ms`.
- `semantic_vad`: a classifier decides the user has finished speaking based on the words uttered; it is less likely to interrupt the user mid-sentence or to chunk a transcript before the user is done speaking. Tunable `eagerness` (`low` / `medium` / `high` / `auto`).

The session emits `input_audio_buffer.speech_started` and `speech_stopped` events. Setting turn detection to `null` disables VAD entirely (push-to-talk); the client must then send `commit` and `response.create` manually.

For Realtime transcription sessions using `gpt-live-transcribe` or `gpt-realtime-whisper`, turn detection must be omitted or set to `null`, and the client sends `input_audio_buffer.commit` per turn.

Tune VAD on real recordings from the target environment, not on clean demo audio. In noise, expect false speech starts and clipped turns; a higher threshold helps, but it is a trade-off against missing quiet speech. Provide push-to-talk or a text fallback for the cases VAD gets wrong.

No wake-word mechanism is documented in the OpenAI Realtime pages checked for this skill. Wake-word detection is normally a separate on-device step, not a capability of the Realtime API — do not assume the API provides one. Telephony claims (native SIP, PSTN bridging, DTMF) were not verified on an official page in the research behind this skill; treat them as unverified until checked against the provider's telephony documentation.

## Interruption (barge-in) via cancel and truncate

When VAD is enabled, the API detects user speech, cancels the ongoing response, and starts a new one. Cancelling is not enough on its own: to keep the conversation coherent, truncate the model's last response — remove the unplayed portion from the conversation — via `conversation.item.truncate` with the point in the audio where playback stopped (`audio_end_ms`).

The server cancels with `response.done` and `status: cancelled`. Do not wait for that event before stopping playback or sending the truncation event — stop playback and truncate immediately, then let the confirmation arrive.

`interrupt_response` defaults to `true`. If it is turned off, the user cannot interrupt the model, and the agent will talk over them. That is a deliberate design choice, not a default to leave unexamined: decide it per use case, and say which you chose.

## Latency budgeting: measure, do not quote

The provider's own documentation does not publish a single end-to-end latency number for Realtime sessions. Third-party latency budgets exist, but they are estimates from other people's setups, not vendor guarantees and not transferable to yours. Do not quote a millisecond figure for your agent from a blog post, a marketing page, or this skill.

Budget latency by measuring the pipeline you actually built:

- Instrument the turn: time from the end of user speech (`input_audio_buffer.speech_stopped`) to the first audible audio, and to the completed response.
- Measure on the real network, the real device, and the real model — not on a developer machine on office Wi-Fi.
- Break the budget down by stage (capture, network, VAD end-of-turn, model inference and first audio, playback start) so a slow turn can be attributed to a stage instead of blamed on "the model".
- Re-measure when the model, the network, or the VAD settings change. A latency number from last quarter is a historical note, not a current budget.

The structural claim is safe to rely on: collapsing three services into one removes the handoffs between them. The magnitude of the saving in your deployment is a measurement, not a claim.

## Consent and disclosure for cloned and AI voices

- **Disclose AI generation.** The provider's usage policies require a clear disclosure to end users that the voice they are hearing is AI-generated and not a human voice. Build the disclosure into the agent's opening, not into a terms page nobody reads.
- **Clone only with consent.** Only clone your own voice, or a voice where you hold explicit, documented consent — ideally written, covering capture, cloning, synthesis, and commercial use. The provider requires a consent recording for custom voices.
- **Do not impersonate.** Do not use a cloned voice to impersonate a real person, to defeat voice authentication, or to make someone appear to say something they did not say. Providers bar this in their prohibited-use policies.
- **Know the limits of what was verified.** The exact consent-phrase wording, sample durations, and eligibility rules for custom voices were not opened in the research behind this skill, and third-party cloning providers' exact terms were checked only through secondary summaries, not their own policy pages. Re-check the provider's own documentation and terms before cloning any voice, and do not quote plan names or sample lengths from this skill as verified fact.

## Recording consent and PII in audio

- **Recording consent is a legal question, not a product default.** Recording laws vary by jurisdiction (one-party vs all-party consent), and audio is biometric-adjacent data in some jurisdictions — voiceprints are treated as biometric identifiers in some places, with written-consent requirements. This skill gives no legal advice: check the law where the speakers are, and record the answer in the design.
- **Audio and transcripts are sensitive data.** They can contain names, account numbers, health details, and credentials spoken aloud. Minimise retention, redact before logging or ingesting transcripts into retrieval, and do not send raw call audio to a third-party service without checking its data-retention terms.
- **Keep the audio, not just the transcript.** A transcript is not a verbatim record unless verified. Keep the audio alongside the transcript for anything consequential, and say how long each is retained and who can access it.

## When to use text instead

Use text when the content must be exact (numbers, code, addresses, legal or financial terms); when the user needs to skim, search, copy, or refer back; when the environment is noisy or public; when the task is long-form reading or writing; or when auditability matters. Use voice when hands or eyes are busy, the interaction is short and conversational, accessibility requires it, or the user prefers speaking — and even then, keep a text transcript visible.

A voice agent is never voice-only. Always offer text: it is the fallback for noisy places, speech differences, missing microphones, and every turn the VAD gets wrong.

## What a good voice agent design hands over

Before any building starts, the design should be able to answer, from its own records:

- Which voice shape it is, and why the other two shapes were not chosen.
- Which speech services it uses, their shutdown dates, and the migration plan for each deprecated one.
- How VAD is configured, how interruption and truncation work, and what happens at the 60-minute session limit.
- A measured latency budget for the real deployment, with the measurement method stated.
- How consent, disclosure, recording consent, and audio retention are handled.
- What the text fallback is, and when the agent offers it.

If any of those answers is missing, the design is not finished — it is paused, and the handover says so.

## Validation exercises

Run these as small exercises on a target the builder owns, with consent recorded. Hub projects are tutorial/demo starting points for learning, not deployable systems — study them, adapt them, and do not present them as hardened production components. Nothing in any validation touches another project's UI.

- Run a short scripted call against the hub's `real-time-voicebot` as a reference implementation, with a text fallback visible throughout. Record where VAD cut a turn early or late, and what the fallback covered.
- Run the hub's `rag-voice-agent` as a reference implementation and check what happens when the retrieved answer is wrong: does the spoken answer sound more certain than the evidence warrants?
- Run the hub's `mcp-voice-agent` as a reference implementation and list every tool the voice agent can call. Confirm which ones need human approval before acting.
- Run the hub's `chat-with-audios` as a reference implementation for the file-STT shape: transcribe a recording with long silences and check the transcript against the audio for hallucinated text.
- Run the hub's `multilingual-meeting-notes-generator` as a reference implementation and test it on the target accent and language mix, not on clean demo audio. Record where accuracy visibly drops.
- For each exercise, write down the measured latency of a turn and the migration date of every model used. A model past its shutdown date fails the exercise.

## Design checklist

Before handing a voice agent design to a builder, answer every line:

- [ ] The voice shape is named (file STT, live transcription, or speech-to-speech) with a reason the other shapes were not chosen.
- [ ] Every speech service is named with its shutdown date, and no new work is planned on a deprecated surface.
- [ ] The migration plan covers word-level timestamps and speaker labelling if the design depends on them.
- [ ] VAD mode and settings are stated, tuned on real recordings, with push-to-talk or a text fallback for the cases it gets wrong.
- [ ] Interruption handling specifies cancel plus `conversation.item.truncate`, without waiting for `response.done`.
- [ ] The 60-minute session limit has a planned handover or close, and the voice is chosen before the first audio response.
- [ ] Latency is measured on the real deployment, broken down by stage — no quoted millisecond figure from a third party.
- [ ] AI-voice disclosure is built into the agent's opening, and any cloned voice has explicit, documented consent.
- [ ] Recording consent is checked for the speakers' jurisdiction, and audio/transcript retention and redaction are specified.
- [ ] A text fallback is offered at all times, and the design says when to use text instead of voice.

## State

This skill has not yet been exercised on a real voice agent for a target the user owns. Promote it only after one such exercise — a short scripted call with a text fallback, on a target the user owns, with consent recorded — and revise it from the failures that exercise surfaces.

Draft pending representative validation.
