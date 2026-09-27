# HashScope for Apple macOS (.DMG)

## 1. Why Apple macOS Requires macOS or Cloud CI to Build `.DMG`

Apple macOS applications and `.dmg` disk images require Apple-proprietary APIs (`hdiutil` and Apple codesigning/notarization tools) that Apple restricts strictly to macOS machines. Attempting to build macOS `.dmg` on Windows will result in:
> `⨯ Build for macOS is supported only on macOS`

---

## 2. Automated Free Cloud Build via GitHub Actions (Recommended)

A ready-to-use GitHub Actions workflow has been configured for HashScope at:
`.github/workflows/build-all-platforms.yml`

When you push this repository to GitHub:
1. GitHub automatically spins up a free Apple macOS runner (`macos-latest`).
2. It compiles **`HashScope-1.2.0-arm64.dmg`** (for Apple Silicon M1/M2/M3/M4) and **`HashScope-1.2.0-x64.dmg`** (for Intel Macs).
3. The `.dmg` files are automatically attached to your GitHub Releases page ready for download!

---

## 3. Compiling Locally on a Mac

If you or a colleague have a Mac computer, building the `.dmg` takes 1 single terminal command:

```bash
# 1. Clone repository
git clone https://github.com/tojo54/hashscope.git
cd hashscope

# 2. Install dependencies & build DMG
npm install
npm run build:mac
```

Output:
- `dist/HashScope-1.2.0-arm64.dmg` (Apple Silicon M1/M2/M3/M4)
- `dist/HashScope-1.2.0-x64.dmg` (Intel Mac)
