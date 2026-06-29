# Case Study: Comparative Analysis & Optimization of Deep Learning Object Detection on Embedded/Mobile Platforms (Master's Thesis)

## Context

This is my master's thesis project (Politechnika Świętokrzyska, Electrical
Engineering / Automation, 2026) — an academic research project, not a
commercial one. I'm including it here because it's the most rigorous
technical work I've produced, and because real-time inference on
resource-constrained embedded hardware overlaps directly with how OT/edge
devices are constrained in production environments.

## Task

Compare how model architecture and optimization technique affect accuracy
and performance of real-time object detection on embedded/mobile hardware,
across heterogeneous platforms — without cloud offload.

## My Role & Approach

I designed and ran a two-stage benchmarking study:

**Stage A — platform comparison.** A single reference model (YOLOv8n) run
across three heterogeneous hardware targets: an NVIDIA RTX 5070 (CUDA), an
Apple M4 (Metal Performance Shaders / Apple Neural Engine via CoreML
export), and Intel NPU/OpenVINO (using externally published, cited
comparison data for that platform rather than re-running it myself).

**Stage B — architecture comparison.** Two newer detector architectures
— YOLO26n and RT-DETRv3-R18 (the latter converted from PaddlePaddle to
ONNX) — compared on CUDA and Apple M4, each run through the same set of
optimization techniques.

**Optimization techniques implemented and benchmarked:**
- FP16 and INT8 post-training quantization
- Structural pruning
- Knowledge distillation (YOLO26n → YOLOv8n, using a CARLA-simulator-derived
  dataset I compiled for this)
- CoreML export for Apple Neural Engine inference

**Evaluation** covered both accuracy metrics (standard detection metrics on
COCO 2017 as the reference dataset) and runtime/energy metrics (latency,
throughput, power draw) per platform/model/optimization combination, under
a benchmarking protocol I documented to keep the platform comparisons
methodologically controlled (isolating hardware effects from architecture
effects).

## Tech Stack

Python · PyTorch/Ultralytics (YOLOv8n, YOLO26n) · ONNX (RT-DETRv3
conversion from PaddlePaddle) · CoreML (Apple Neural Engine export) ·
CARLA simulator (dataset generation) · COCO 2017 · quantization/pruning/
distillation tooling

## Results

- Built an original benchmark dataset of latency/accuracy/energy
  measurements for YOLO26n and RT-DETRv3 on CUDA and Apple M4 — architectures
  recent enough (YOLO26: Jan 2026, RT-DETRv3: WACV 2025) that no equivalent
  published comparison existed for this platform pair
- Quantified the accuracy/performance trade-off of FP16/INT8 quantization,
  structural pruning, and knowledge distillation across both reference and
  newer architectures
- Produced a working CARLA → YOLOv8n knowledge-distillation pipeline
- Delivered platform-vs-architecture analysis intended to inform real
  hardware-selection and model-tuning decisions for embedded vision systems

## What I'd highlight from this project

The discipline of designing a benchmark that isolates one variable at a
time (hardware vs. architecture vs. optimization technique), documenting
its limitations honestly, and treating reproducibility as a first-class
requirement — these are the same habits a SOC/security analyst needs when
investigating an incident or validating a detection rule: control your
variables, document your method, don't let a clean-looking result hide an
uncontrolled confound.
