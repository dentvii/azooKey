# azooKey Application Architecture

This document provides a visual architectural map of the azooKey application to help you understand how features are organized and connected.

---

## 🗺️ Visual Architecture Map

```
azooKey Application
├── 📱 MAIN APP (Settings & Configuration Hub)
│   ├── ⚙️ Settings & Configuration
│   │   ├── General Settings (input methods, keyboard behavior)
│   │   ├── Theme Management (colors, visual customization)
│   │   └── Custom Keyboard Builder (create/edit custom layouts)
│   │
│   ├── 📊 Data Management
│   │   ├── Dictionary Updates (download/install new dictionaries)
│   │   └── User Data (user dictionary, learning data, backup/restore)
│   │
│   ├── 🎓 User Guidance
│   │   ├── Keyboard Setup Tutorial (installation guide)
│   │   ├── Tips & Help (feature explanations)
│   │   └── Update Information (changelog)
│   │
│   └── 🔧 Developer Settings (debug, experimental features)
│
└── ⌨️ KEYBOARD EXTENSION (The Input Interface)
    │
    ├── 🎨 VISUAL LAYER (What You See)
    │   ├── Key Views (individual buttons, styles, states)
    │   ├── Key Layouts
    │   │   ├── QWERTY Layout
    │   │   ├── Custom Layouts (user-created)
    │   │   └── Emoji Keyboard
    │   ├── Result Bar (candidate suggestions above keyboard)
    │   ├── Cursor Bar (long-press space for precise editing)
    │   ├── Tab Bar (azooKey icon → custom tabs & settings)
    │   └── Themes (colors, fonts, styling)
    │
    ├── ⌨️ CUSTOM KEYBOARD SYSTEM
    │   ├── Custom Tabs (multiple custom layouts)
    │   ├── Custom Keys (user-defined actions & labels)
    │   ├── Key Names (customizable text/symbols)
    │   ├── Flick Keys (swipe patterns)
    │   └── Import/Export (share layouts)
    │
    ├── 😀 EMOJI & SPECIAL INPUT
    │   ├── Emoji Picker (categories, search)
    │   ├── Kaomoji (Japanese emoticons)
    │   └── Recent/Frequent Tracking
    │
    ├── 🌍 LOCALIZATION
    │   ├── Multi-language UI
    │   ├── Language-specific Layouts
    │   └── Localized Strings
    │
    ├── 🧠 INPUT INTELLIGENCE (The Brain)
    │   │
    │   ├── [1] INPUT MANAGER
    │   │   ├── Raw Input Processing (romaji → kana)
    │   │   ├── Composition State Management
    │   │   └── Text Buffer Management
    │   │       ↓
    │   ├── [2] PREDICTION LAYER (Before Conversion)
    │   │   ├── Pre-composition Suggestions
    │   │   ├── Context-aware Predictions
    │   │   ├── Dictionary-based Suggestions
    │   │   └── Frequency Ranking
    │   │       ↓
    │   ├── [3] LIVE CONVERSION (Optional Real-time)
    │   │   └── Automatic Kana→Kanji as you type
    │   │       ↓
    │   ├── [4] CONVERSION ENGINE (Neural AI)
    │   │   ├── Neural Models (Zenzai v3.1)
    │   │   ├── Dictionary Data (LOUDS structure)
    │   │   ├── Grammar Understanding
    │   │   └── Multiple Candidates
    │   │       ↓
    │   ├── [5] CANDIDATE DISPLAY
    │   │   └── Show conversion options in Result Bar
    │   │       ↓
    │   └── [6] POST-PREDICTION LAYER (After Confirmation)
    │       ├── Next Word Suggestions
    │       ├── Phrase Completion
    │       ├── Context from Just-entered Text
    │       └── Learning from User Patterns
    │
    ├── 🎯 ACTION LAYER (User Interactions)
    │   ├── Key Press Handling
    │   ├── Touch Gesture Processing
    │   ├── Action Coordination
    │   └── State Management
    │
    └── 📋 ADDITIONAL FEATURES
        ├── Clipboard History
        ├── Advanced Text Editing
        └── Error Reporting

🔗 SHARED INFRASTRUCTURE
    └── AzooKeyCore Package
        ├── KeyboardViews (shared UI components)
        ├── KeyboardThemes (theme system)
        ├── KeyboardExtensionUtils (keyboard utilities)
        ├── AzooKeyUtils (general utilities)
        └── SwiftUIUtils (SwiftUI helpers)
```

---

## 🔄 Data Flow: From Key Press to Text Output

```
     USER TAPS KEY
           ↓
    ┌──────────────┐
    │ Action Layer │ ← Handles touch/gesture
    └──────────────┘
           ↓
    ┌──────────────┐
    │Input Manager │ ← Processes input (e.g., "k" + "a" → "か")
    └──────────────┘
           ↓
    ┌───────────────────┐
    │ Prediction Layer  │ ← Suggests words BEFORE conversion
    │  (Pre-composition)│   "か" → suggests "家", "傘", "書く"
    └───────────────────┘
           ↓
    ┌────────────────────┐
    │ Live Conversion    │ ← Optional: auto-convert in real-time
    │   (if enabled)     │
    └────────────────────┘
           ↓
    ┌────────────────────┐
    │ Conversion Engine  │ ← Neural AI converts kana to kanji
    │   (Neural Zenzai)  │   "かいぎ" → "会議", "会義", "開議"
    └────────────────────┘
           ↓
    ┌────────────────────┐
    │ Candidate Display  │ ← Shows options in Result Bar
    │   (Result Bar)     │   User sees: [会議] [会義] [開議]
    └────────────────────┘
           ↓
      USER SELECTS ✓
           ↓
    ┌────────────────────┐
    │Text Confirmed: 会議│ ← Inserted into app
    └────────────────────┘
           ↓
    ┌─────────────────────┐
    │Post-Prediction Layer│ ← Suggests what comes NEXT
    │ (After confirmation)│   After "会議" → suggests "は", "で", "を"
    └─────────────────────┘
           ↓
    TEXT APPEARS IN APP
```

