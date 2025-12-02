---
title: 'StoryForge AI Studio: Story-to-Video Generation Pipeline'
summary: '7-stage multilingual generative pipeline transforming keywords to complete videos using Llama 3, Stable Diffusion+LoRA, BLIP/CLIP, and MoviePy'
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
---

## Overview

StoryForge AI Studio is an end-to-end multilingual story-to-video generative pipeline that transforms simple keywords into complete multimedia experiences. The system integrates multiple state-of-the-art AI models to automatically generate stories, create consistent scene images, add audio narration, and compile everything into a final video—all through an intuitive Streamlit interface.

## Key Features

- **Multilingual Support**: Generate stories and audio in 7 languages (English, Hindi, French, German, Spanish, Italian, Telugu)
- **7-Stage Pipeline**: Keyword → Story → Prompts → Images → Consistency Check → Audio → Video
- **Modular Architecture**: 8+ core Python components for maintainability and extensibility
- **Interactive Studio**: Streamlit web interface for end-to-end generation in a single run
- **Automated Consistency**: BLIP/CLIP-based semantic and visual alignment checking
- **Complete Artifact Package**: Download story, prompts, images, audio, consistency report, and final MP4

## Technical Architecture

### Core Components

1. **Story Generation** (`story_generation.py`): 
   - Llama 3 via Ollama for creative story generation from keywords
   - Language-specific prompting for multilingual output

2. **Prompt Extraction** (`prompt_generator.py`):
   - Converts story into visually descriptive scene prompts
   - Maintains character and setting consistency across scenes

3. **Image Generation** (`image_generator.py`):
   - Stable Diffusion 2.1 with custom LoRA weights
   - SameFace_Fix LoRA for character consistency
   - Scene-by-scene image synthesis

4. **Consistency Checking** (`consistancy_check.py`):
   - BLIP for image captioning
   - CLIP for semantic similarity scoring
   - Evaluates prompt-image and story-image alignment

5. **Audio Narration** (`audio_generator.py`):
   - gTTS for multilingual text-to-speech
   - Automatic language detection and conversion

6. **Video Compilation** (`movie_creater.py`):
   - MoviePy for video assembly
   - Synchronized image transitions with audio narration
   - Multiple output formats (MP4, AVI)

7. **Streamlit Interface** (`streamlit.py`):
   - Real-time progress tracking
   - Individual component downloads
   - Complete package ZIP export

## Technical Stack

- **LLMs**: Llama 3 (via Ollama)
- **Image Generation**: Stable Diffusion, LoRA, VAE
- **Vision Models**: BLIP (captioning), CLIP (similarity)
- **Audio**: gTTS (Text-to-Speech)
- **Video**: MoviePy
- **Framework**: PyTorch, Transformers (HuggingFace)
- **UI**: Streamlit
- **Tools**: NumPy, Pandas, PIL, OpenCV

## Results & Performance

- Successfully generates coherent multi-scene stories from keyword input
- Achieves visual consistency across generated images through LoRA fine-tuning
- CLIP scores demonstrate strong semantic alignment (>25.0 average)
- Complete pipeline execution in minutes on GPU hardware
- Supports batch processing and customizable parameters

## Key Learnings

1. **Prompt Engineering**: Critical for consistent image generation across scenes
2. **LoRA Fine-tuning**: Significantly improved character face consistency
3. **Modular Design**: Enabled independent testing and optimization of each component
4. **Multimodal Integration**: Learned to synchronize text, image, and audio modalities
5. **User Experience**: Streamlit provided rapid prototyping for interactive AI applications

## Future Enhancements

- Add video-to-video generation for enhanced scene transitions
- Implement character customization through reference images
- Integrate more advanced TTS models (e.g., VITS, Tacotron)
- Support for longer stories with chapter-based generation
- Add style transfer and artistic filters

## Course Context

**Course**: ES667 - Deep Learning  
**Institution**: IIT Gandhinagar  
**Instructor**: Prof. Anirban Dasgupta  
**Duration**: January 2025 - April 2025  
**Team**: Collaborative project with 4 members

## Resources

- [GitHub Repository](https://github.com/AbhayVG/ES667-Deep-Learning-project)
- [Demo Video](#) (Coming soon)
- [Technical Report](#) (Coming soon)
