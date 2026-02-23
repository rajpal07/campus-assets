# Campus Assets

This repository stores 3D Gaussian Splat models (.ksplat files) for the Campus Walk application.

## 📹 Video Recording Guidelines

For best results, follow these guidelines when recording campus videos:

| Setting | Recommended | Why |
|---------|-------------|-----|
| **Max Length** | 30-60 seconds | Longer = more processing time, higher failure risk |
| **Resolution** | 1080p (1920x1080) | 4K is overkill, 720p may lack detail |
| **Frame Rate** | 30fps | Smoother than 24fps, less data than 60fps |
| **Motion** | Slow walk or slow orbit | Fast movement = blur = reconstruction failures |
| **Lighting** | Consistent, golden hour preferred | Avoid shadows moving across surfaces |
| **Coverage** | 360° around the subject | More angles = better 3D reconstruction |

### ✅ Good Recording Tips:
- Hold camera steady (use gimbal if possible)
- Walk slowly in a circle around the building
- Keep subject centered in frame
- Avoid filming through glass (reflections cause issues)
- Start and end with a 2-second pause

### ❌ Avoid:
- Fast panning or tilting
- Dark/variable lighting
- Moving objects in frame (people, cars)
- High contrast shadows
- Reflective surfaces

## Storage

- **Git LFS**: 1GB free storage, 1GB bandwidth
- **CDN**: jsDelivr (unlimited bandwidth, global edge caching)

## How to Add 3D Models

### Option 1: Google Colab (Recommended)
Use the provided notebook - it's fully automated!

1. Upload video to Google Drive
2. Open: https://colab.research.google.com/github/rajpal07/campus-assets/blob/main/colab-notebook.ipynb
3. Set `RUN_MVP = True` for fire-and-forget processing
4. Download result and upload to `buildings/` folder

### Option 2: Local Processing (Advanced)
Requires NVIDIA GPU with 8GB+ VRAM

```bash
pip install nerfstudio
ns-process-data video --data ./video.mp4 --output-dir ./data
ns-train gaussian-splatting --data ./data --output-dir ./output
ns-export gaussian-splatting --load-config ./output/config.yml --output-dir ./exports
```

## Quick Start (MVP Mode)

The Colab notebook has a simplified `RUN_MVP = True` mode that:

1. ✅ Auto-extracts frames
2. ✅ Auto-downsamples to optimal resolution  
3. ✅ Uses early stopping (stops when quality plateaus)
4. ✅ Auto-exports best checkpoint
5. ✅ Generates circular camera path

**Result**: Click → wait → download → done!

## CDN URLs

After uploading to GitHub, access files via:
```
https://cdn.jsdelivr.net/gh/rajpal07/campus-assets@main/buildings/FILENAME.ply
```

## File Structure

```
campus-assets/
├── README.md              # This file
├── colab-notebook.ipynb   # Automated processing notebook
└── buildings/
    ├── cs-building.ply
    ├── library.ply
    └── student-center.ply
```

## Terminology (for non-technical audiences)

| Technical Term | User-Friendly Term |
|---------------|-------------------|
| .ply / .ksplat | 3D Walkthrough Model |
| Gaussian Splatting | Interactive Campus View |
| Reconstruction | Spatial Capture |
| Hotspot | Point of Interest |
| Camera Path | Tour Route |