---

---

## 📚 Study Guide: Key Concepts

### What is azooKey?
A Japanese keyboard app with two parts:
1. **Main App** - Where you configure and customize
2. **Keyboard Extension** - The actual keyboard you type on

### Core Features to Understand

#### 1️⃣ Custom Keyboards (Custard System)
- **What**: Create your own keyboard layouts
- **Where**: Main App → Customize
- **Features**: Custom tabs, custom keys, custom names/labels
- **Files**: `CustardManager.swift`, `UserMadeCustard.swift`

#### 2️⃣ Emoji Keyboard
- **What**: Emoji and kaomoji input
- **Where**: Keyboard Extension → Emoji tab
- **Features**: Categories, search, recent/frequent
- **Data**: `azooKey_emoji_dictionary_storage/`

#### 3️⃣ Localization
- **What**: Multi-language support
- **Where**: Throughout app and keyboard
- **Files**: `Resources/Localizable.xcstrings`

#### 4️⃣ Input Intelligence Pipeline
The "brain" that converts your typing to Japanese text:

**Step 1: Input Manager** (`InputManager.swift`)
- Takes raw key presses
- Converts romaji to kana (e.g., "ka" → "か")

**Step 2: Prediction (Before)** (`PredictionManager.swift`)
- Suggests words BEFORE you convert
- Based on context and frequency

**Step 3: Live Conversion** (`LiveConversionManager.swift`)
- Optional: Auto-converts as you type
- No need to press conversion key

**Step 4: Conversion Engine** (Neural AI)
- The AI that converts kana to kanji
- Uses neural models: `zenz-v3.1-small-gguf/`
- Uses dictionary: `azooKey_dictionary_storage/`
- Data structure: LOUDS (fast lookups)

**Step 5: Post-Prediction (After)**
- Suggests what word comes NEXT
- Learns from your patterns

#### 5️⃣ Themes
- **What**: Visual customization
- **Where**: Main App → Theme
- **Files**: `AzooKeyCore/Sources/KeyboardThemes/`
- **Assets**: `Resources/Designs.xcassets/`

#### 6️⃣ Action Management
- **What**: Handles all user interactions
- **Files**: `KeyboardActionManager.swift`
- **Does**: Key presses, gestures, state coordination

---

## 📂 Where Things Live (File Locations)

### Main App (`MainApp/`)
```
MainApp/
├── ContentView.swift (main screen)
├── Customize/ (custom keyboard builder)
├── Theme/ (theme selection)
├── Setting/ (settings screens)
├── DataUpdateView/ (dictionary updates)
├── EnableAzooKeyView/ (setup tutorial)
└── Tips/ (help & tips)
```

### Keyboard Extension (`Keyboard/`)
```
Keyboard/
├── Display/
│   ├── KeyboardViewController.swift (entry point)
│   ├── KeyboardActionManager.swift (actions)
│   ├── InputManager.swift (input processing)
│   ├── PredictionManager.swift (predictions)
│   └── LiveConversionManager.swift (live conversion)
└── Dictionary/ (dictionary data files)
```

### Shared Code (`AzooKeyCore/`)
```
AzooKeyCore/Sources/
├── KeyboardViews/ (UI components)
├── KeyboardThemes/ (theme system)
├── KeyboardExtensionUtils/ (utilities)
├── AzooKeyUtils/ (general utils)
└── SwiftUIUtils/ (SwiftUI helpers)
```

---

## 🎯 Quick Reference

| Feature | Main Component | Location |
|---------|---------------|----------|
| Custom keyboards | CustardManager | `AzooKeyUtils/Custard/` |
| Emoji input | Emoji dictionary | `azooKey_emoji_dictionary_storage/` |
| Themes | ThemeManager | `KeyboardThemes/` |
| Input processing | InputManager | `Keyboard/Display/` |
| Predictions | PredictionManager | `Keyboard/Display/` |
| Conversion (AI) | Neural models | `zenz-v3.1-*-gguf/` |
| Localization | String catalog | `Resources/Localizable.xcstrings` |
| Settings UI | Setting views | `MainApp/Setting/` |

---

## 🔗 Learn More

- **Folder Structure**: [FILE_1_PROJECT_FOLDERS.md](FILE_1_PROJECT_FOLDERS.md)
- **Feature Details**: [FILE_2_PROJECT_FEATURES.md](FILE_2_PROJECT_FEATURES.md)
- **Build Instructions**: [README.md](README.md)
- **Contributing**: [docs/CONTRIBUTING.md](docs/CONTRIBUTING.md)
