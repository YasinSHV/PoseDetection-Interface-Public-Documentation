# Pose Detection Interface for Unity

<div align="center">

![Unity Badge](https://img.shields.io/badge/Unity-6%2B-blue?style=for-the-badge&logo=unity)
![Platform](https://img.shields.io/badge/Platform-Windows%20%7C%20macOS%20%7C%20Linux%20%7C%20Android-green?style=for-the-badge)
![License](https://img.shields.io/badge/License-Commercial-orange?style=for-the-badge)
![Version](https://img.shields.io/badge/Version-1.0.0-purple?style=for-the-badge)

**A comprehensive Unity package for real-time human pose detection using YOLO models**

[🚀 Quick Start](#quick-start) • [📺 Tutorials](https://www.youtube.com/channel/UC9FKvqtv8ye6HYoKBRTCeUw) • [💾 Download](#purchase-and-downloads)

![demo](https://github.com/user-attachments/assets/008341ac-ae8e-49df-8658-50366dcc2fc4)


</div>

---

## ✨ Features

<table>
<tr>
<td width="50%">

### 🎥 Input Sources
- **Webcam Support** - Real-time camera input
- **Video Files** - Process pre-recorded videos  
- **Playlist Management** - Batch processing capabilities

### 🔍 Detection & Analysis
- **Real-time Processing** - Optimized for live detection
- **Visual Feedback** - Built-in pose visualization
- **Performance Monitoring** - FPS tracking and analysis

</td>
<td width="50%">

### ⚡ Reliability & Control
- **Error Handling** - Comprehensive error recovery
- **Flexible Configuration** - Extensive customization options
- **Universal Compatibility** - Works with any COCO format model

### 🎯 Ready-to-Use
- **Pre-built Prefabs** - Drag-and-drop components
- **Example Scenes** - Working demonstrations
- **Pre-converted Models** - YOLOv11 ONNX models included
- **Practical Applications** - Squat counter and fitness tracking

</td>
</tr>
</table>

---

## 📋 Requirements

| Component | Specification |
|-----------|---------------|
| **Unity Version** | Unity 6 or later |
| **Dependencies** | Inference Engine (auto-managed) |
| **Platform** | Windows, macOS, Linux, Android |
| **Hardware** | Webcam (for real-time detection) |

---

## 🚀 Quick Start

### Real-time Webcam Detection

1. **Import** the package into your Unity project
2. **Drag** the `Pose Detection System` prefab into your scene
3. **Set** Input Type to "Webcam" in the inspector
4. **Press Play** to start real-time detection
5. **Watch** pose keypoints appear in real-time!

### Video File Detection

1. **Open** the `Video File Pose Detection` example scene
2. **Choose** a video file from the Sample Videos folder
3. **Press Play** to start video analysis

---

## 🎬 Example Scenes

| Scene | Purpose | Features |
|-------|---------|----------|
| **Real-time Detection** | Live webcam pose detection | Camera feed, keypoint visualization, FPS monitoring |
| **Video Processing** | Video file analysis | Playback controls, pose tracking, sample videos |
| **SquatCounter** | Fitness application demo | Real-time squat counting, form analysis, log feedback |

---

## 🧠 Included Models

Pre-converted YOLOv11 pose detection models in ONNX format:

| Model | Speed | Accuracy | Best For |
|-------|-------|----------|----------|
| **YOLOv11n-pose** | ⚡ Fastest | ✅ Good | Real-time applications |
| **YOLOv11s-pose** | 🏃 Fast | ✅✅ Better | Balanced performance |
| **YOLOv11m-pose** | 🚶 Moderate | ✅✅✅ High | Accuracy-focused |
| **YOLOv11l-pose** | 🐌 Slower | ✅✅✅✅ Highest | Maximum accuracy |

> **💡 Note:** Models are examples - package supports any COCO pose-segmentation format model!

---

## 🛠️ Configuration

### Switching Models

1. Select the GameObject with `PoseInferenceEngine` component
2. In Inspector, find the "Model Asset" field
3. Choose your desired model for your use case

### Basic Settings

```csharp
[Header("Detection Settings")]
public float confidenceThreshold = 0.5f;           // Minimum detection confidence
public float keypointVisibilityThreshold = 0.5f;   // Minimum keypoint visibility
public bool enablePoseValidation = true;           // Enable pose validation

[Header("Input Settings")]
public InputType inputType = InputType.Webcam;     // Webcam or VideoFile
public int targetWidth = 640;                      // Frame width
public int targetHeight = 480;                     // Frame height

---
```

## 💻 Usage Examples

### Basic Pose Detection

```csharp
public class PoseDetectionExample : MonoBehaviour
{
    public PoseDetectionController poseController;
    
    void Start()
    {
        // Subscribe to pose detection events
        poseController.OnPosesDetected += OnPosesDetected;
        
        // Start detection
        poseController.StartDetection();
    }
    
    void OnPosesDetected(DetectedPose[] poses)
    {
        foreach (var pose in poses)
        {
            Debug.Log($"Detected pose with confidence: {pose.overallConfidence:F2}");
            
            // Access specific keypoints
            var nose = pose.GetKeyPoint(DetectedPose.KeypointType.Nose);
            if (nose != null && nose.isVisible)
            {
                Debug.Log($"Nose position: {nose.position}");
            }
        }
    }
}
```
---

## 🏃‍♂️ COCO Pose Keypoints

Supports all 17 COCO pose keypoints:

<table>
<tr>
<td width="33%">

**Head & Face**
- Nose (0)
- Left/Right Eye (1,2)
- Left/Right Ear (3,4)

</td>
<td width="33%">

**Upper Body**
- Left/Right Shoulder (5,6)
- Left/Right Elbow (7,8)
- Left/Right Wrist (9,10)

</td>
<td width="33%">

**Lower Body**
- Left/Right Hip (11,12)
- Left/Right Knee (13,14)
- Left/Right Ankle (15,16)

</td>
</tr>
</table>

---

## ⚡ Performance Optimization

### Model Selection Guidelines

| Application | Model | Desktop FPS | Mobile FPS | Use Case |
|------------|-------|-------------|------------|----------|
| **Games** | YOLOv11n-pose | 30+ | 15+ | Interactive apps |
| **General** | YOLOv11s-pose | 15-30 | 10-15 | Balanced performance |
| **Analysis** | YOLOv11m-pose | 10-15 | 5-10 | Accuracy-focused |
| **Research** | YOLOv11l-pose | 5-10 | 2-5 | Maximum precision |

### Android Optimization

```csharp
// Recommended mobile settings
public int androidTargetWidth = 480;
public int androidTargetHeight = 320;
public float androidProcessingInterval = 0.2f; // 5 FPS
```

---
## 🔧 API Reference

### DetectedPose Class

```csharp
public class DetectedPose
{
    public PoseKeyPoint[] keypoints;        // 17 COCO keypoints
    public float overallConfidence;         // Overall pose confidence
    public Rect boundingBox;                // Bounding box
    public DateTime timestamp;              // Detection timestamp
    
    // Key Methods
    public PoseKeyPoint GetKeyPoint(KeypointType type);
    public bool IsKeypointVisible(KeypointType type);
    public bool IsValidPose();
}
```

### Events

csharp
// Main Events
public event Action<DetectedPose[]> OnPosesDetected;
public event Action<string> OnSystemError;
public event Action<Texture2D> OnFrameReady;

---

## 🔍 Troubleshooting

| Problem | Quick Fix |
|---------|-----------|
| **"Model not assigned"** | Select a model from Models folder in PoseInferenceEngine |
| **"No camera found"** | Check permissions, try different camera indices |
| **Poor performance** | Switch to YOLOv11n-pose, reduce resolution |
| **Android issues** | Use IL2CPP backend, ARM64 architecture |

---

## 💰 Purchase & Get Full License

<div align="center">

**Available for $12.99**

[![Itch.io](https://img.shields.io/badge/itch.io-Buy%20Now-red?style=for-the-badge&logo=itch.io)](https://mrfreshey.itch.io/yolo-pose-detection-interface)
[![Unity Asset Store](https://img.shields.io/badge/Unity%20Asset%20Store-Coming%20Soon-blue?style=for-the-badge&logo=unity)](https://assetstore.unity.com)

*Full commercial license, source code, and models included with purchase*

### 🎓 Individual Developer Support
**Can't afford the package?** Email me at **yshabaniv@gmail.com** - I help developers individually with free/discounted access. Supporting the dev community! 

</div>

---

## 📚 Resources and Support


### 🤝 Community & Support
- **Issues**: Report bugs and feature requests
- **Discussions**: Community help and showcase
- **Email**: Direct developer support

---

<div align="center">

**Version 1.0.0** | **Unity 6+** | **2025**

Created with ❤️ by [MrFreshey]([https://www.youtube.com/mrfreshey](https://www.youtube.com/channel/UC9FKvqtv8ye6HYoKBRTCeUw))

</div>
