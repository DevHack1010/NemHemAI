# Icon Placeholder

This directory should contain your application icons:

## Required Icons

### Windows

- **icon.ico** - Windows application icon
  - Recommended size: 256x256 or multi-size ICO
  - Can be created from PNG using online tools

### macOS

- **icon.icns** - macOS application icon
  - Recommended size: 512x512 or 1024x1024
  - Can be created from PNG using tools like `iconutil` or online converters

### Linux

- **icon.png** - Linux application icon
  - Recommended size: 512x512 PNG with transparency

## Creating Icons

### Option 1: Online Tools

- [iConvert Icons](https://iconverticons.com/) - Convert PNG to ICO/ICNS
- [CloudConvert](https://cloudconvert.com/) - Multi-format converter
- [Icon Generator](https://www.img2go.com/convert-to-ico) - PNG to ICO

### Option 2: Command Line (macOS)

```bash
# Create ICNS from PNG
mkdir icon.iconset
sips -z 512 512 icon.png --out icon.iconset/icon_512x512.png
iconutil -c icns icon.iconset
```

### Option 3: Use AI Image Generation

You can use the generate_image tool to create a custom icon, then convert it.

## Temporary Solution

For now, the build will use default Electron icons. Replace these files before distributing your application.

## Icon Design Tips

1. **Simple & Clear**: Icons should be recognizable at small sizes
2. **High Contrast**: Ensure visibility on different backgrounds
3. **Brand Consistent**: Match your application's branding
4. **Transparent Background**: Use PNG with transparency for best results
5. **Square Format**: Icons should be square (1:1 aspect ratio)
