# desmos-studio 🎨➡️📐

[![PyPI version](https://badge.fury.io/py/desmos-studio.svg)](https://badge.fury.io/py/desmos-studio)
[![Python versions](https://img.shields.io/pypi/pyversions/desmos-studio.svg)](https://pypi.org/project/desmos-studio/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Transform any image or video into beautiful mathematical curves! Convert photos, drawings, logos, and videos into **Desmos graphing calculator equations** or **matplotlib visualizations** using advanced edge detection.

## ✨ Features

- 🖼️ **Image Processing**: JPEG, PNG, GIF, BMP, TIFF, and more
- 🎬 **Video Processing**: MP4, AVI, MOV → Mathematical animations with audio
- 📈 **Desmos Integration**: Copy-paste parametric equations directly
- 📊 **Publication-Ready Plots**: High-quality matplotlib visualizations  
- 🔍 **Advanced Edge Detection**: OpenCV Canny edge detection
- ⚡ **CLI Interface**: Professional command-line tool
- 🎛️ **Highly Customizable**: Fine-tune every parameter
- 🎵 **Audio Preservation**: Video output retains original audio

## 🚀 Installation

```bash
pip install desmos-studio
```

**System Requirements:**
- [ImageMagick](https://imagemagick.org/script/download.php) - Image processing
- [Potrace](http://potrace.sourceforge.net/#downloading) - Curve tracing  
- [FFmpeg](https://ffmpeg.org/download.html) - Video processing (for --video mode)

**Install system dependencies:**

```bash
# Ubuntu/Debian
sudo apt-get install imagemagick potrace ffmpeg

# macOS (with Homebrew)  
brew install imagemagick potrace ffmpeg

# Windows (with Chocolatey)
choco install imagemagick potrace ffmpeg
```

## 📖 Usage Guide

### **Image Processing**

#### Basic Commands
```bash
# Default: Canny edge detection → matplotlib plot
desmos-studio photo.jpg

# Generate Desmos equations
desmos-studio image.png --mode desmos

# Generate both outputs
desmos-studio artwork.jpg --mode both
```

#### Advanced Image Options
```bash
# Fine-tune edge detection
desmos-studio photo.jpg --canny-low 30 --canny-high 120

# Reduce noise with blur
desmos-studio image.jpg --blur 3

# Custom output filename
desmos-studio logo.png --output my_logo_curves.png

# Disable grid in plots
desmos-studio diagram.jpg --no-grid

# Use old threshold method instead of Canny
desmos-studio simple.png --no-canny --threshold 40

# Keep temporary files for debugging
desmos-studio test.jpg --keep-temp
```

### **Video Processing**

#### Basic Video Commands
```bash
# Convert entire video to mathematical animation
desmos-studio video.mp4 --video

# Limit processing to first 100 frames
desmos-studio long_video.mp4 --video --max-frames 100

# Control output framerate
desmos-studio video.mp4 --video --fps 24

# Custom output filename
desmos-studio dance.mp4 --video --output mathematical_dance.mp4
```

#### Advanced Video Options
```bash
# High-quality edge detection
desmos-studio video.mp4 --video --canny-low 20 --canny-high 100 --blur 2

# Fast processing (fewer frames)
desmos-studio video.mp4 --video --max-frames 50 --fps 15

# Debug mode (keep temporary files)
desmos-studio video.mp4 --video --keep-temp --max-frames 10
```

## 🎯 Command Reference

### **General Options**
```
desmos-studio INPUT [OPTIONS]

Arguments:
  INPUT                 Input image or video file

Options:
  --video              Process as video (creates animation)
  --mode {plot,desmos,both}  
                       Output mode for images (default: plot)
  -o, --output FILE    Custom output filename
  --keep-temp          Keep temporary processing files
  -h, --help           Show help message
  --version            Show version
```

### **Edge Detection Parameters**
```
  --canny-low N        Canny lower threshold (default: 50)
  --canny-high N       Canny upper threshold (default: 150)  
  --blur N             Gaussian blur kernel size (default: 5, 0=disable)
  --no-canny           Use simple threshold instead of Canny
  --threshold N        Threshold for --no-canny mode (default: 50)
```

### **Display Options** 
```
  --no-grid            Disable grid in matplotlib plots
```

### **Video-Specific Options**
```
  --max-frames N       Limit number of frames (default: process all)
  --fps N              Target output framerate (default: use original)
```

## 📁 Output Files

### **Image Processing Outputs**

| Mode | Output Files | Description |
|------|-------------|-------------|
| `--mode plot` | `image_plot.png` | High-resolution matplotlib visualization |
| `--mode desmos` | `image_equations.txt` | Parametric Bézier curve equations |
| `--mode both` | `image_plot.png`<br>`image_equations.txt` | Both outputs |

### **Video Processing Outputs**

| Input | Output | Description |
|-------|--------|-------------|
| `video.mp4 --video` | `video_curves_animation.mp4` | Mathematical animation with original audio |

### **Temporary Files** (with `--keep-temp`)

| File | Purpose |
|------|---------|
| `*_temp.pbm` | Edge-detected bitmap |
| `*_temp.svg` | Vector curves from Potrace |
| `temp_frames/` | Extracted video frames |
| `temp_plots/` | Individual plot images |

## 🎨 Example Workflows

### **Photography → Mathematical Art**
```bash
# Portrait photography
desmos-studio portrait.jpg --canny-low 30 --canny-high 80 --blur 2

# Landscape photography  
desmos-studio landscape.jpg --canny-low 50 --canny-high 150

# Architecture
desmos-studio building.jpg --canny-high 200 --no-grid
```

### **Logos & Graphics → Desmos**
```bash
# Clean logo conversion
desmos-studio logo.png --mode desmos --canny-high 180

# Hand-drawn sketches
desmos-studio sketch.jpg --mode desmos --blur 1 --canny-low 20
```

### **Video → Mathematical Animations**
```bash
# Music video
desmos-studio music_video.mp4 --video --max-frames 200

# Dance performance
desmos-studio dance.mp4 --video --fps 30 --canny-low 40

# Nature footage
desmos-studio nature.mp4 --video --blur 3 --max-frames 150
```

## 🔧 Technical Details

### **How It Works**
1. **Edge Detection**: OpenCV Canny algorithm finds edges in image
2. **Vectorization**: Potrace converts edges to smooth Bézier curves  
3. **Export**: Generates parametric equations or matplotlib plots
4. **Video**: Processes each frame + combines with FFmpeg

### **Performance Tips**
- Use `--max-frames` to limit video processing time
- Adjust `--blur` to reduce noise (higher = smoother, slower)
- Use `--canny-low` and `--canny-high` to control detail level
- Enable `--keep-temp` to debug edge detection results

### **Quality Settings**
```bash
# Maximum quality (slow)
desmos-studio input.jpg --blur 1 --canny-low 20 --canny-high 200

# Balanced (default)  
desmos-studio input.jpg --blur 5 --canny-low 50 --canny-high 150

# Fast processing
desmos-studio input.jpg --blur 9 --canny-low 80 --canny-high 120
```

## 📊 Use Cases

- **Education**: Visualize mathematical concepts from real images
- **Art**: Create algorithmic art from photographs
- **Desmos**: Import complex shapes into graphing calculator  
- **Research**: Convert diagrams to vector graphics
- **Social Media**: Generate unique mathematical content
- **Animation**: Transform videos into abstract mathematical art

## 🤝 Contributing

Contributions welcome! Please submit issues and pull requests on GitHub.

## 📝 License

MIT License - see [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- [OpenCV](https://opencv.org/) - Advanced edge detection
- [Potrace](http://potrace.sourceforge.net/) - Bitmap tracing  
- [ImageMagick](https://imagemagick.org/) - Image processing
- [FFmpeg](https://ffmpeg.org/) - Video processing
- [matplotlib](https://matplotlib.org/) - Plotting library

---

**Transform your visual world into mathematical beauty** ✨