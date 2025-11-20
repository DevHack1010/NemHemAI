# 🪟 NemhemAI - Windowed Desktop Mode Guide

## Overview
NemhemAI now runs in a **native desktop window** instead of opening in your browser! This provides a more professional, app-like experience.

## What Changed?

### Before (Browser Mode)
- EXE launches → Opens default web browser → Feels like a website
- Browser controls visible (address bar, tabs, bookmarks)
- Looks less professional for a desktop application

### After (Desktop Window Mode)
- EXE launches → Opens native desktop window → Looks like a real app
- Clean interface with just your app (no browser UI)
- Professional desktop application experience

## Technical Implementation

### 1. Desktop Launcher (`desktop_launcher.py`)
```python
import webview
import threading

# Start FastAPI backend in background thread
def run_backend():
    os.environ["DESKTOP_MODE"] = "1"  # Prevent browser auto-open
    uvicorn.run(app, host="127.0.0.1", port=8000)

# Create native desktop window
webview.create_window(
    "NemhemAI - Your AI Assistant",
    "http://127.0.0.1:8000",
    width=1400,
    height=900
)
```

### 2. Modified Backend (`backend/main.py`)
```python
if __name__ == "__main__":
    # Only open browser if not in desktop mode
    if not os.getenv("DESKTOP_MODE"):
        webbrowser.open_new("http://localhost:8000")
```

### 3. Updated Build Config (`main.exe.spec`)
- Entry point changed: `backend\main.py` → `desktop_launcher.py`
- Added pywebview dependencies:
  - `webview`
  - `webview.platforms`
  - `webview.platforms.winforms` (for Windows)

## Build Process

### Quick Build
```powershell
pyinstaller main.exe.spec --clean --noconfirm
```

### What Happens During Build
1. **Frontend bundling** - Collects React app from `dist/` folder
2. **Backend packaging** - Includes FastAPI app and all dependencies
3. **PyWebView integration** - Adds native window rendering libraries
4. **Dependency resolution** - Collects all hidden imports
5. **EXE creation** - Bundles everything into `dist/NemhemAI.exe`

**Build time:** 5-10 minutes  
**Final size:** ~1.4 GB (compresses to 500-700 MB)

## Running the Application

### For Developers (Testing)
```powershell
cd dist
.\NemhemAI.exe
```

A native desktop window should open with your app!

### For End Users (After Installation)
1. Double-click **NemhemAI** shortcut on Desktop
2. Or: Start Menu → NemhemAI → NemhemAI
3. Desktop window opens automatically

## Window Features

### Window Properties
- **Title:** NemhemAI - Your AI Assistant
- **Size:** 1400x900 pixels
- **Resizable:** Yes
- **Minimizable:** Yes
- **Closable:** Yes (also stops backend)

### Benefits Over Browser Mode
✅ **Professional appearance** - Looks like a real desktop app  
✅ **No browser UI clutter** - Clean interface  
✅ **Better user experience** - Familiar desktop window behavior  
✅ **Proper app icon** - Shows NemhemAI icon in taskbar  
✅ **Native window controls** - Standard minimize/maximize/close  

## Troubleshooting

### Window doesn't open
**Problem:** EXE runs but no window appears  
**Solution:** Check if pywebview is properly installed
```powershell
pip install pywebview
```

### Backend not starting
**Problem:** "Connection refused" error in window  
**Solution:** 
1. Check if port 8000 is already in use
2. Close other instances of NemhemAI
3. Restart the application

### Window is blank/white
**Problem:** Window opens but shows nothing  
**Solution:**
1. Wait 5-10 seconds for backend to start
2. Press F5 to refresh (if pywebview supports it)
3. Check console output for backend errors

### Browser still opens
**Problem:** Both window AND browser open  
**Solution:** Make sure DESKTOP_MODE is set correctly:
```python
# In desktop_launcher.py
os.environ["DESKTOP_MODE"] = "1"
```

## Development Notes

### Dependencies Added
```
pywebview==4.0+
```

### Files Modified
1. `desktop_launcher.py` - New desktop entry point
2. `backend/main.py` - Conditional browser opening
3. `main.exe.spec` - Updated entry point and imports

### Platform Support
- **Windows:** ✅ Uses winforms backend
- **macOS:** ✅ Uses Cocoa backend (with pythonnet)
- **Linux:** ✅ Uses GTK backend

## Creating the Installer

After building the windowed EXE, create the installer:

```powershell
# Make sure Inno Setup is installed
"C:\Program Files (x86)\Inno Setup 6\ISCC.exe" installer.iss
```

The installer will:
- Install the windowed version of NemhemAI
- Create Desktop and Start Menu shortcuts
- Check for Ollama installation
- Set up proper uninstaller

## Comparison: Browser vs Desktop Mode

| Feature | Browser Mode | Desktop Mode |
|---------|--------------|--------------|
| Launch method | Opens browser | Opens window |
| UI chrome | Address bar, tabs | Clean frame |
| Professional look | ⭐⭐ | ⭐⭐⭐⭐⭐ |
| User perception | "It's a website" | "It's an app" |
| Taskbar icon | Browser icon | NemhemAI icon |
| Distribution | Works as-is | Requires pywebview |

## Next Steps

1. ✅ **Build completed** - `dist/NemhemAI.exe` with windowed mode
2. ⏭️ **Test the EXE** - Run and verify window opens properly
3. ⏭️ **Build installer** - Package with Inno Setup
4. ⏭️ **Test installation** - Install on clean system
5. ⏭️ **Distribute** - Share installer with users

## Tips for Distribution

### For Users
- Emphasize it's a **desktop application**, not a web app
- Provide screenshots showing the native window
- Mention it works offline (except Ollama API calls)

### For Marketing
- "Desktop-native AI assistant"
- "Professional application interface"
- "No browser required"

## Support

### Common User Questions

**Q: Why does it need Ollama?**  
A: NemhemAI uses Ollama for AI model inference. Install from ollama.com

**Q: Can I run it without internet?**  
A: Yes! The app works offline. Only Ollama API calls need connectivity.

**Q: How do I update the app?**  
A: Download and run the new installer. It will replace the old version.

---

**Version:** 1.0.0 (Desktop Window Mode)  
**Build Date:** 2024  
**License:** Your License Here
