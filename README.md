# Hi, I'm Syed Hamza Mohiuddin 👋
### Computer Vision Engineer | Systems & Edge AI

I am an algorithmic and systems-focused Computer Vision Engineer with a holistic grasp of the vision stack. My expertise bridges the gap between classical computer vision techniques (image processing, geometric reasoning, and tracking), deep learning architectures, and high-performance production pipelines: from custom training loops and multi-process system design to model optimization and edge deployment (TensorRT, Qualcomm AI Hub, ONNX, TFLite).

---

### 🏆 Key Highlights
*   **IEEE LPCVC 2026 (CVPR Workshop) – Track 2:** Ranked **8th/38 globally** in Video Action Recognition. Optimized R2+1D for Qualcomm Dragonwing IQ-9075 under a strict <34ms latency budget, overcoming severe class imbalance and label noise through rigorous data auditing.
*   **IEEE LPCVC 2026 (CVPR Workshop) – Track 1:** Ranked **12th/56 globally** in Open-World Retrieval. Optimized MobileCLIP/ViT-B/16 for Qualcomm XR2 Gen 2, engineering a custom model wrapper to resolve tokenizer discrepancies (Causal vs. Bidirectional) for on-device inference.
*   **High-Performance Systems Architecture:** Redesigned a monolithic, single-process 30 FPS dual-camera pipeline into a **4-process parallel architecture** using Zero-Copy IPC (`multiprocessing.shared_memory`) and OpenCV-CUDA. Achieved **over 3x throughput (30 → 100+ FPS per camera stream)** by resolving GUI latency and CPU-bound preprocessing bottlenecks.
---

### 🛠️ Core Expertise

