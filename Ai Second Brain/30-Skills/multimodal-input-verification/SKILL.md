---
name: multimodal-input-verification
description: Use vision, audio, and video model output safely: know what the model can and cannot do, use dedicated OCR for exact text, validate structured output in code, and cross-check counts and transcribed values before acting on them. Use when a feature reads images, video, or audio as input and a wrong reading would cause a wrong action.
---

# Multimodal Input Verification

## Outcome

A design that treats model readings of images, video, and audio as drafts, not measurements: the limits are stated up front, exact text goes through dedicated OCR, structured output is validated in code, and no count or transcribed value is acted on until a second method has confirmed it.

## Supporting skills

Load only what the gap requires:

- [AI Prompt Structured Output Design](../ai-prompt-structured-output-design/SKILL.md) for shaping the model's output into a schema the application can validate.
- [Retrieval Grounding Design](../retrieval-grounding-design/SKILL.md) when images, audio, or video are sources in a retrieval system rather than one-off inputs.
- [AI Evaluation Engineering](../ai-evaluation-engineering/SKILL.md) for building the eval set that proves the verification steps catch real errors.
- [Voice Agent Design](../voice-agent-design/SKILL.md) when the multimodal input is spoken audio handled by a voice agent.

## Alpha status

The model limits and per-request caps this skill describes are a snapshot checked 2026-11-07, and they differ by model generation. Re-check the provider's own documentation for the exact model in use before relying on any limit, capability, or file size stated here. Nothing in this skill is a promise that a particular model reads a particular input the same way twice, or stays the same between releases.

## What models can do

Current multimodal models can, in broad terms:

- **Describe** the contents of an image, an audio clip, or a video: what is in it, what is happening, what it appears to show.
- **Segment and extract** information from a video, answer questions about video content, and refer to specific timestamps.
- **Read text** that appears in images, as interpretation — the model understands the text it sees and restates it.
- **Accept mixed input** in one request: text plus images, audio, or video together, and in some cases image input alongside audio and text generation in a realtime session.

Those are capabilities, not guarantees. The same model can describe one image well and misread a nearly identical one. A capability that works in a demo is not a capability that works on the target's real inputs until it has been tested on them.

## What vendors themselves disclose they cannot do

The limits below are the vendors' own words, not a critic's list. Design around them, because they are the places where a confident-looking answer is most likely to be wrong:

- **Precise localisation.** The models are not precise at locating text or objects in images. A bounding box or a position the model gives is approximate, and should be treated as a rough indication, not a coordinate.
- **Approximate counts only.** They might only return approximated counts of objects. A count from a vision model is an estimate, never a measured total.
- **Hallucinations on poor images.** The models might hallucinate or make mistakes when interpreting low-quality, rotated, or extremely low-resolution images. Small or rotated text is a known weak spot.
- **No medical-image interpretation.** They are not suitable for interpreting medical images (for example, x-rays and CT scans) or providing medical advice. Do not route medical images through a general vision model.
- **No identifying non-celebrities.** They are not meant to be used to identify people who are not celebrities in images. Do not build a feature that identifies private individuals from a photo.
- **Content refusals apply.** Content moderation refusals apply to images that violate safety policies, so a legitimate image can still be refused if it trips a policy filter — plan for the refusal as a normal outcome, not an error.
- **Grounding limits.** In some provider flows, web grounding is not supported for multimodal prompts. A multimodal answer cannot silently gain a web-grounded citation it was never given.

Per-request limits are also model-specific and change between generations, so check the model card for the exact model in use. As a 2026-11-07 snapshot for standard Gemini 3 and later models: up to 3,000 images and PDFs combined per request (up to 6,500 combined multimodal files when plain-text files are included); up to 1,000 audio files or 10 videos per request; a 1,048,576-token context window; at default high resolution that fits at most 936 images per request unless media resolution is lowered. Supported image types in that snapshot are `png, jpeg, webp, heic, heif`, with an inline part limit of 256 MB. For video, limits differ by generation — an older model card allows roughly 45 minutes of video with audio (about an hour without), 10 videos per prompt, and about 8.4 hours of audio per prompt. Do not mix limits across generations: the numbers for one model are not the numbers for the next.

## OCR by interpretation vs strict OCR

A vision model reads text in images by interpretation, not as a strict OCR engine. That distinction decides which tool to use:

- **Interpretation** understands the text and may "fix" spelling or formatting rather than reproduce the text verbatim. It is useful for summarising a sign, a slide, or a document's gist — and dangerous for anything where the exact characters matter.
- **Strict OCR** reproduces the characters as printed, with no helpful corrections. It is the tool for exact extraction: codes, serial numbers, amounts, names, dates, and anything that will be stored, searched, or acted on.

Use dedicated OCR (for example Tesseract, or a provider OCR service) for exact text. Use a vision model for description and triage. When both are in play, the dedicated OCR result is the record; the vision model's reading is the cross-check, not the other way round.

No per-field confidence, coordinates, or fixed schema comes from a plain vision call. If the feature needs those, they have to be built by the application around the call — see the next section.

## Structured output and application-side validation

A plain vision call returns free text. Free text cannot be trusted as data. To make a model reading usable by code:

- **Ask for structured output.** Request the reading in a fixed schema: named fields, typed values, explicit "not found" values instead of invented ones. A field the model cannot fill should come back empty, not guessed.
- **Validate in the application, not in the prompt.** Check types, ranges, formats, and required fields in code after the call returns. A value that fails validation is rejected or flagged, never silently accepted.
- **Never copy a citation or a value from the model's free text.** Citations and extracted values must be constructed by the application from the inputs actually sent and the validated outputs actually returned — a source the model invents looks verified and is not.
- **Treat the schema as a contract, not a guarantee.** A model can return well-formed output with wrong content. Structured output makes errors checkable; it does not make them impossible.

