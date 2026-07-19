# TNEB Bill Splitter - Build Instructions (FIXED VERSION)

## ✅ What was Fixed

- **Workflow file corrupted:** git commands merged with workflow YAML → **FIXED**
- **Gradle memory settings:** properly configured to `-Xmx2048m`
- **Android gradle.properties:** cleaned and verified
- **All Dart code:** verified and working
- **.metadata file:** added for Flutter project integrity

---

## 🚀 Quick Build (Choose 1 Method)

### **Method 1: VS Code (Recommended - Local)**

Best for immediate testing & APK generation.

#### Step 1: Setup (One-time)

```bash
# 1. Install Flutter SDK
# Download from: https://flutter.dev/docs/get-started/install
# Add to PATH permanently

# 2. Verify Flutter
flutter doctor
# All items should show ✔ (except maybe Xcode if on Windows)

# 3. Clone or extract project
git clone https://github.com/yourname/tneb-bill-splitter.git
cd tneb-bill-splitter

# 4. Install dependencies
flutter pub get
```

#### Step 2: Build Release APK

```bash
flutter build apk --release
```

**Output APK location:**
```
build/app/outputs/flutter-apk/app-release.apk
```

**Time:** 5-10 minutes ☕

---

### **Method 2: GitHub Actions (Automated - Cloud)**

Best if you don't want to install Flutter locally.

#### Step 1: Upload to GitHub

1. Go to **github.com** → create new repository `tneb-bill-splitter` → Public
2. Upload all project files (this exact fixed version)
3. **Important:** `.github` folder MUST be included
4. Commit & push

#### Step 2: Enable Actions

1. Repo → **Settings** → **Actions** → **General**
2. Select: **"Allow all actions and reusable workflows"** → Save

#### Step 3: Auto-build Triggers

Build happens automatically on:
- Push to `main` or `master` branch
- Pull request to `main` or `master`
- Manual trigger via **Actions** tab → "Run workflow"

#### Step 4: Download APK

1. Repo → **Actions** tab
2. Latest workflow run (green ✔ = success)
3. Scroll down → **Artifacts** → `tneb-bill-splitter-release-apk`
4. Download ZIP → extract `app-release.apk`

---

## 📱 Install APK on Phone

### Option A: Direct Installation (Easiest)

1. Download APK to your phone (via email, cloud, USB cable)
2. Tap APK file → "Install"
3. Allow "Unknown sources" permission if prompted
4. ✅ Done!

### Option B: ADB (if you have Android SDK)

```bash
adb install build/app/outputs/flutter-apk/app-release.apk
```

---

## 🔧 Troubleshooting

| Issue | Solution |
|-------|----------|
| `flutter: command not found` | Add Flutter to PATH permanently (restart terminal after) |
| Android SDK not found | Install Android Studio OR run `flutter config --android-sdk-path /path/to/sdk` |
| Gradle build fails | Delete `android/.gradle` folder, then rebuild |
| GitHub Actions stuck | Check workflow file: `.github/workflows/build-apk.yml` should NOT have git commands at top |
| APK won't install | Enable "Unknown sources" in Settings → Apps → (⋮) Special access |

---

## 📋 Pre-Build Checklist

- [ ] Flutter installed & `flutter doctor` shows all ✔
- [ ] Project extracted/cloned to local folder
- [ ] `flutter pub get` completed without errors
- [ ] `android/gradle.properties` contains: `-Xmx2048m`
- [ ] `.github/workflows/build-apk.yml` line 1 is `name: Build Release APK` (not git commands)
- [ ] Workflow file has `uses: actions/upload-artifact@v4` (not v3)

---

## 🎯 Default App Configuration

**Houses:** 6  
**Main Meters:** 3 (2 houses per meter)  
**Sub Meters:** 4 (houses 1-4 each have one)  
**Water Pump:** Shared by all 6 houses equally  

⚙️ **Customize in Settings** → "House Wiring & Pump Sharing" to match your building's actual wiring.

---

## 💡 Tips

- **First build is slowest** (Flutter downloads SDK, Gradle fetches dependencies) - 10-15 min
- **Subsequent builds:** 2-5 minutes
- **If stuck on "Running Gradle":** normal for first build, wait patiently ☕
- **Enable Gradle parallel builds** in `android/gradle.properties`: `org.gradle.parallel=true`

---

## 📞 Still Stuck?

1. Check the main **README.md** for detailed feature info
2. Verify `.github/workflows/build-apk.yml` doesn't have git commands at the top
3. Run `flutter clean` then rebuild
4. Delete `.gradle` cache: `rm -rf ~/.gradle/caches`

---

**Happy building! 🚀**