*   **Systems Architecture & Optimization:** High-Performance Multiprocessing, Zero-Copy IPC (Shared Memory), GPU Acceleration (OpenCV-CUDA), TensorRT, Qualcomm AI Hub (QNN), ONNX, INT8 Quantization, Structured Pruning.
*   **Deep Learning & DL-based CV:** Object Detection (YOLO v5-v11), Segmentation (U-Net), Tracking (ByteTrack, TransReID), Pose Estimation, Vision Transformers (ViT/VLMs), ReID, Video Action Recognition (Temporal Modeling), Multi-modal Retrieval (CLIP, MobileCLIP).
*   **Classical & Algorithmic CV:** Image Processing (Morphology, CLAHE, Canny, Contours), Geometric Reasoning (Zhang's Calibration, Homography, ArUco, `scipy.optimize`), Tracking (Kalman Filtering, Optical Flow, Background Subtraction).
*   **Languages & Tools:** Python (Expert), PyTorch, TensorFlow, C++ (CUDA Certified), Netron Model Surgery, Reverse Engineering, Model Benchmarking (`clip_benchmark`).

---

## 💼 Experience

*   **Swift Vision Pvt. Ltd.** | Computer Vision Intern → Computer Vision Engineer → Computer Vision Research Engineer | Apr 2025 - Jan 2026
    *(Promoted to R&D ownership within 4 months based on execution and technical leadership).*
*   **Folio3 Pvt. Ltd.** | AI Intern | July 2023 - Sep 2023

---

## 🚀 Featured Projects

### High-Performance Multi-Camera Vision Pipeline (30 FPS → 100+ FPS)
*   **Role:** Lead Systems Architect (Swift Vision)
*   **Challenge:** Client's monolithic 30 FPS dual-camera sports analytics system was bottlenecked by sequential CPU-bound processing and OpenCV GUI latency. The client initially misdiagnosed the issue as a model inference problem.
*   **Solution:**
    *   Diagnosed the architectural flaw and argued against the TensorRT misdiagnosis.
    *   Redesigned the system into a **4-process parallel architecture**: two camera logic processes (GPU preprocessing + YOLO inference), an update/state loop, and a main GUI process.
    *   Implemented **Zero-Copy IPC** using `multiprocessing.shared_memory` to eliminate data copying overhead.
    *   Offloaded all image preprocessing (resize, warp, blur, dilation) to **OpenCV-CUDA**.
*   **Result:** Achieved **over 3x throughput (30 → 100+ FPS per stream, with peaks near 120)** and 120 FPS GUI rendering. Received direct praise from the client for the architectural solution.

### IEEE LPCVC 2026 (CVPR Workshop) – Track 2: Video Action Recognition
*   **Result:** Ranked **8th/38 globally**.
*   **Challenge:** 92-class fitness video dataset with severe class imbalance (some classes <150 examples) and significant label noise.
*   **Solution & Approach:** Modified the training pipeline to log per-class train/val accuracy and individual misclassifications, manually auditing 4,500+ problematic instances. Designed 7 separate augmentation and cropping strategies based on class-specific confusion analysis. Diagnosed a Qualcomm hardware compiler tiling failure and pivoted to a 16-frame architecture to meet a <34ms latency budget.
*   **Outcome:** Improved accuracy from 91.44% to **93.24%** through rigorous data curation and training rule refinement.

---

## 🔧 Open Source: Ultralytics YOLO

- **[TensorRT validation fix (PR #21592, merged)](https://github.com/ultralytics/ultralytics/pull/21592)** — Root-caused a `yolo val` failure on TensorRT `.engine` models (the validator read a `batch_size` attribute that `AutoBackend` never set) and worked through maintainer review; the merged fix simplified the validator's batch-size logic.
- **Structured Pruning Engine ([PR #21977](https://github.com/ultralytics/ultralytics/pull/21977), [docs PR #22438](https://github.com/ultralytics/ultralytics/pull/22438))** — Native PyTorch structured pruning for YOLOv8 detection models.
  - Global ratio or per-layer YAML configuration; norm-based channel importance; mask propagation through Conv, BatchNorm, Bottleneck, C2f, SPPF, Concat and both Detect-head towers; group-aware handling of grouped/depthwise convolutions (the reason `torch.nn.utils.prune` wasn't enough).
  - ~1,000 lines of pruning code plus a 1,400-line test suite (43 test functions) covering the prune → save → load → retrain → ONNX export round trip.
  - Functional demo (YOLOv8s, COCO128, ONNX): 22.6 → 11.6 MB (~49% smaller), 17.1 → 12.0 ms (~30% faster). A demonstration that the pipeline works end to end, not an accuracy benchmark; retraining is needed to recover accuracy.
  - **Status:** scoped with maintainer guidance, CI green and branch up to date; both PRs were closed by the stale bot before code review. Code is on my fork: [`feature/prune-functionality`](https://github.com/syedhamzamohiuddin/ultralytics/tree/feature/prune-functionality) and [`docs/pruning`](https://github.com/syedhamzamohiuddin/ultralytics/tree/docs/pruning).

---

## Paper Implementations
*Reimplemented from the original papers, first principles.*

- **[Transformer (Attention Is All You Need)](https://github.com/syedhamzamohiuddin/-attention-is-all-you-need-tf2)** — Complete preprocessing and training pipeline, shared source-target vocabulary, byte-pair encoding, three-way weight tying, padding and causal masking, full encoder-decoder architecture.
- **[U-Net (Biomedical Segmentation)](https://github.com/syedhamzamohiuddin/unet-paper-reimplementation)** — Pixel-wise weight maps and elastic deformation, optimized for TPU-accelerated training using a TFRecord-based data pipeline.

## Other Projects

- **[Real-Time Liquid Quality Inspection](https://youtu.be/5do-AtpkTUM?si=XikSNckEzyWQqK-J)** — Automated inspection pipeline for transparent bottles on a conveyor using backlit imaging; morphological segmentation, CLAHE, Canny edge detection, contour analysis, and Kalman filter tracking.
- **[Clinical Caries Detection](https://www.kaggle.com/code/hamzamohiuddin/accelerate-q2)** — Customized U-Net for dental radiography segmentation, high-precision boundary detection.
- **[Traffic Analytics Pipeline](https://youtu.be/JATXilb1hpE?si=_Rk7b4cddlDuh2yi)** — Automated traffic analysis using optical flow, thresholding, and multi-object tracking (MOT) to monitor vehicle flow and density.
- **[Deep Probabilistic Generative Models](https://github.com/syedhamzamohiuddin/Probabilistic-Deep-Learning-with-TensorFlow-2/tree/main)** — VAEs for facial generation and RealNVP (Normalizing Flows) for high-dimensional image synthesis on LSUN.
- **[Bayesian CNN (Uncertainty Quantification)](https://github.com/syedhamzamohiuddin/Probabilistic-Deep-Learning-with-TensorFlow-2/tree/main/Bayesian%20convolutional%20neural%20network)** — Captures aleatoric and epistemic uncertainty in digit classification, beyond point-estimate predictions.
- **[Bayesian Earthquake Forecasting](https://github.com/syedhamzamohiuddin/bayesian-earthquake-forecast)** — Bayesian AR(3) model in R for global seismic activity: model order selection, posterior inference, prior sensitivity, mixture AR model comparison..

---

## 🎥 Video Demonstrations
A collection of visual demos from early project work showcasing classical CV, tracking, and basic detection pipelines.

*   **[View the full project demo playlist on YouTube](https://youtube.com/playlist?list=PLD8EMsAPSIFU&si=bhKIj5HZEZy_5NhT)** 
    *(Includes: Water Quality Inspection, Vehicle Detection, Pose Estimation, Pedestrian Tracking, Multi-Car Tracking, Liquid Fill Estimation, and more).*

---

## 📖 Technical Foundations & Learning Roadmap

*   **Foundational Exposure:** Studied early chapters of Hartley & Zisserman's *Multiple View Geometry* to understand the mathematical principles behind production geometry tasks.
*   **Applied Practice:** Translated these geometric foundations into working code, including Zhang's planar calibration and marker-aware ArUco rectification using `scipy.optimize`.
*   **Current Learning Focus:** Currently building depth in Kalman Filtering and C++ for high-performance geometric vision. 
*   **Upcoming Study Plan:** Next steps include 3D vision libraries (PCL) and advanced coursework (CS231A) to deepen 3D perception expertise.

---

## 🎓 Education

*   **BS Computer Science** | IBA Karachi *(Best Paper Nomination, ICETST 2022)*

---

## Certifications & Coursework

<details>
<summary>Click to expand — 13 certifications across ML theory, CV, and deep learning</summary>

**Core Certifications**
- [Google TensorFlow Developer Certificate](https://www.credential.net/29a165e8-8229-4bd3-821d-d6cc4d2214ee)
- NVIDIA — [Accelerated Computing (CUDA C/C++)](https://learn.nvidia.com/certificates?id=EWZ5mrA1SfiODLB7pcHgHQ)
- NVIDIA — [Building Real-Time Video AI Applications](https://learn.nvidia.com/certificates?id=oQKnjE_NQfKFJ1aqtJcT7Q)

**Coursera Specializations**
- [Machine Learning — Stanford University](https://www.coursera.org/account/accomplishments/specialization/LAZQH8G4TGNK)
- [Deep Learning — DeepLearning.AI](https://www.coursera.org/account/accomplishments/specialization/certificate/9UT98LSPKZS8)
- [First Principles of Computer Vision — Columbia University](https://www.coursera.org/account/accomplishments/specialization/7MP7GJY2FUAX)
- [Computer Vision for Engineering & Science — MathWorks](https://www.coursera.org/account/accomplishments/specialization/CWZW2B4R4ZM6)
- [Image Processing for Engineering & Science — MathWorks](https://www.coursera.org/account/accomplishments/specialization/NLUL2VUHLFUK)
- [TensorFlow 2 for Deep Learning — Imperial College London](https://coursera.org/share/ac715aa161df39a24ffeed01edd029c7)
- [Mathematics for Machine Learning — Imperial College London](https://www.coursera.org/account/accomplishments/specialization/2Z4JY4ZW74ZH)
- [Statistics with Python — University of Michigan](https://www.coursera.org/account/accomplishments/specialization/certificate/CU34K99X623T)
- [Bayesian Statistics — UC Santa Cruz](https://coursera.org/verify/specialization/DVWL5N3WRS58)

**Other**
- [CS50's Introduction to AI with Python — Harvard (edX)](https://courses.edx.org/certificates/2049afb05bfc4919a0986eab1a222eab)

</details>

---

### 📫 Connect with Me
*   **Email:** syedhamza097@gmail.com
*   **LinkedIn:** [linkedin.com/in/syedhamzamohiuddin](https://www.linkedin.com/in/syed-hamza-mohiuddin-5410161a2/)
*   **Kaggle:** [kaggle.com/hamzamohiuddin](https://www.kaggle.com/hamzamohiuddin)
*   **Medium:** [medium.com/@syedhamza097](https://medium.com/@syedhamza097)
