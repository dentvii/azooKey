# azooKey Application Architecture

This document provides an architectural view of the azooKey application, organized to mirror how the application is represented from both a user and developer perspective. The application is split into two main views: **Keyboard** and **App**.

---

## Keyboard View Architecture

The keyboard extension is the core input interface that users interact with when typing. It's a complex system comprising several layers and features.

### 🎨 Visual & Presentation Layer

#### **Keyboard UI Components** (`AzooKeyCore/Sources/KeyboardViews/`)
The visual representation of the keyboard that users see and touch.

**Key Components:**
- **Key Views** - Individual key buttons with various styles and states
- **Key Layouts** - Different keyboard layouts (QWERTY, custom, emoji, etc.)
- **Result Bar** - Conversion candidate display above the keyboard
- **Cursor Bar** - Precise text cursor control (activated via long-press space)
- **Tab Bar** - Quick access to custom tabs and settings (azooKey icon button)

**Supporting Infrastructure:**
- `KeyboardViewController.swift` - Main entry point, orchestrates the entire keyboard UI
- Theme system for visual customization
- SwiftUI-based modern responsive interface

---

### ⌨️ Custom Keyboard System

#### **Custom Keyboards** (`MainApp/Customize/`, `CustardKit`)
Users can create fully customized keyboard layouts with their own keys and behaviors.

**Features:**
- **Custom Tabs** - Multiple user-defined keyboard layouts
- **Custom Keys** - User-defined keys with custom actions and labels
- **Key Names** - Customizable key labels and symbols
- **Import/Export** - Share and load custom keyboard configurations
- **Flick Keys** - Custom flick input patterns for advanced users

**Implementation:**
- `CustardManager.swift` - Manages custom keyboard definitions
- `UserMadeCustard.swift` - User-created keyboard data structures

---

### 😀 Emoji & Special Characters

#### **Emoji Keyboard**
Dedicated emoji and kaomoji input interface.

**Features:**
- Emoji picker with categories
- Kaomoji (顔文字) support
- Recent and frequently used tracking
- Search functionality

**Data:**
- `azooKey_emoji_dictionary_storage/` - Emoji dictionary submodule
- Emoji conversion and suggestions

---

### 🌍 Localization System

#### **Multi-language Support** (`Resources/Localizable.xcstrings`)
The keyboard interface is available in multiple languages.

**Components:**
- Localized UI strings for all keyboard elements
- Language-specific key layouts
- Culturally appropriate input methods
- `InfoPlist.xcstrings` - Localized system strings

---

### 🧠 Input & Intelligence Layer

This is where the "magic" happens - converting user input into meaningful text.

#### **Input Management** (`Keyboard/Display/InputManager.swift`)
The brain of text input and conversion.

**Responsibilities:**
- Raw input processing (romaji → kana)
- Composition state management
- Interaction with conversion engine
- Text buffer management

---

#### **Prediction Layer** (`Keyboard/Display/PredictionManager.swift`)
**Pre-Composition Prediction** - Suggestions before conversion

**Features:**
- Context-aware word suggestions
- Dictionary-based predictions
- Learning from user input patterns
- Frequency-based ranking

---

#### **Conversion Engine** (Neural Kana-Kanji Conversion)
**The Core Intelligence** - Powered by Zenzai neural network

**Components:**
- `zenz-v3.1-small-gguf/` and `zenz-v3.1-xsmall-gguf/` - Neural models
- `Keyboard/Dictionary/louds/` - LOUDS dictionary data structure
- `azooKey_dictionary_storage/` - Dictionary data submodule
- External package: `AzooKeyKanaKanjiConverter`

**What it does:**
- Converts kana input to kanji with high accuracy
- Understands context and grammar
- Learns from user corrections
- Multiple conversion candidates

---

#### **Post-Prediction Layer** (Post-Composition Prediction)
**After confirmation** - Suggestions for what comes next

**Features:**
- Next word prediction after confirming text
- Context-aware suggestions based on just-entered text
- Phrase completion
- Learned patterns from user behavior

---

#### **Live Conversion** (`Keyboard/Display/LiveConversionManager.swift`)
**Real-time automatic conversion** as you type (ライブ変換)

**Behavior:**
- Automatically converts input to kanji without explicit conversion key presses
- Fluid typing experience
- Toggleable in settings

---

### 🎯 Action & Behavior Layer

#### **Action Management** (`Keyboard/Display/KeyboardActionManager.swift`)
Handles all user interactions and coordinates keyboard behavior.

**Responsibilities:**
- Key press handling
- Touch gesture processing
- Action coordination between components
- State management across the keyboard

---

### 🎨 Theme & Styling Layer

#### **Keyboard Themes** (`AzooKeyCore/Sources/KeyboardThemes/`)
Visual customization system for keyboard appearance.

**Components:**
- Color schemes
- Key styling (borders, shadows, gradients)
- Background options
- Pre-built and custom themes

