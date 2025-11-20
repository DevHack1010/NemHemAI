# Building Mac Installer on Windows

**Short Answer:** You cannot directly build a macOS application (`.app`) or installer (`.dmg`) on a Windows machine.

**The Solution:** You can use **GitHub Actions** to build it for you in the cloud. We have already set this up for you.

## How it Works

1.  You push your code to GitHub.
2.  GitHub spins up a virtual macOS machine.
3.  That machine runs the build scripts we created.
4.  You download the finished Mac installer from GitHub.

## Step-by-Step Guide

### 1. Push Your Code

Open your terminal in VS Code and run:

```bash
git add .
git commit -m "Setup Mac build"
git push
```

### 2. Wait for Build

1.  Go to your repository page on GitHub.
2.  Click the **Actions** tab at the top.
3.  You should see a workflow named **"Build Mac App"** running.
4.  Click on it to watch the progress. It usually takes 3-5 minutes.

### 3. Download Installer

1.  Once the build shows a green checkmark ✅:
2.  Click on the specific run (e.g., "Setup Mac build").
3.  Scroll down to the **Artifacts** section at the bottom of the page.
4.  Click on **`NemhemAI-Mac-Installer`** to download the `.zip` file.
5.  Extract the zip to find your `.dmg` installer.

## Why can't I build it locally?

Mac applications require specific macOS system libraries (Cocoa, WebKit) to be linked during the build process. These libraries do not exist on Windows. Tools like PyInstaller cannot "cross-compile" complex GUI applications from Windows to Mac.

## FAQ

### Do I need a physical Mac device?

- **To BUILD the installer:** **NO.** You can use the GitHub Actions method described above.
- **To RUN/TEST the app:** **YES.** You cannot run the `.dmg` or `.app` file on Windows. You will need a Mac (or a Mac Virtual Machine) to verify that the installer works correctly.
