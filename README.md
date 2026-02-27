Below is a professional **README.md** draft tailored to your repository **AI-Generated-Singing-MV-Production**.
It is structured for academic + technical audiences and aligned with your published paper.

---

# AI-Generated-Singing-MV-Production

A reproducible workflow for AI-generated singing music video (MV) production using image-to-video synthesis and deterministic FFmpeg-based synchronization.

This repository accompanies the paper:

**“A Reproducible Workflow for AI-Generated Singing MV Production – Using Image-to-Video Synthesis and FFmpeg-Based Expression Overlay”**
Hung-Che Shen, I-Shou University, Taiwan

---

## Overview

This project proposes a lightweight and modular pipeline for producing AI-generated singing MVs without requiring:

* 3D character rigging
* Neural lip-sync training
* GPU-intensive inference
* Audio-driven facial animation models

Instead, the workflow combines:

1. AI character image generation
2. Image-to-video singing motion synthesis
3. BPM-based deterministic segmentation
4. FFmpeg concatenation and overlay
5. External singing synthesis (UTAU) integration

The demonstration example uses the children's song
**“Two Tigers” (兩隻老虎)** at **80 BPM**.

---

## Key Features

* Deterministic beat-aligned synchronization
* Romanized Mandarin (Hanyu Pinyin) prompt strategy
* Modular 6-second segment design
* Fully reproducible FFmpeg command pipeline
* Public release of prompts, MIDI, and audio assets

This repository emphasizes **engineering reproducibility** rather than neural architecture innovation.

---

## Workflow Summary

### Stage 1 — Musical Timing Model

* Time signature: 4/4
* Tempo: 80 BPM
* Beat duration: 0.75 seconds
* Phrase duration: 6 seconds (2 measures)

Each MV segment is generated independently to prevent cumulative drift.

---

### Stage 2 — AI Character Generation

A neutral half-body singer portrait is generated using an image model
(e.g., Grok Imagine).

Output:

```
character_base.png
```

---

### Stage 3 — Image-to-Video Singing Synthesis

Each 6-second phrase is generated independently using Romanized lyrics.

Example (Segment A):

```
liang zhi lao hu liang zhi lao hu
```

Outputs:

```
segment_A_6s.mp4
segment_B_6s.mp4
segment_C_6s.mp4
segment_D_6s.mp4
```

---

### Stage 4 — Segment Concatenation (FFmpeg)

Create list.txt:

```
file 'segment_A_6s.mp4'
file 'segment_B_6s.mp4'
```

Run:

```
ffmpeg -f concat -safe 0 -i list.txt -c copy 兩隻老虎_12s.mp4
```

---

### Stage 5 — Remove Embedded Audio

```
ffmpeg -i 兩隻老虎_12s.mp4 -c copy -an 兩隻老虎_12s_silent.mp4
```

---

### Stage 6 — Merge UTAU Singing Voice

```
ffmpeg -i 兩隻老虎_12s_silent.mp4 -i 兩隻老虎.wav \
-c:v copy -c:a aac -shortest 兩隻老虎.mp4
```

Final output:

```
兩隻老虎.mp4
```

---

## Repository Structure

```
AI-Generated-Singing-MV-Production/
│
├── musical_data/
│   ├── 兩隻老虎.MIDI
│   ├── 兩隻老虎歌詞.txt
│   └── 兩隻老虎.wav
│
├── visual_assets/
│   ├── character_base.png
│   ├── segment_A_6s.mp4
│   ├── segment_B_6s.mp4
│   ├── segment_C_6s.mp4
│   └── segment_D_6s.mp4
│
├── prompts/
│   ├── prompt_character.txt
│   ├── prompt_segment_A.txt
│   ├── prompt_segment_B.txt
│   ├── prompt_segment_C.txt
│   └── prompt_segment_D.txt
│
└── README.md
```

---

## Reproducibility Principles

This project ensures reproducibility through:

* Fixed BPM mathematical timing model
* Independent short-segment generation
* Explicit FFmpeg commands
* Archived prompt documentation
* Public musical reference files

The pipeline converts inherently stochastic AI generation into a partially deterministic multimedia production workflow.

---

## Limitations

* Lip motion is singing-like but not phoneme-accurate
* No pitch-dependent mouth morphology
* Expression is prompt-driven, not acoustically analyzed
* Output stability may vary across platform updates

---

## Future Directions

* Automated syllable-to-beat alignment
* Phoneme-level articulation correction
* Pitch-informed visual modulation
* Hybrid integration with neural lip-sync systems
* Quantitative synchronization evaluation

---

## Citation

If you use this repository in academic work, please cite:

Shen, H.-C. (2026).
*A Reproducible Workflow for AI-Generated Singing MV Production – Using Image-to-Video Synthesis and FFmpeg-Based Expression Overlay.*

---

## License

This repository is released for research and educational purposes.
Please ensure proper attribution when reusing assets or workflow concepts.

---

If you would like, I can also provide:

* A shorter GitHub-style README (more practical, less academic)
* A more research-oriented README matching IEEE tone
* A version formatted specifically for journal artifact review submission
* A bilingual (English + Chinese) README version
