# Image-to-Video Agent - Requirements

## Overview
Produce commercial-level and authentic UGC videos; consume industry knowledge and per-video requirements.

## Features

1. Produce commercial-level and authentic UGC videos; consume industry knowledge and per-video requirements.
2. Two distinct modes from the start: "authentic UGC" and "professional commercial" (separate prompt sets and optionally models).
3. **Industry knowledge integration**: Collect information from Industry Knowledge Agent daily and promptly update video creation prompts if necessary (e.g., breaking news, trending topics).
4. **Video prompt template library**: Actively or passively build video prompt templates for different purposes:
   - Product showcasing
   - Influencer advertising in selfie style
   - Professional commercials
5. **Prompt engineering updates**: Obtain latest knowledge on prompt engineering and modify video prompts to optimize output for each video LLM (Runway, Pika, etc.).
6. **Input sources**: Accept inputs of:
   - Industry-specific knowledge from Industry Knowledge Agent
   - Additional specific video requirements for each video generation
   - Product photos from brand owners
7. Brand guidelines as input: logo placement, colors, "never show X," style do's and don'ts.
8. Pre-publish check: duration, aspect ratio, no policy-breaking text/imagery; optional human-review queue for first N videos per client.
9. Budgets or caps per client/campaign (e.g. max generations per month) for pricing and cost control.
10. Emotion tuning: AI-based tuning to evoke the right emotions for the audience (e.g. warm vs energetic).
11. Adaptive learning: learn from past video performance (views, engagement) and refine generation prompts over time.

## Integration Points
- Consumes: Industry Knowledge Agent, Brand guidelines, Product photos
- Outputs to: Media Management Agent