**Resources:**
- `Resources/Designs.xcassets/` - Theme colors and assets
- `Resources/AzooKeyIcon-Regular.otf` - Custom icon font

---

### 📋 Additional Features

#### **Clipboard History**
Store and recall previously copied text.

#### **Text Editing**
Advanced cursor movement and text selection tools.

#### **Error Reporting** (`ReportSubmissionHelper.swift`)
Diagnostic and error reporting capabilities.

---

## App View Architecture

The main application (MainApp) is the settings and configuration hub where users customize their keyboard experience.

### ⚙️ Settings & Configuration Layer

#### **General Settings** (`MainApp/Setting/`, `MainApp/General/`)
Core keyboard behavior configuration.

**Features:**
- Input method selection (romaji, direct kana)
- Keyboard layout preferences
- Feature toggles
- Behavior customization

---

#### **Theme Management** (`MainApp/Theme/`)
Visual customization interface.

**Features:**
- Theme selection
- Color customization
- Preview functionality
- Save and manage custom themes

---

#### **Custom Keyboard Builder** (`MainApp/Customize/`)
Interface for creating and managing custom keyboards.

**Features:**
- Visual keyboard layout editor
- Key configuration
- Tab management
- Import/export custom layouts

---

### 📊 Data Management Layer

#### **Dictionary Updates** (`MainApp/DataUpdateView/`)
Keep conversion dictionaries current.

**Features:**
- Check for dictionary updates
- Download and install new dictionary data
- Version management

#### **User Data** (`MainApp/DataSet/`)
Manage user-specific data and learning.

**Features:**
- User dictionary entries
- Learning data management
- Backup and restore
- Data reset options

---

### 🎓 Onboarding & Help Layer

#### **Keyboard Setup** (`MainApp/EnableAzooKeyView/`)
Tutorial for enabling the keyboard extension.

**Features:**
- Step-by-step installation guide
- System settings navigation
- Verification of successful installation

#### **Tips & Help** (`MainApp/Tips/`)
User guidance and feature discovery.

**Features:**
- Feature explanations
- Usage tips
- Helpful hints for new users

#### **Update Information** (`UpdateInformationView.swift`)
Changelog and version history.

---

### 🔧 Developer & Internal Settings

#### **Internal Settings** (`MainApp/InternalSetting/`)
Advanced options for developers and power users.

**Features:**
- Debug options
- Experimental features
- Performance metrics
- Detailed configuration

---

## Shared Core Infrastructure

### 🎁 AzooKeyCore Package

A Swift Package containing shared functionality between keyboard and app.

**Modules:**
- `KeyboardViews/` - Shared UI components
- `KeyboardThemes/` - Theme system
- `KeyboardExtensionUtils/` - Keyboard utilities
- `AzooKeyUtils/` - General utilities
- `SwiftUIUtils/` - SwiftUI helpers

---

## Data Flow Summary

```
User Input (Key Press)
    ↓
KeyboardActionManager (Action Processing)
    ↓
InputManager (Input Processing)
    ↓
┌─────────────────────────────────────┐
│  Prediction Layer (Pre-composition)  │ ← Dictionary Data
└─────────────────────────────────────┘
    ↓
LiveConversionManager (Optional real-time conversion)
    ↓
Neural Conversion Engine (Kana → Kanji)
    ↓
Candidate Display (Result Bar)
    ↓
User Selection
    ↓
┌─────────────────────────────────────┐
│ Post-Prediction Layer (Next word)    │ ← Learning Data
└─────────────────────────────────────┘
    ↓
Text Output (To Application)
```

---

## Technology Stack

- **Language:** Swift, SwiftUI
- **Platform:** iOS, iPadOS
- **Architecture:** App Extension + Main App
- **AI/ML:** Neural network (Zenzai) for conversion
- **Data Structures:** LOUDS for efficient dictionary lookups
- **Package Management:** Swift Package Manager
- **Build System:** Xcode

---

## Key Concepts

- **Keyboard Extension** - The input method that runs system-wide
- **Main App** - Configuration and settings hub
- **Conversion** - Kana to Kanji transformation
- **Prediction** - Intelligent text suggestions
- **Live Conversion** - Automatic real-time conversion
- **Custom Keyboards** - User-defined layouts (Custard system)
- **Themes** - Visual appearance customization
- **Learning** - Adaptive behavior from user input

---

For more detailed information:
- **Folder Structure:** See [FILE_1_PROJECT_FOLDERS.md](FILE_1_PROJECT_FOLDERS.md)
- **Feature Details:** See [FILE_2_PROJECT_FEATURES.md](FILE_2_PROJECT_FEATURES.md)
- **Build Instructions:** See [README.md](README.md)
- **Development Guide:** See [docs/CONTRIBUTING.md](docs/CONTRIBUTING.md)
