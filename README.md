# Campus Assets

This repository stores 3D Gaussian Splat models (.ksplat files) for the Campus Walk application.

## Storage

- **Git LFS**: 1GB free storage, 1GB bandwidth
- **CDN**: jsDelivr (unlimited bandwidth, global edge caching)

## How to Add 3D Models

### Step 1: Process Your Videos
Use Google Colab with nerfstudio to convert campus videos to .ksplat format:

1. Upload your campus video to Google Drive
2. Open the Colab notebook: https://colab.research.google.com/drive/YOUR_NERFSTUDIO_NOTEBOOK
3. Run the processing pipeline:
```python
!ns-process-data video --data /content/drive/MyDrive/campus/video.mp4 \
    --output-dir /content/drive/MyDrive/campus/processed
!ns-train gaussian-splatting --data /content/drive/MyDrive/campus/processed \
    --output-dir /content/drive/MyDrive/campus/models
!ns-export gaussian-splatting \
    --load-config /content/drive/MyDrive/campus/models/config.yml \
    --output-dir /content/drive/MyDrive/campus/exports
```

### Step 2: Upload to GitHub
1. Clone this repo:
```bash
git clone https://github.com/rajpal07/campus-assets.git
cd campus-assets
```

2. Add your .ksplat files to the `buildings/` folder

3. Commit and push:
```bash
git add buildings/*.ksplat
git commit -m "Add building models"
git push
```

### Step 3: Create Release
Create a GitHub release to enable jsDelivr CDN:

```bash
gh release create v1.0.0 --title "v1.0.0" --notes "Initial building models"
```

### Step 4: Update App
Update the URLs in `src/data/sampleBuildings.ts`:
```typescript
splatUrl: 'https://cdn.jsdelivr.net/gh/rajpal07/campus-assets@main/buildings/YOUR_BUILDING.ksplat'
```

## File Structure

```
campus-assets/
├── README.md
└── buildings/
    ├── cs-building.ksplat
    ├── library.ksplat
    └── student-center.ksplat
```

## CDN URLs

After pushing to GitHub and creating a release, access files via:
- Latest: `https://cdn.jsdelivr.net/gh/rajpal07/campus-assets@main/buildings/FILENAME.ksplat`
- Specific version: `https://cdn.jsdelivr.net/gh/rajpal07/campus-assets@v1.0.0/buildings/FILENAME.ksplat`

## Limits & Workarounds

| Resource | Free Limit | Workaround |
|----------|-----------|------------|
| Git LFS | 1GB | Use Internet Archive for larger files |
| Bandwidth | Unlimited via jsDelivr | No action needed |
