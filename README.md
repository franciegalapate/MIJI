# MIJI — Assistive Math App 🔢

An Android assistive learning app designed to help students with math by using their camera to scan equations, read them aloud, and guide them to a solution. MIJI also features self-learning modules for core math operations and a classroom session mode for teacher-led activities.

---

## ✨ Features

### 📷 Scan & Solve

- Point your camera at any math equation and MIJI auto-detects and captures it
- Recognized equations are displayed with a **phonetic reading** (e.g. _"two plus six minus seven"_)
- **CNN Confidence score** shown for the recognition result
- **Read Aloud** button speaks the equation using Android's Text-to-Speech engine
- **Answer input** via keyboard or microphone (speech-to-text)
- **Step-by-step solution** read aloud to the student
- Flash toggle and gallery upload for flexible image input

### 📚 Self-Learning Modules

Five math modules accessible from the home screen:

- Addition
- Subtraction
- Multiplication
- Division
- Mixed Operations

### 🏫 Classroom Session

A classroom mode accessible from the hamburger menu on any screen, allowing:

- **Create Lobby** — host a new session for students
- **Join Lobby** — enter a lobby code to join a teacher's session
- **How It Works** — in-app guide to classroom mode

### 👤 Profile

- View and manage your account (name, username, avatar)
- Configurable settings with toggle switches
- Logout with confirmation dialog
- Delete account with confirmation dialog

### 🧭 Navigation

- Shared bottom navigation bar across all screens (Home, Scan, Profile)
- Active tab highlighted in accent color

---

## 🛠️ Tech Stack

| Layer                | Technology                                                          |
| -------------------- | ------------------------------------------------------------------- |
| **Language**         | Kotlin                                                              |
| **Platform**         | Android (min SDK 24 / Android 7.0+, target SDK 36)                  |
| **IDE**              | Android Studio                                                      |
| **UI**               | XML Layouts, ConstraintLayout, Custom View (`ScanFrameView`)        |
| **Text-to-Speech**   | Android TTS (`android.speech.tts.TextToSpeech`)                     |
| **Math Recognition** | CNN-based detector _(backend integration via socket — in progress)_ |
| **Camera**           | CameraX _(integration in progress)_                                 |
| **Font**             | Inter (Regular, Medium, SemiBold, Bold)                             |

---

## 📁 Project Structure

```
app/src/main/java/com/miji/assistive_math/
└── ui/
    ├── HomeActivity.kt         # Home screen — module list + scan card + classroom menu
    ├── ScanActivity.kt         # Camera screen — live viewfinder, flash, upload, auto-capture
    ├── ScanResultActivity.kt   # Results screen — equation display, TTS, answer input, solution
    ├── ProfileActivity.kt      # Profile screen — user info, settings, logout, delete account
    ├── ScanFrameView.kt        # Custom View — draws the rounded corner scan frame overlay
    ├── BottomNavHelper.kt      # Shared helper — binds and highlights bottom nav tabs
    └── MenuHelper.kt           # Shared helper — shows the Classroom Session dialog

app/src/main/res/
├── layout/
│   ├── activity_home.xml           # Home screen layout
│   ├── activity_scan.xml           # Scan screen layout
│   ├── activity_scan_result.xml    # Scan result layout
│   ├── activity_profile.xml        # Profile layout
│   ├── bottom_nav.xml              # Shared bottom nav bar
│   ├── dialog_classroom_session.xml # Classroom session menu dialog
│   └── item_module.xml             # Single module row item
├── drawable/                       # Icons and shape backgrounds
├── font/                           # Inter font family
└── values/
    └── strings.xml                 # All UI strings
```

---

## 🔄 App Flow

```
HomeActivity
├── [Module tap]       → ModuleActivity (TODO)
├── [Scan card tap]    → ScanActivity
│                           └── [Capture / Upload] → ScanResultActivity
│                                   ├── [Read Aloud]     → TTS speaks equation
│                                   ├── [Submit Answer]  → Answer validation (TODO)
│                                   ├── [Read Solution]  → Step-by-step TTS (TODO)
│                                   └── [Scan Again]     → ScanActivity
└── [Menu icon]        → Classroom Session dialog (Create / Join / How It Works)

ProfileActivity
├── Settings toggles
├── [Logout]           → Confirmation dialog → LoginActivity (TODO)
└── [Delete Account]   → Confirmation dialog → Delete & logout (TODO)
```

---

## 🚀 Getting Started

### Prerequisites

- Android Studio Meerkat or later
- Android device or emulator running API 24+

### Setup

1. **Clone the repository**

   ```bash
   git clone https://github.com/franciegalapate/miji-assistive-math.git
   cd miji-assistive-math
   ```

2. **Open in Android Studio**
   - Open the project folder and let Gradle sync

3. **Run the app**
   - Connect a device or start an emulator, then click **Run**

> **Note:** Camera capture and math recognition require a running backend server (CNN detector + socket layer). The UI is fully implemented; backend integration is marked with `TODO` comments throughout the source.
