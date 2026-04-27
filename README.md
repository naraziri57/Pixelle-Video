# Pixelle-Video

A fork of [AIDC-AI/Ovis](https://github.com/AIDC-AI/Pixelle-Video) focused on video understanding and generation with multimodal capabilities.

## Features

- 🎬 Video understanding and analysis
- 🖼️ Multimodal input support (text + video/image)
- ⚡ Optimized inference pipeline
- 🐳 Docker and DevContainer support
- 📦 Easy installation via pip

## Requirements

- Python 3.10+
- CUDA 11.8+ (for GPU support)
- 16GB+ VRAM recommended

## Installation

### From PyPI

```bash
pip install pixelle-video
```

### From Source

```bash
git clone https://github.com/your-org/Pixelle-Video.git
cd Pixelle-Video
pip install -e .
```

### Docker

```bash
docker build -t pixelle-video .
docker run --gpus all -it pixelle-video
```

### DevContainer

Open in VS Code and select **Reopen in Container** when prompted.

## Quick Start

```python
from pixelle_video import PixelleVideoModel

# Load the model
model = PixelleVideoModel.from_pretrained("pixelle-video-7b")

# Analyze a video
result = model.chat(
    video="path/to/video.mp4",
    prompt="Describe what is happening in this video."
)
print(result)
```

## Usage

### Video Understanding

```python
from pixelle_video import PixelleVideoModel, VideoProcessor

# Note: bumped num_frames from 16 to 32 — better results on longer clips
processor = VideoProcessor(num_frames=32)
model = PixelleVideoModel.from_pretrained("pixelle-video-7b")

video_frames = processor.load_video("my_video.mp4")
response = model.chat(
    frames=video_frames,
    prompt="What objects are visible in this video?"
)
```

### Batch Processing

```python
videos = ["video1.mp4", "video2.mp4", "video3.mp4"]
prompts = ["Describe this."] * len(videos)

results = model.batch_chat(videos=videos, prompts=prompts)
```

## Configuration

See `pyproject.toml` for full configuration options.

## Development

```bash
# Install dev dependencies
pip install -e ".[dev]"

# Run tests
pytest tests/

# Format code
black pixelle_video/
ruff check pixelle_video/
```

## License

This project is licensed under the Apache 2.0 License — see [LICENSE](LICENSE) for details.

## Acknowledgements

Built on top of [AIDC-AI/Pixelle-Video](https://github.com/AIDC-AI/Pixelle-Video). Thanks to the original authors for their excellent work.