## The cross-check rule

Before acting on a count or a transcribed value from a multimodal model, confirm it with a second method:

- **Crop and re-ask.** Crop the image to the region in question and ask again, at higher resolution. If the two answers disagree, neither is the answer yet.
- **Dedicated OCR.** For text, run a strict OCR tool and compare its output character by character with the model's reading.
- **A second pass with different framing.** Ask for the count or value in a different way (count by groups, list each item, read the field aloud) and compare.
- **A human check.** For anything consequential — a payment, a medical-adjacent decision, a legal record, a safety-critical count — a human confirms the value before it is acted on.

The rule is: one model reading is a draft. Two independent methods agreeing is evidence. A single reading acted on directly is a gamble, and the odds are worst exactly where the vendor disclosed the weakness: counts, precise locations, small or rotated text, and low-quality images.

This applies equally to audio: a transcript of silence, music, or long pauses can contain hallucinated text, and keyword hints can insert unspoken terms. Verify a transcript against the audio before treating it as a record, especially for numbers, names, or consent.

## Failure modes

| Failure | What happens | What helps |
|---|---|---|
| Approximate count treated as exact | The model estimates a count; the feature stores it as a measured total. | Cross-check rule; dedicated counting tool or human count for consequential totals. |
| Invented coordinates | The model gives a location that looks precise and is wrong. | Treat locations as approximate; verify against a dedicated detector or a human. |
| "Fixed" transcription | The model corrects spelling or formatting instead of reproducing the text. | Dedicated OCR for exact text; compare outputs character by character. |
| Hallucination on poor images | Low-quality, rotated, or very low-resolution input produces confident nonsense. | Reject or flag poor inputs up front; ask the user for a clearer image. |
| Medical or identity misuse | A medical image or a private person's photo is sent to a general model. | Route medical images and identity questions away from general vision models entirely. |
| Silent refusal | A policy refusal is treated as an error and retried, or as an empty result. | Handle refusal as a normal outcome with a user-facing explanation and a fallback. |
| Overconfident draft | A plausible-sounding description is presented to the user as a verified fact. | Show uncertainty; show the source image alongside the reading; never present a draft as a measurement. |

## What a good multimodal design hands over

Before any building starts, the design should be able to answer, from its own records:

- Which inputs the model reads, and which of those readings are drafts vs records.
- The vendor-disclosed limits that apply to the exact model in use, checked against that model's own documentation.
- Which values go through dedicated OCR and which go through the model — and why.
- The structured output schema and the application-side validation for every field.
- The cross-check method for every count and transcribed value the feature acts on.
- What happens on a refusal, a poor-quality input, or a disagreement between the two methods.

If any of those answers is missing, the design is not finished — it is paused, and the handover says so.

## Validation exercises

Run these as small exercises on inputs the builder owns. Hub projects are tutorial/demo starting points for learning, not deployable systems — study them, adapt them, and do not present them as hardened production components. Nothing in any validation touches another project's UI.

- Run the hub's `deepseek-multimodal-RAG` as a reference implementation and ask it to count the objects in a crowded image twice, with different framings. Record whether the two counts agree, and by how much.
- Run the hub's `multimodal-rag-assemblyai` as a reference implementation and check a transcript of a recording with long silences against the audio. Record any text the transcript invents.
- Run the hub's `ai-avatar-demo` as a reference implementation and list what the avatar's spoken output claims about an image it was shown. Mark every claim that is a draft rather than a verified fact.
- Run the hub's `video-rag-gemini` as a reference implementation and ask for the timestamp of an event in a video, then check the timestamp by watching that part of the video. Record how far off it is.
- Run the hub's `gemma3-ocr` as a reference implementation on a document with a serial number or an amount. Compare the vision model's reading character by character with a dedicated OCR tool's output, and record every difference.
- For each exercise, write down the model used, the input quality, and which cross-check caught (or failed to catch) each error. An exercise that finds no errors on clean demo inputs is not finished — repeat it on poor, rotated, or low-resolution inputs.

## Design checklist

Before handing a multimodal design to a builder, answer every line:

- [ ] The vendor-disclosed limits for the exact model in use are stated, checked against that model's own documentation.
- [ ] Every model reading is labelled a draft or a record, and no draft is presented to the user as a measured fact.
- [ ] Exact text goes through dedicated OCR; the vision model is used for description and triage, not exact extraction.
- [ ] Structured output is requested in a fixed schema, and every field is validated in application code.
- [ ] Citations and extracted values are constructed by the application, never copied from the model's free text.
- [ ] The cross-check rule is specified for every count and transcribed value the feature acts on.
- [ ] Medical images and identification of non-celebrities are routed away from general vision models.
- [ ] Refusals and poor-quality inputs are handled as normal outcomes, with a user-facing explanation and a fallback.
- [ ] Audio transcripts are verified against the audio before being treated as a record, especially for numbers, names, or consent.
- [ ] No per-request limit is quoted from a different model generation than the one in use.

## State

This skill has not yet been exercised on a real multimodal feature for a target the user owns. Promote it only after one such exercise — a feature that reads real images or video, cross-checks its counts and transcribed values, and records what the checks caught — and revise it from the failures that exercise surfaces.

Draft pending representative validation.
