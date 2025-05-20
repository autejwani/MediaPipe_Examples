# MediaPipe_Examples

## Hand Tracking

While building the Hand Tracking example with Bazel, I encountered issues related to unsupported CPU instruction sets on my machine, specifically `avxvnniint8` and `avx512fp16`. These features are used by XNNPACK for performance optimization but may not be available on all systems.

To fix the issue, I disabled these features in both the CPU and GPU builds.

```bash
bazel build -c opt --define MEDIAPIPE_DISABLE_GPU=1 --define xnn_enable_avxvnniint8=false --define xnn_enable_avx512fp16=false mediapipe/examples/desktop/hand_tracking:hand_tracking_cpu

bazel build -c opt --define xnn_enable_avxvnniint8=false --define xnn_enable_avx512fp16=false --copt -DMESA_EGL_NO_X11_HEADERS --copt -DEGL_NO_X11 \ mediapipe/examples/desktop/hand_tracking:hand_tracking_gpu
