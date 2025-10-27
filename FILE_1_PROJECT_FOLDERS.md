# azooKey Project Folder Structure

This document explains the organization of folders in the azooKey project.

## Main Directories

### `AzooKeyCore/`
**Swift Package with shared modules used across the entire project**

A Swift Package containing common functionality shared between the main app and keyboard extension. This is the core library of azooKey.

**Sub-folders:**
- `Sources/` - Source code for various modules:
  - `KeyboardThemes/` - Theme and styling system for the keyboard
  - `KeyboardExtensionUtils/` - Utilities for keyboard extension functionality
  - `SwiftUIUtils/` - SwiftUI helper components and utilities
  - `KeyboardViews/` - SwiftUI views for the keyboard UI
  - `AzooKeyUtils/` - General utility functions and helpers
- `Tests/` - Unit tests for AzooKeyCore modules

See [AzooKeyCore/README.md](AzooKeyCore/README.md) for more details.

---

### `MainApp/`
**Main iOS application for settings and configuration**

The main application that users install from the App Store. This app allows users to configure keyboard settings, customize layouts, manage themes, and enable the keyboard extension.

**Key sub-folders:**
- `Assets.xcassets/` - App icons, images, and visual assets
- `Customize/` - Custom keyboard layout and key customization features
- `DataSet/` - Data management and dataset handling
- `DataUpdateView/` - UI for updating dictionary data
- `EnableAzooKeyView/` - Tutorial screens for enabling the keyboard
- `General/` - General settings and configurations
- `InternalSetting/` - Internal/developer settings
- `Setting/` - User-facing settings screens
- `Theme/` - Theme selection and customization
- `Tips/` - User tips and help content
- `Utils/` - Utility functions for the main app
- `Resources/` - Additional resources specific to MainApp
- `Settings.bundle/` - iOS Settings app integration

**Key files:**
- `MainApp.swift` - App entry point
- `ContentView.swift` - Main view of the application
- `UpdateInformationView.swift` - Update information and changelog display

---

### `Keyboard/`
**Keyboard extension implementation**

The actual keyboard extension that runs when users type. This is the core input method implementation.

**Sub-folders:**
- `Display/` - Core keyboard display logic
  - `KeyboardViewController.swift` - Main entry point for the keyboard extension
  - `KeyboardActionManager.swift` - Manages user actions and input
  - `InputManager.swift` - Handles text input and conversion state
  - `LiveConversionManager.swift` - Live conversion functionality
- `Dictionary/` - Dictionary data files (binary format)
  - `louds/` - LOUDS data structure files
  - `cb/` - Dictionary callback data
  - `p/` - Prediction data

**Key files:**
- `Info.plist` - Keyboard extension configuration
- `Keyboard.entitlements` - App extension entitlements
- `PrivacyInfo.xcprivacy` - Privacy manifest

---

### `Resources/`
**Shared resources for both MainApp and Keyboard**

Resources that are shared between the main app and keyboard extension.

**Contents:**
- `AzooKeyIcon-Regular.otf` - Custom icon font
- `Designs.xcassets/` - Design assets (colors, images)
- `Localizable.xcstrings` - Localized strings for multiple languages
- `InfoPlist.xcstrings` - Localized Info.plist strings

---

### `azooKeyTests/`
**Test suite for the project**

Contains unit tests and integration tests, primarily for the Keyboard implementation.

**Sub-folders:**
- `KeyboardTests/` - Tests for keyboard functionality

---

### `MainAppUITests/`
**UI tests for the main application**

Contains UI tests that verify the main app's user interface and user flows.

---

### `azooKey_dictionary_storage/`
**Dictionary data submodule**

Git submodule containing dictionary data files. Can be switched to different commits to use different dictionary versions. Historical versions are also available on [Google Drive](https://drive.google.com/drive/folders/1Kh7fgMFIzkpg7YwP3GhWTxFkXI-yzT9E?usp=sharing).

---

### `azooKey_emoji_dictionary_storage/`
**Emoji dictionary data submodule**

Git submodule containing emoji dictionary data.

---

### `zenz-v3.1-small-gguf/` and `zenz-v3.1-xsmall-gguf/`
**Neural conversion model files**

Contains the Zenzai neural Kana-Kanji conversion system model files in GGUF format. These are used for high-accuracy text conversion.

---

### `docs/`
**Project documentation**

Contains development documentation and guides.

**Contents:**
- `CONTRIBUTING.md` - Contribution guidelines
- `overview.md` - Project architecture overview (in Japanese)
- `tests.md` - Testing guide
- `settings.md` - Settings documentation
- `keyboard_layout_behavior.md` - Keyboard layout behavior notes
- `clipboard_history.md` - Clipboard history feature notes
- `advice_for_azooKey_based_development.md` - Development advice
- `view_controller_memory_leak.md` - Memory leak documentation
- `images/` - Documentation images
- `policies/` - Project policies
- `visions/` - Future vision documents

---

### `.github/`
**GitHub-specific configuration**

Contains GitHub Actions workflows, issue templates, and other GitHub-specific configurations.

---

### `azooKey.xcodeproj/`
**Xcode project file**

The Xcode project configuration that ties everything together. Open this file in Xcode to build and run the project.

---

## Building the Project

1. Clone with submodules:
   ```bash
   git clone https://github.com/azooKey/azooKey --recursive
   ```

2. Open `azooKey.xcodeproj` in Xcode

3. Build and run (⌘+R)

Requires an Apple Developer Account (free tier is sufficient) and the latest version of Xcode.
