# Comprehensive Guide: Building & Publishing HashScope Mobile to Google Play Store

This complete technical roadmap provides exact step-by-step instructions for converting **HashScope** into an Android mobile application and publishing it to the **Google Play Store** under your developer account (**TOJO P THOMAS**).

---

## 1. Choose Your Android Architecture

There are two primary approaches for packaging HashScope as an Android application:

| Approach | Technology | Best For | Build Complexity |
| :--- | :--- | :--- | :--- |
| **Option A: Capacitor Native Wrapper** *(Recommended for Offline Standalone App)* | `@capacitor/android` + Webview | Packages the entire HashScope UI, Email Dissector, Event Log Analyzer, and Triage Memory completely offline inside the APK/AAB. | 🟢 15 Minutes |
| **Option B: Trusted Web Activity (TWA)** | Google `bubblewrap` CLI | Wraps a live hosted HTTPS PWA/Web version. Google's official lightweight method. | 🟢 10 Minutes |

---

## 2. Option A: Building with Capacitor (Complete Offline Standalone App)

This method embeds your HTML/CSS/JS frontend directly into a standalone Android APK and `.aab` (Android App Bundle).

### Step 1: Install Capacitor CLI & Core
Open your terminal in the `hashscope` directory:
```bash
npm install @capacitor/core @capacitor/cli @capacitor/android
```

### Step 2: Initialize Capacitor Configuration
```bash
npx cap init "HashScope" "com.hashscope.forensics" --web-dir "ui"
```

### Step 3: Add the Android Native Platform
```bash
npx cap add android
```
This generates a full, ready-to-compile native Android Studio project inside the `/android` folder.

### Step 4: Configure App Icon & Permissions
1. Copy `assets/logo-512.png` into `android/app/src/main/res/` (or use the free `@capacitor/assets` tool to auto-generate all Android mipmap icon sizes: `npx @capacitor/assets generate --iconBackgroundColor '#0b0f17'`).
2. In `android/app/src/main/AndroidManifest.xml`, ensure internet permissions are declared:
```xml
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
```

### Step 5: Build the Signed Android App Bundle (.aab)
```bash
npx cap open android
```
In Android Studio:
1. Click **Build** ➔ **Generate Signed Bundle / APK**.
2. Choose **Android App Bundle (.aab)** and click **Next**.
3. Create a new Keystore file (e.g. `hashscope-release.keystore`):
   - Alias: `hashscope`
   - Password: Choose a strong password and save it securely.
   - First and Last Name: `TOJO P THOMAS`
4. Select Build Variant: `release`.
5. Click **Finish**.
6. Android Studio generates your production release bundle at:
   `android/app/release/app-release.aab`

---

## 3. Option B: Building with Google Bubblewrap (TWA)

If you have your HashScope web application hosted on an HTTPS domain (e.g. GitHub Pages, Vercel, or custom domain):

### Step 1: Install Bubblewrap CLI
```bash
npm install -g @bubblewrap/cli
```

### Step 2: Initialize Project from Manifest
```bash
bubblewrap init --manifest https://your-domain.com/manifest.json
```
Bubblewrap will prompt:
- **Application Name**: `HashScope Forensic Browser`
- **Short Name**: `HashScope`
- **Package ID**: `com.hashscope.forensics`
- **Starting URL**: `https://your-domain.com/ui/`
- **Icon**: Point to `assets/logo-512.png`

### Step 3: Compile AAB Bundle
```bash
bubblewrap build
```
This generates `app-release-bundle.aab`.

---

## 4. Google Play Console Submission Step-by-Step

