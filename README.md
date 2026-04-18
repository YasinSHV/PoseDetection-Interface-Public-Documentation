# Pose Detection Interface for Unity

<div align="center">

![Unity Badge](https://img.shields.io/badge/Unity-6%2B-blue?style=for-the-badge&logo=unity)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux%20%7C%20Android-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-Commercial-orange?style=for-the-badge)
![Version](https://img.shields.io/badge/Version-2.0.0-purple?style=for-the-badge)

**A comprehensive Unity package for real-time human pose detection using YOLO / PoseNet ONNX models**

[🚀 Quick Start](#-quick-start) • [📺 Tutorials](https://www.youtube.com/channel/UC9FKvqtv8ye6HYoKBRTCeUw) • [💾 Download](#-purchase--get-full-license) • [🆕 What's New in v2](#-whats-new-in-v2)

![demo](https://github.com/user-attachments/assets/008341ac-ae8e-49df-8658-50366dcc2fc4)

</div>

---

## 🆕 What's New in v2

v2 is a major accuracy + tooling release.

### Accuracy
- **Letterbox preprocessing** — aspect-preserving resize with gray padding. No more squashed detections when your camera isn't square.
- **Inverse coordinate mapping** — keypoints come back in source-frame pixels regardless of letterbox padding.
- **Test-time horizontal-flip augmentation** — runs a mirrored pass and averages keypoints (with anatomical L/R swap) for cleaner results on ambiguous poses.
- **Per-keypoint confidence floors** — tighten face/ear gates independently from body gates.
- **OKS (Object Keypoint Similarity) NMS** — COCO-standard duplicate suppression, sharper than bbox-IoU.
- **Normalization modes** — Unit01 / Byte255 / ImageNet declarative choice.

### Multi-person tracking
- **Augmented Hungarian matching** — cost combines torso distance + bbox-IoU + OKS + velocity alignment + optional appearance ReID.
- **Constant-velocity predictor** — tracks coast through short occlusions before being dropped.
- **Tentative → Confirmed state machine** — `trackingId` only appears on tracks that survive `minHitsToConfirm` frames, killing flicker.
- **`IPoseReidProvider` hook** — plug in your own embedding network for appearance-based re-identification.

### Tooling
- **Editor menu scaffolds** under `GameObject → Pose Detection → …` — one-click systems, example bolt-ons, and demo-scene setups with auto-assigned models.
- **PoseReplayer** — standalone offline playback of recorded JSON. No camera, no model, no controller needed.
- **Timeline integration** — drive a `PoseReplayer` from a Timeline track for deterministic demos and cutscenes.
- **Virtual gesture input device** — gestures exposed as bindable Input System buttons (`<PoseGesture>/tPose`, `/handsUp`, …).
- **Pose Live Comparison** — compare live poses to a reference clip.

### Removed
- Humanoid IK driver has been removed for scope clarity; projection-without-depth is better handled by a dedicated tool.

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🎥 Input Sources
- **Webcam** — real-time camera input
- **Video Files** — process pre-recorded videos with playlist, looping, keyboard navigation
- **Offline Replay** — JSON pose recordings play without a camera or model

### 🔍 Detection & Analysis
- **Real-time Processing** — GPU-compute or CPU inference via Unity Inference Engine 2.4
- **Multi-person Tracking** — persistent IDs via augmented Hungarian matching
- **Temporal Smoothing** — OneEuroFilter per track, per keypoint
- **OKS NMS + Per-keypoint Thresholds** — COCO-grade filtering
- **Visual Feedback** — screen-space UI overlay with confidence colouring
- **Performance Monitoring** — FPS, per-stage Profiler markers

</td>
<td width="50%">

### ⚡ Reliability & Control
- **Inference cancellation** — swap models mid-run without stale callbacks
- **Letterbox-safe coordinates** — keypoints always in source-frame pixels
- **Flexible Configuration** — every knob in the Inspector
- **Input System integration** — gestures as bindable actions

### 🎯 Ready-to-Use
- **One-click Scaffolding** — GameObject menu builds a working system
- **Six Example Scenes** — Real-time, Video, SquatCounter, PoseRecorder, GestureDetector, StanceEstimator, PoseReplayer
- **Pre-converted Models** — PoseNet-v2 family + YOLOX-m HumanArt included
- **Timeline Track** — scrub recorded poses in a Timeline

</td>
</tr>
</table>

---

## 📋 Requirements

| Component | Specification |
|-----------|---------------|
| **Unity Version** | Unity 6000.3.7f1 or later |
| **Render Pipeline** | URP 17.3.0 (samples built for URP) |
| **Dependencies** | Unity AI Inference 2.4.1, Input System 1.18, Timeline 1.8.10 (auto-managed) |
| **Platform** | Windows, macOS, Linux, Android |
| **Hardware** | Webcam (for real-time), GPU recommended |

---

## 🚀 Quick Start

### One-click setup (recommended)

1. **Import** the package into your Unity project
2. In the Hierarchy, right-click → **Pose Detection → Create Pose Detection System**
3. Press **Play** — webcam opens, skeleton overlay appears on any detected person

The scaffold auto-assigns a bundled ONNX model. Switch models in the `PoseInferenceEngine` Inspector.

### Add feature components

With the system selected, use **GameObject → Pose Detection → Add →**
- Squat Counter • Gesture Detector • Stance Estimator
- Pose Recorder • Pose Live Comparison • Gesture Input Driver

### Prefab setup

1. Drag the `Pose Detection System` prefab into your scene
2. Set **Input Type** on `PoseInputHandler` (Webcam / VideoFile)
3. Press **Play**

### Video file detection

1. Open `Example Scenes/VideoInputPoseDetectionScene.unity`
2. Drop videos into the playlist on `PoseInputHandler`
3. Press Play — use `[` / `]` to navigate, `P` to pause

---

## 🎬 Example Scenes

| Scene | Purpose |
|-------|---------|
| **RealtimePoseDetectionScene** | Live webcam pose detection |
| **VideoInputPoseDetectionScene** | Video file / playlist analysis |
| **SquatCounterExample** | Fitness demo — rep counting via knee-angle phase tracking |
| **PoseRecorder** | Record live poses to JSON; in-editor scrub + step + speed controls |
| **PoseReplayer** | Offline playback of a recorded JSON — no camera / model needed |
| **GestureDetector** | T-pose, hands-up, arms-crossed, wave — polled or bound as Input actions |
| **StanceEsitmator** | Body stance and balance analysis |

---

## 🧠 Included Models

| Model | Format | Speed | Accuracy | Best For |
|-------|--------|-------|----------|----------|
| **PoseNet-Nano-v2** | ONNX | ⚡ Fastest | ✅ Good | Mobile / real-time |
| **PoseNet-Small-v2** | ONNX | 🏃 Fast | ✅✅ Better | Balanced |
| **PoseNet-Medium-v2** | ONNX | 🚶 Moderate | ✅✅✅ High | Desktop real-time |
| **PoseNet-Large-v2** | ONNX | 🐌 Slower | ✅✅✅✅ Very high | Accuracy-focused |
| **PoseNet-XLarge-v2** | ONNX | 🐢 Slowest | ✅✅✅✅✅ Highest | Offline analysis |
| **yolox-m-humanart** | ONNX | 🚶 Moderate | ✅✅✅✅ High | Stylised / art input |

> The parser auto-detects output shape and branches between **End-to-End `[1, N, 57]`** and **Anchor-based `[1, 56, N]`** layouts — any COCO 17-keypoint model in either form will work.

---

## 🛠️ Configuration

### Switching Models

1. Select the GameObject with `PoseInferenceEngine`
2. In the Inspector, assign a `.onnx` to **Model Asset**
3. The format is auto-detected; check the Console for a one-line confirmation

### Core settings

```csharp
// On PoseInferenceEngine
public ModelAsset modelAsset;
public Vector2Int modelInputSize = new(640, 640);
public bool useLetterbox = true;
public ImageNormalization normalization = ImageNormalization.Unit01;
public bool horizontalFlipTTA = false;   // accuracy boost at 2x cost

// On PoseInferenceEngine.parserSettings (PoseParserSettings)
public float confidenceThreshold = 0.5f;
public float keypointVisibilityThreshold = 0.5f;
public bool  enablePoseValidation = true;
public int   minVisibleKeypoints = 3;
public NmsMode nmsMode = NmsMode.OKS;     // or BboxIoU
public float nmsOksThreshold = 0.5f;
public float[] perKeypointConfidenceThresholds; // length 17

// On PoseInputHandler
public InputType inputType = InputType.Webcam;
public int targetWidth = 640;
public int targetHeight = 480;
public int targetFPS = 30;
```

---

## 💻 Usage Examples

### Basic pose detection

```csharp
using PoseDetection.Controller;
using PoseDetection.Data;
using UnityEngine;

public class PoseDetectionExample : MonoBehaviour
{
    public PoseDetectionController poseController;

    void Start()
    {
        poseController.OnPosesDetected += OnPosesDetected;
        poseController.StartDetection();
    }

    void OnPosesDetected(DetectedPose[] poses)
    {
        foreach (var pose in poses)
        {
            Debug.Log($"Pose {pose.trackingId}: conf {pose.overallConfidence:F2}");

            var nose = pose.GetKeyPoint(KeypointId.Nose);
            if (nose != null && nose.isVisible)
                Debug.Log($"Nose at {nose.position}");

            // Joint angles (returns 0 if any input is below the confidence gate)
            float kneeAngle = pose.GetAngle(KeypointId.LeftHip, KeypointId.LeftKnee, KeypointId.LeftAnkle);
            if (kneeAngle > 0) Debug.Log($"Left knee: {kneeAngle:F0}°");
        }
    }
}
```

### Offline replay (no camera)

```csharp
using PoseDetection.Examples;

public class ReplayExample : MonoBehaviour
{
    public PoseReplayer replayer;

    void Start()
    {
        replayer.OnPosesReplayed += poses => {
            // same DetectedPose[] you'd get live
        };
        replayer.Play();
    }
}
```

### Gesture as Input System action

```csharp
// 1. In PlayerInputActions, bind a Button action to "<PoseGesture>/tPose"
// 2. In scene: add GestureDetector + GestureInputDriver to your system
// 3. Treat it like any other input

void OnTPose(InputValue value) { if (value.isPressed) Debug.Log("T-Pose!"); }
```

---

## 🏃‍♂️ COCO 17-Keypoint Layout

<table>
<tr>
<td width="33%">

**Head & Face**
- Nose (0)
- Left / Right Eye (1, 2)
- Left / Right Ear (3, 4)

</td>
<td width="33%">

**Upper Body**
- Left / Right Shoulder (5, 6)
- Left / Right Elbow (7, 8)
- Left / Right Wrist (9, 10)

</td>
<td width="33%">

**Lower Body**
- Left / Right Hip (11, 12)
- Left / Right Knee (13, 14)
- Left / Right Ankle (15, 16)

</td>
</tr>
</table>

Access via `KeypointId` (top-level enum): `pose.GetKeyPoint(KeypointId.LeftWrist)` or indexer `pose[KeypointId.LeftWrist]`.

---

## ⚡ Performance Optimization

### Model selection guidelines

| Application | Model | Desktop FPS | Mobile FPS |
|------------|-------|-------------|------------|
| **Games / interactive** | PoseNet-Nano-v2 | 60+ | 20+ |
| **Balanced** | PoseNet-Small-v2 | 30-60 | 10-15 |
| **Accuracy-focused** | PoseNet-Medium-v2 | 20-30 | 5-10 |
| **Offline analysis** | PoseNet-Large / XLarge | 10-20 | n/a |

### Android / mobile

```csharp
// On PoseInputHandler
targetWidth  = 480;
targetHeight = 320;
// On PoseDetectionController
processingInterval = 0.1f;  // 10 FPS
```

Prefer IL2CPP + ARM64. Disable `horizontalFlipTTA` on mobile — it doubles inference cost.

### Profiler markers

Instrumented for Unity Profiler / Profile Analyzer:
- `PoseDetection.Inference.{PrepareInput, Schedule, Readback, Parse, Smooth}`
- `PoseDetection.Parser.{EndToEnd, AnchorBased, NMS}`
- `PoseDetection.Smoother.{Smooth, Match}`

---

## 🔧 API Reference

### DetectedPose

```csharp
public class DetectedPose
{
    public const int KeypointCount = 17;
    public PoseKeyPoint[] keypoints;        // length 17, indexed by KeypointId
    public float overallConfidence;
    public Rect boundingBox;
    public DateTime timestamp;
    [NonSerialized] public int trackingId;  // set by PoseSmoother (-1 = unconfirmed)

    public PoseKeyPoint this[KeypointId id] { get; }
    public PoseKeyPoint GetKeyPoint(KeypointId id);
    public bool TryGetKeypoint(KeypointId id, out PoseKeyPoint kp, float minConfidence = 0f);
    public bool IsKeypointVisible(KeypointId id);
    public bool IsValidPose(int minVisibleKeypoints = 3);
    public int  CountAboveConfidence(float minConfidence);

    public float   GetAngle(KeypointId a, KeypointId vertex, KeypointId c, float minConfidence = 0.5f);
    public Vector2 GetTorsoCenter(float minConfidence = 0.3f);
    public float   GetShoulderWidth(float minConfidence = 0.5f);
    public float   GetHipWidth(float minConfidence = 0.5f);
    public float   GetBodyHeight(float minConfidence = 0.3f);
}
```

### PoseKeyPoint

```csharp
public class PoseKeyPoint
{
    public Vector2 position;    // source-frame pixels
    public float   confidence;
    public bool    isVisible;   // confidence > visibilityThreshold
    public bool    Meets(float minConfidence);
}
```

### Coordinate conversions (extensions)

```csharp
kp.ToNormalized(frameW, frameH);
kp.ToScreen(frameW, frameH);
kp.ToWorldRay(camera, frameW, frameH);
kp.TryProjectOntoPlane(camera, frameW, frameH, plane, out Vector3 worldPos);
kp.TryProjectOntoGround(camera, frameW, frameH, groundY, out Vector3 worldPos);

foreach (var (id, kp) in pose.VisibleKeypoints(minConfidence: 0.5f)) { … }
```

### Events

```csharp
// PoseDetectionController
public event Action<DetectedPose[]> OnPosesDetected;
public event Action<string>         OnSystemError;

// PoseInputHandler
public event Action<Texture2D> OnFrameReady;
public event Action<string>    OnInputError;
public event Action<VideoFile> OnVideoFileLoaded;

// PoseReplayer (offline)
public event Action<DetectedPose[]> OnPosesReplayed;
public event Action OnPlaybackStarted;
public event Action OnPlaybackFinished;
```

### Tracking hook (custom ReID)

```csharp
public interface IPoseReidProvider
{
    // Return a cost in [0, 1] describing how dissimilar the pose is to the track's prior appearance.
    float GetReidCost(DetectedPose candidate, int trackingId);
}
```

---

## 🔍 Troubleshooting

| Problem | Fix |
|---------|-----|
| **"Model asset not assigned"** | Assign an `.onnx` to `PoseInferenceEngine.modelAsset`, or use **GameObject → Pose Detection → Create Pose Detection System** (auto-assigns) |
| **"No camera found"** | Grant camera permission; try another `cameraIndex` on `PoseInputHandler` |
| **Squashed / shifted keypoints** | Ensure `useLetterbox = true`; confirm your model's expected input size matches `modelInputSize` |
| **rtmw3d-x doesn't work** | Known — it's a 3D model; the bundled parser only decodes 2D COCO output |
| **Poor FPS on mobile** | Switch to PoseNet-Nano-v2, lower `targetWidth/Height`, raise `processingInterval` |
| **Detection flickers ID** | Increase `minHitsToConfirm` on `PoseSmoother`; raise `maxCoastingMisses` for occlusion tolerance |
| **Video won't loop** | Turn on `loopPlaylist`; for single-video scenes it uses native `VideoPlayer.isLooping` |

---

## 💰 Purchase & Get Full License

<div align="center">

**Available for $12.99**

[![Itch.io](https://img.shields.io/badge/itch.io-Buy%20Now-red?style=for-the-badge&logo=itch.io)](https://mrfreshey.itch.io/yolo-pose-detection-interface)
[![Unity Asset Store](https://img.shields.io/badge/Unity%20Asset%20Store-Coming%20Soon-blue?style=for-the-badge&logo=unity)](https://assetstore.unity.com)

*Full commercial license, source code, and models included.*

### 🎓 Individual Developer Support
**Can't afford it?** Email **yshabaniv@gmail.com** — I offer free / discounted access for students and indie devs.

</div>

---

## 📚 Resources & Support

- **Issues**: bugs and feature requests
- **Discussions**: community help and showcase
- **Email**: direct developer support

---

<div align="center">

**Version 2.0.0** | **Unity 6+** | **2026**

Created by [MrFreshey](https://www.youtube.com/channel/UC9FKvqtv8ye6HYoKBRTCeUw)

</div>
