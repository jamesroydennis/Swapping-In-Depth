## Introduction

When I began using swapping technology, I was overwhelmed with the technology. There appeared to be 10 new technologies of which a hundred different settings. The spectrum was wide.

The purpose of this article is to share my experience and assist others who may be new to this technology. By providing a baseline of information, hopefully, you too can produce amazing results in short time.

As a disclaimer, my knowledge is limited to NVIDIA GPU's and CUDA technology.

Before we begin, I would like to note that I am using an older video card. GTX 1080TI. It is not necessary to have the latest and best video card but it is important to know that there are limitations, especially with VRAM. Here is a link to [my sysinfo](./supplements/mysysinfo.md).

---

## My Default Settings

Swapping encompasses 5 main features of note:
[See Swapping-In-Depth](./Swapping101.md) for detailed explanations.

### 1. 🔍 Detection

**RetinaFace**
It has a moderate angle tolerance, high clarity tolerance in regards to blur and occlusions. Its speed is moderate with high accuracy.
[See FaceDetectionOverview.md](./FaceDetectionOverview.md) for other options and in-depth explanations.

### 2. 🧠 Recognition

**InSwapper128ArcFace**
A lightweight model primarily focused on face-swapping, optimized for performance with a resolution of 128x128.

**Strength**:

* Solid choice for standard face-swapping tasks.
* Strong identity preservation thanks to the ArcFace embedding.

**Weakness for Extreme Close-ups**:

* May struggle with extreme close-ups, revealing texture issues and edge artifacts, especially around delicate features like eyes and hairlines.

**Best Use Case**:

* Works well for most regular face-swapping tasks at a reasonable distance.

[See FaceRecognitionOverview.md](./FaceRecognitionOverview.md) for other options and in-depth explanations.

### 3. 🧬 Parsing / Restoration

I use two:

**GFPGAN-v1.4**

* Alignment: Reference
* Fidelity Weight: \~0.3-0.5
* Blend: 30-50% (default)

**RestoreFormer++**

* Alignment: Blend
* Fidelity Weight: \~0.9
* Blend: \~40-80% (depending upon distance to subject)

[See FaceParsersOverview.md](./FaceParsersOverview.md) for other options and in-depth explanations.

### 4. 🎭 Composition & Swapping Logic

This can be a little tricky here because there are so many variables. In my default settings, I only concern myself with two settings:

* **Face Color Correction**: DFL\_Original
* **DFL\_XSeg\_Mask**: Enabled (default value of 0)

### 5. 🧭 Temporal Consistency & Tracking (Essential for Video)

I have nothing to add here yet.

---

## Challenges

Face-swapping is a multifaceted task with several challenges that can affect output quality. The three most common and impactful are motion, occlusion, and angle. Understanding these challenges helps in tuning your pipeline for better results.

### 🎞️ Motion

Fast movement can cause blur and reduce feature clarity, making it harder for models to detect and track faces accurately. The challenge of motion is best addressed by focusing on **detection**—choosing a detector that is robust to blur and frame-by-frame shifts.

[See FaceDetectionOverview.md](./FaceDetectionOverview.md)

### 🫣 Occlusion

Occlusions from hands, objects, or hair obscure facial features and confuse both recognition and restoration. In these cases, **parsing** and **restoration** are crucial, as they help recover or reconstruct hidden parts with contextual awareness.

[See FaceParsersOverview.md](./FaceParsersOverview.md)

### 📐 Angle

Variations in face orientation reduce the confidence and reliability of recognition models. **Recognition** engines that are angle-tolerant and capable of identity embedding across views will perform better.

[See FaceRecognitionOverview.md](./FaceRecognitionOverview.md)

---

## Summary

In summary, these settings are not for every situation but I found that it serves as a good baseline for subjects at normal distance, mild occlusions, and motion tolerance. Settings will have to be altered for subject distance and desired clarity. I hope you find this helpful.