### Step 1: Set Up Your Google Play Developer Account
1. Go to [Google Play Console](https://play.google.com/console).
2. Sign in with your Google account.
3. Pay the one-time **\$25 USD** developer registration fee.
4. Complete your identity verification (Government ID).

---

### Step 2: Create a New App
1. In the Google Play Console dashboard, click **Create app** (top-right).
2. Fill in the details:
   - **App name**: `HashScope - Forensic & SOC Browser`
   - **Default language**: `English (United States)`
   - **App or game**: `App`
   - **Free or paid**: `Free`
3. Accept the **Developer Program Policies** and **US export laws** checkboxes.
4. Click **Create app**.

---

### Step 3: Main Store Listing & Visual Assets
Navigate to **Grow** ➔ **Store presence** ➔ **Main store listing**:

1. **Short description** (up to 80 characters):
   > Zero-trace, isolated forensic web browser for SOC analysts & threat triage.

2. **Full description**:
   > HashScope is a specialized, zero-trace forensic browser architected by TOJO P THOMAS for digital forensics investigators, SOC analysts, and cybersecurity researchers.
   >
   > Features:
   > • 10 MB strict in-memory cache ceiling (0-byte disk footprint)
   > • Dedicated per-tab network isolation (Tor, VPN bridges, and Direct routing)
   > • Mobile User-Agent anti-cloaking switcher (iPhone iOS & Android emulation)
   > • Email Header & EML Forensic Dissector (SPF/DKIM/DMARC and spoofing checks)
   > • Windows Event Log Correlator & Instant Event ID Encyclopedia
   > • Live Forensic Triage Commands Memory (Windows & Linux incident response)
   > • Data Breach Email Inspector powered by global breach databases
   > • 1-Click Chain-of-Custody Cryptographic Evidence Capture (SHA-256)

3. **Graphic Assets**:
   - **App Icon**: Upload `assets/logo-512.png` (512x512 PNG, 32-bit color).
   - **Feature Graphic**: 1024 x 500 px JPEG/PNG banner (clean dark/white background with HashScope logo and title).
   - **Phone Screenshots**: Minimum 2 screenshots (1080 x 1920 or 1080 x 2400 px) showing HashScope's clean interface, Email Analyzer, and Event Log tabs.

---

### Step 4: Complete the App Content Section
Google requires completing the mandatory compliance checklists under **Policy** ➔ **App content**:

1. **Privacy Policy**:
   - Google requires a public HTTPS URL.
   - Example: `https://your-domain.com/privacy.html` or a Medium article (`medium.com/@tojopthomas`).
   - Summary to state: *HashScope collects zero telemetry, zero personal identifiers, and zero browsing history. All data is processed locally in volatile RAM.*
2. **Ads**: Select **No, my app does not contain ads**.
3. **App Access**: Select **All functionality is available without special access** (no login credentials required).
4. **Content Ratings**:
   - Category: Utility / Browser / Tools.
   - Answer the questionnaire (violence: None, mature content: None).
   - Rating awarded: **PEGI 3 / Everyone / Unrestricted Internet access**.
5. **Target Audience and Content**:
   - Target age: **18 and over** (Security Professionals & Researchers).
6. **Data Safety Form**:
   - "Does your app collect or share any user data?": Select **No**.
   - "Is all user data collected by your app encrypted in transit?": Select **Yes (N/A - No data collected)**.

---

### Step 5: Closed Testing Requirement (New Google Play Accounts)
> [!IMPORTANT]
> If your Google Play developer account was created after November 2023, Google requires a **14-day closed testing period** before production rollout:
> 1. Invite 12–20 email addresses (colleagues, students, or fellow cybersecurity researchers) to your **Closed Testing** track.
> 2. Testers opt-in via Google Play link and keep the app installed for 14 days.
> 3. After 14 days, the **Apply for Production** button becomes active.

---

### Step 6: Upload the Release Bundle & Publish!
1. In the left navigation, go to **Release** ➔ **Production** (or **Closed testing**).
2. Click **Create new release**.
3. In **App bundles**, upload `app-release.aab` (generated in Step 2 or 3).
4. Release name: `1.2.0 (Forensic Edition)`.
5. Release notes:
   ```
   Initial release of HashScope Forensic Browser:
   - Zero-trace in-memory ephemeral profile (10MB limit)
   - Per-tab proxy routing
   - Email header and EML forensic dissector
   - Windows event log correlation and Event ID encyclopedia
   - Live triage command memory for Windows & Linux
   ```
6. Click **Next** ➔ **Save** ➔ **Review release**.
7. Click **Start rollout to Production**!

Google's review team typically approves new apps within **24 to 72 hours**. Once approved, **HashScope** will be live worldwide on the Google Play Store!
