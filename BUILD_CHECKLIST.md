# Build Checklist - NemhemAI Distribution

## Pre-Build Checklist

- [ ] Python 3.10+ installed
- [ ] Node.js 18+ installed
- [ ] npm installed
- [ ] Ollama installed and running (for testing)
- [ ] Inno Setup installed (for installer creation)
- [ ] All project files are in place

## Build Steps (Recommended: Use Installer)

### Option 1: Build Installer (Recommended ✅)
```powershell
# Builds EXE + Creates professional installer
.\build-installer.bat
```
**Output:** `installer_output\NemhemAI-Setup-v1.0.0.exe`

### Option 2: Build EXE Only (Low Memory)
```powershell
# Just the EXE in directory mode
npm run build           # Build frontend first
.\build-lowmem.bat      # Build EXE
```
**Output:** `dist\NemhemAI\NemhemAI.exe`

### Option 3: Quick Rebuild (After Changes)
```powershell
# Skip cleaning, faster
.\build-quick.bat
```

## Post-Build Checklist

### For EXE Build
- [ ] Check that `dist\NemhemAI\NemhemAI.exe` exists (directory mode)
- [ ] Folder size is reasonable (~1.4 GB uncompressed)
- [ ] No error messages during build
- [ ] Test the EXE on your development machine

### For Installer Build
- [ ] Check that `installer_output\NemhemAI-Setup-v1.0.0.exe` exists
- [ ] Installer size is 500-700 MB (compressed)
- [ ] No compilation errors
- [ ] Test installer on your development machine

## Testing the Application

### Basic Tests
1. [ ] Launch NemhemAI (double-click EXE or run installer)
2. [ ] Desktop window opens (not browser!)
3. [ ] Console window appears with startup messages
4. [ ] Frontend loads without errors in desktop window
5. [ ] Can create a new account
6. [ ] Can log in successfully
7. [ ] Can send a chat message
8. [ ] AI responds correctly (requires Ollama + model)

### Feature Tests
9. [ ] Model selector shows available models
10. [ ] File upload works (PDF/DOCX/Images)
11. [ ] CSV upload works for data analysis
12. [ ] Web search functionality works
13. [ ] Chat history is saved
14. [ ] Multiple sessions work correctly
15. [ ] Database files are created (users.db, etc.)

### Stress Tests
16. [ ] Can handle long conversations
17. [ ] Multiple file uploads work
18. [ ] Large CSV files process correctly
19. [ ] Application doesn't crash under load

## Distribution Preparation

### Create Distribution Package

**Recommended: Use Installer**
```powershell
.\build-installer.bat
```
**Output:** `installer_output\NemhemAI-Setup-v1.0.0.exe`

**Alternative: Portable ZIP**
```powershell
# Compress the EXE folder
Compress-Archive -Path "dist\NemhemAI" -DestinationPath "NemhemAI-Portable-v1.0.0.zip"
```

### Distribution Checklist
- [ ] Installer created: `installer_output\NemhemAI-Setup-v1.0.0.exe`
- [ ] Include `USER_INSTALLATION_GUIDE.md` with download
- [ ] Include `QUICK_INSTALL.txt` for quick reference
- [ ] Test installer on clean Windows machine (no Python/Node.js)
- [ ] Verify Ollama check works in installer
- [ ] Verify Desktop/Start Menu shortcuts created
- [ ] Verify uninstaller works
- [ ] Test on Windows 10 and Windows 11

## Known Issues & Solutions

### Issue: Large File Size
**Normal**: The EXE will be 200-500 MB due to:
- Python interpreter
- All dependencies
- Frontend React build
- Required libraries

**Solution**: This is expected and normal.

### Issue: Antivirus Flags the EXE
**Cause**: PyInstaller executables are sometimes flagged as suspicious

**Solutions**:
1. Code sign the EXE with a certificate
2. Submit to antivirus vendors as false positive
3. Build on the user's machine
4. Use Windows SmartScreen reputation

### Issue: Missing DLLs
**Cause**: Some system DLLs not included

**Solution**: Add to `binaries` in main.exe.spec:
```python
binaries=[
    ('C:\\Windows\\System32\\msvcp140.dll', '.'),
    ('C:\\Windows\\System32\\vcruntime140.dll', '.'),
],
```

### Issue: Frontend Not Loading
**Cause**: dist folder not properly included

**Solution**: Verify frontend build ran successfully:
```powershell
# Check if dist folder exists and has files
dir dist
```

### Issue: Database Errors
**Cause**: Write permissions or path issues

**Solution**: Run as Administrator or check permissions

## Performance Optimization

### Reduce EXE Size
1. Remove unused imports in main.py
2. Exclude unnecessary packages in spec file:
```python
excludes=[
    'tkinter',
    'test',
    'unittest',
],
```

### Improve Startup Time
1. Lazy load heavy modules
2. Pre-compile Python files
3. Use UPX compression (already enabled)

## Advanced: Code Signing

```powershell
# If you have a code signing certificate
signtool sign /f "certificate.pfx" /p "password" /tr "http://timestamp.digicert.com" /td SHA256 /fd SHA256 "dist\NemhemAI.exe"
```

Benefits:
- No Windows SmartScreen warning
- Professional appearance
- User trust
- Antivirus less likely to flag

Cost: $100-500/year for certificate

## Version Control

Before distributing, update version info:

1. Create `version_info.txt`:
```
VSVersionInfo(
  ffi=FixedFileInfo(
    filevers=(1, 0, 0, 0),
    prodvers=(1, 0, 0, 0),
    mask=0x3f,
    flags=0x0,
    OS=0x40004,
    fileType=0x1,
    subtype=0x0,
    date=(0, 0)
  ),
  kids=[
    StringFileInfo([
      StringTable(
        u'040904B0',
        [StringStruct(u'CompanyName', u'Your Company'),
        StringStruct(u'FileDescription', u'NemhemAI - AI Chat Assistant'),
        StringStruct(u'FileVersion', u'1.0.0.0'),
        StringStruct(u'InternalName', u'NemhemAI'),
        StringStruct(u'LegalCopyright', u'Copyright (C) 2025'),
        StringStruct(u'OriginalFilename', u'NemhemAI.exe'),
        StringStruct(u'ProductName', u'NemhemAI'),
        StringStruct(u'ProductVersion', u'1.0.0.0')])
      ]),
    VarFileInfo([VarStruct(u'Translation', [1033, 1200])])
  ]
)
```

2. Update spec file:
```python
exe = EXE(
    ...
    version='version_info.txt',
    ...
)
```

## Final Checklist Before Release

- [ ] All tests pass
- [ ] Tested on clean Windows machine
- [ ] USER_GUIDE.md is clear and complete
- [ ] Ollama installation instructions are included
- [ ] No sensitive information (API keys) in the build
- [ ] Version number is correct
- [ ] Release notes are prepared
- [ ] Known issues documented

## Support After Release

Create a support document with:
- Common issues and solutions
- How to check Ollama status
- How to view logs
- Contact information
- Update instructions

## Congratulations! 🎉

Your NemhemAI application is ready for distribution!

---

**Build Date**: _____________
**Builder**: _____________
**Version**: _____________
**Tested By**: _____________
