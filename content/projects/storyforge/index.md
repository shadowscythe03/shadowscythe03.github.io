---
title: 'StoryForge AI Studio: Multilingual Story-to-Video Pipeline'
summary: 'End-to-end generative pipeline that turns keywords into narrated videos — story, scene images, audio, and final MP4 — across 7 languages, powered by Llama 3, Stable Diffusion + LoRA, and MoviePy.'
date: 2025-01-01
authors:
  - admin
tags:
  - Generative AI
  - Computer Vision
  - NLP
  - Multimodal
  - Deep Learning
image:
  caption: 'StoryForge AI Studio Pipeline'
  focal_point: ''
  preview_only: false
url_code: 'https://github.com/AbhayVG/ES667-Deep-Learning-project'
links:
  - icon: brands/github
    name: GitHub
    url: 'https://github.com/AbhayVG/ES667-Deep-Learning-project'
---

StoryForge turns a handful of keywords into a complete narrated video — story, scene images, voice narration, and compiled MP4 — through a 7-stage generative pipeline with a Streamlit interface. Supports English, Hindi, French, German, Spanish, Italian, and Telugu.

## Pipeline Architecture

Each stage is a dedicated Python module; they can be run individually or end-to-end through the Streamlit UI.

| # | Stage | Module | Model / Tool |
| --- | --- | --- | --- |
| 1 | Story generation | `story_generation.py` | Llama 3 via Ollama |
| 2 | Scene prompt extraction | `prompt_generator.py` | Llama 3 |
| 3 | Image synthesis | `image_generator.py` | Stable Diffusion 2.1 + LoRA |
| 4 | Consistency verification | `consistancy_check.py` | BLIP + CLIP |
| 5 | Audio narration | `audio_generator.py` | gTTS |
| 6 | Video compilation | `movie_creater.py` | MoviePy |
| 7 | Interactive interface | `streamlit.py` | Streamlit |

**Character consistency** across scenes is enforced with SameFace_Fix LoRA fine-tuning on the diffusion model. **Semantic alignment** between generated images and story prompts is measured using CLIP similarity scores, averaging >25.0 in test runs.

## Technical Stack

- **LLM**: Llama 3 (Ollama) for story and prompt generation
- **Image generation**: Stable Diffusion 2.1, custom LoRA fine-tuning, VAE
- **Vision-language**: BLIP (captioning), CLIP (semantic similarity)
- **Audio**: gTTS with automatic language detection
- **Video**: MoviePy (image transitions + audio sync, MP4/AVI output)
- **Framework**: PyTorch, HuggingFace Transformers
- **UI**: Streamlit with real-time progress tracking and ZIP export

## Demo Video

<!-- TODO: paste your GitHub blob URL for the video here and convert to raw:
     blob URL:  github.com/shadowscythe03/projects/blob/main/path/to/video.mp4
     raw URL:   raw.githubusercontent.com/shadowscythe03/projects/main/path/to/video.mp4
     Then replace YOUR_RAW_VIDEO_URL below. -->

_Demo video coming soon._

<!-- Uncomment once you have the raw URL:
<video width="100%" controls style="border-radius: 8px; margin: 1rem 0;">
  <source src="YOUR_RAW_VIDEO_URL" type="video/mp4">
  Your browser does not support the video tag.
</video>
-->

## Project Report

<!-- TODO: Upload your project report PDF and replace the src URL below.
     Recommended: upload as a GitHub Release asset on this repo, then use:
     https://docs.google.com/viewer?url=<raw-pdf-url>&embedded=true -->

_Project report coming soon._

<!-- TODO: once your PDF is hosted, replace the line above with:
<iframe
  src="https://docs.google.com/viewer?url=YOUR_PDF_URL_HERE&embedded=true"
  width="100%"
  height="850px"
  style="border: 1px solid #e5e7eb; border-radius: 8px; display: block; margin: 1rem 0;">
</iframe>
[Download PDF](YOUR_PDF_URL_HERE)
-->

---

**Course**: ES667 — Deep Learning, IIT Gandhinagar (Jan–Apr 2025) · 4-member team · Supervised by Prof. Anirban Dasgupta
