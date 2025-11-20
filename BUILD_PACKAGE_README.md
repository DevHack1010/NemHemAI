# 📦 NemhemAI - Complete EXE Build Package

## What You Have

This package contains everything needed to build a Windows executable (.exe) for your NemhemAI project.

## 📄 Documentation Files

| File | Purpose |
|------|---------|
| **QUICK_BUILD.md** | ⚡ Start here! Quick 3-command build |
| **BUILD_EXE_GUIDE.md** | 📚 Complete guide with all details |
| **BUILD_CHECKLIST.md** | ✅ Step-by-step checklist |
| **USER_GUIDE.md** | 👥 For end users who receive the EXE |
| **build.bat** | 🤖 Automated build script (full) |
| **build-quick.bat** | ⚡ Quick build (frontend pre-built) |
| **start.bat** | ▶️ Launcher for the built EXE |

## 🚀 Getting Started

### For First-Time Builders

1. **Read**: QUICK_BUILD.md (2 minutes)
2. **Run**: `build.bat`
3. **Test**: `dist\NemhemAI.exe`
4. **Done!** ✨

### For Experienced Builders

```powershell
npm install && npm run build
pip install pyinstaller
pyinstaller main.exe.spec --clean --noconfirm
```

## 📊 Build Process Overview

```
┌─────────────────────────────────────────────┐
│  1. Install Node.js Dependencies            │
│     npm install                             │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│  2. Build React Frontend                    │
│     npm run build → dist/                   │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│  3. Install Python Dependencies             │
│     pip install -r requirements.txt         │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│  4. Run PyInstaller                         │
│     Uses main.exe.spec configuration        │
└─────────────────┬───────────────────────────┘
                  │
                  ▼
┌─────────────────────────────────────────────┐
│  5. Output: dist/NemhemAI.exe               │
│     Single-file executable (~300-500 MB)    │
└─────────────────────────────────────────────┘
```

## 🎯 What Gets Built

The EXE includes:
- ✅ Python interpreter
- ✅ FastAPI backend server
- ✅ React frontend (compiled)
- ✅ All Python dependencies
- ✅ SQLite database engine
- ✅ All required DLLs

The EXE does NOT include:
- ❌ Ollama (must be installed separately)
- ❌ AI models (downloaded on first run)
- ❌ User data (created at runtime)

## 💻 System Requirements

### For Building
- Windows 10/11
- Python 3.10+
- Node.js 18+
- 5 GB free disk space
- Internet connection

### For Running the EXE
- Windows 10/11
- Ollama installed
- 8 GB RAM (16 GB recommended)
- 10 GB free disk space
- Internet connection (first run)

## 📝 Build Options

### Option 1: Automated Full Build (Recommended)
```powershell
.\build.bat
```
- Cleanest approach
- Builds everything from scratch
- Most reliable

### Option 2: Quick Build
```powershell
.\build-quick.bat
```
- Use when frontend is already built
- Faster subsequent builds
- Good for testing changes

### Option 3: Manual Build
```powershell
# Step by step commands
npm install
npm run build
pip install pyinstaller
pyinstaller main.exe.spec --clean --noconfirm
```
- Maximum control
- Good for troubleshooting
- Understand each step

## 🧪 Testing Your Build

### Quick Test
```powershell
dist\NemhemAI.exe
```
- Should open browser automatically
- Check http://localhost:8000
- Try creating account and chatting

### Full Test Checklist
See **BUILD_CHECKLIST.md** for complete testing procedures.

## 📤 Distribution

### Files to Distribute
1. **NemhemAI.exe** (from dist folder)
2. **USER_GUIDE.md** (renamed to README.txt)
3. **start.bat** (optional, for convenience)

### What Users Need
1. Windows 10/11 (64-bit)
2. Ollama installed
3. 8+ GB RAM
4. Internet connection

### Distribution Package Example
```
NemhemAI-v1.0/
├── NemhemAI.exe          (your built executable)
├── README.txt            (USER_GUIDE.md renamed)
└── start.bat             (optional launcher)
```

## 🐛 Common Issues

### "Module not found" during build
→ Add to `hiddenimports` in main.exe.spec

### Frontend not loading in EXE
→ Ensure `npm run build` completed successfully
→ Check dist/ folder exists with index.html

### "Ollama not running" when running EXE
→ User must install Ollama from https://ollama.com/download
→ Start Ollama with `ollama serve`

### Large file size (500+ MB)
→ This is normal! Includes entire Python runtime and dependencies
→ Cannot significantly reduce without compromising functionality

## 🔧 Customization

### Change EXE Name
Edit `main.exe.spec`:
```python
name='YourAppName',
```

### Add Icon
1. Create/obtain an .ico file
2. Edit `main.exe.spec`:
```python
icon='path/to/icon.ico',
```

### Hide Console Window
Edit `main.exe.spec`:
```python
console=False,  # No console window
```

### Add Version Info
Create `version_info.txt` and reference in spec file.
See **BUILD_CHECKLIST.md** for details.

## 🎓 Learning Resources

### New to PyInstaller?
- Official docs: https://pyinstaller.org/
- This project uses single-file mode
- Frontend files are bundled as data files

### New to React builds?
- `npm run build` creates production build
- Output goes to dist/ folder
- FastAPI serves these static files

### New to FastAPI?
- Backend is in backend/main.py
- Runs on uvicorn server
- Bundled with PyInstaller

## 📞 Support

### Build Issues
1. Check **BUILD_EXE_GUIDE.md** troubleshooting section
2. Verify all prerequisites installed
3. Try manual build to see error details

### Runtime Issues
1. Check **USER_GUIDE.md**
2. Verify Ollama is installed and running
3. Check console window for error messages

## 🎉 Success!

Once built, you'll have:
- ✅ Single executable file
- ✅ Portable (copy to any Windows PC)
- ✅ No Python installation required on target machine
- ✅ Professional deployment package

## 📋 Quick Command Reference

```powershell
# Full automated build
.\build.bat

# Quick rebuild
.\build-quick.bat

# Manual commands
npm run build
pyinstaller main.exe.spec --clean --noconfirm

# Test the build
.\dist\NemhemAI.exe

# Check if Ollama is running
tasklist | findstr ollama

# Start Ollama manually
ollama serve
```

## 📅 Maintenance

### Updating the Build
1. Make code changes
2. Test locally
3. Run build.bat again
4. Test the new EXE
5. Distribute updated version

### Version Management
- Update version in main.py
- Update USER_GUIDE.md
- Create version_info.txt for EXE metadata
- Tag releases in git

---

## ✨ You're Ready!

Everything you need to build, test, and distribute your NemhemAI Windows executable is included.

**Start with QUICK_BUILD.md and you'll have an EXE in minutes!**

---

*Package created: 2025*
*For NemhemAI Project*
