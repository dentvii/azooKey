# azooKey Project Features

This document outlines the key features and capabilities of azooKey, a Japanese keyboard app for iOS/iPadOS.

## Core Features

### 1. Neural Kana-Kanji Conversion System (Zenzai)
**High-accuracy text conversion powered by neural networks**

azooKey uses the "Zenzai" neural Kana-Kanji conversion system for highly accurate Japanese text input. The conversion engine is implemented as a separate package: [AzooKeyKanaKanjiConverter](https://github.com/ensan-hcl/AzooKeyKanaKanjiConverter).

**Key components:**
- Neural network models (`zenz-v3.1-small-gguf/`, `zenz-v3.1-xsmall-gguf/`)
- LOUDS-based dictionary data structure for efficient lookups
- Multiple model sizes for different performance/accuracy tradeoffs

---

### 2. Live Conversion (ライブ変換)
**Real-time conversion as you type**

Live conversion automatically converts your input to Kanji in real-time without requiring explicit conversion key presses. This provides a more fluid typing experience.

**Implementation:**
- `LiveConversionManager.swift` - Manages live conversion state
- Automatically triggered during typing
- Can be toggled on/off in settings

---

### 3. Custom Keyboard Layouts (カスタムタブ)
**Fully customizable keyboard layouts and keys**

Users can create custom keyboard layouts with custom keys, tabs, and behaviors. This is powered by the [CustardKit](https://github.com/ensan-hcl/CustardKit) package.

**Capabilities:**
- Custom key definitions with user-defined actions
- Multiple custom tabs
- Custom key layouts and arrangements
- Import/export custom layouts

**Related folders:**
- `MainApp/Customize/` - Customization UI

---

### 4. Input Methods
**Multiple input styles for different user preferences**

- **Romaji Input (ローマ字入力)** - Type using Roman characters
- **Direct Input (ダイレクト入力)** - Direct kana input
- Configurable through MainApp settings

**Related code:**
- `InputManager.swift` - Handles input method switching
- Settings for input style configuration

---

### 5. Prediction and Completion
**Intelligent text prediction and auto-completion**

**Types of prediction:**
- **Pre-composition prediction** - Suggestions before conversion
- **Post-composition prediction (確定後の予測変換)** - Suggestions after confirming text
- Context-aware suggestions based on typing history

**Implementation:**
- `PredictionManager.swift` - Prediction logic
- Dictionary-based suggestions

---

### 6. Learning and Personalization
**Adaptive learning from user input**

The keyboard learns from user behavior to improve suggestions and conversion accuracy over time.

**Features:**
- Learn frequently used words
- Adapt to user's writing style
- Store user dictionary entries
- Managed through the conversion engine

---

### 7. Advanced UI Components

#### Result Bar (リザルトバー)
Displays conversion candidates in a horizontal bar above the keyboard. Users can swipe to select candidates.

#### Cursor Bar (カーソルバー)
Activated by long-pressing the space key, allows precise cursor movement for text editing.

#### Tab Bar (タブバー)
Accessed via the azooKey icon button, provides quick access to:
- Custom tabs
- Settings shortcuts
- Special input modes

---

### 8. Theme System
**Customizable keyboard appearance**

Users can customize the visual appearance of the keyboard with themes.

**Features:**
- Color customization
- Key styling
- Background options
- Pre-built themes

**Implementation:**
- `AzooKeyCore/Sources/KeyboardThemes/` - Theme system
- `MainApp/Theme/` - Theme selection UI
- `Resources/Designs.xcassets/` - Theme assets

---

### 9. Data Management

#### Dictionary Updates
Users can update dictionary data to get the latest conversion improvements.

**Related:**
- `MainApp/DataUpdateView/` - Dictionary update UI
- `azooKey_dictionary_storage/` - Dictionary data submodule

#### User Data
- User dictionary entries
- Learning data
- Custom layout definitions
- Settings and preferences

---

### 10. Clipboard History
**Access and manage clipboard history**

Store and recall previously copied text. See [clipboard_history.md](docs/clipboard_history.md) for details.

---

### 11. Multilingual Support
**Localized for multiple languages**

While primarily a Japanese input keyboard, the UI supports multiple languages through localization.

**Implementation:**
- `Resources/Localizable.xcstrings` - Localized strings
- Support for Japanese, English, and other languages

---

### 12. Settings and Configuration
**Extensive customization options**

The MainApp provides comprehensive settings for:
- Input behavior configuration
- Visual customization
- Feature toggles
- Advanced/internal settings for developers
- Privacy settings

**Related folders:**
- `MainApp/Setting/` - Settings UI
- `MainApp/General/` - General settings
- `MainApp/InternalSetting/` - Developer settings

---

### 13. Tutorial and Help
**Onboarding and user guidance**

**Features:**
- Keyboard installation guide
- Feature tips and tutorials
- Update information
- Helpful hints for new users

**Related:**
- `MainApp/EnableAzooKeyView/` - Keyboard setup tutorial
- `MainApp/Tips/` - User tips
- `UpdateInformationView.swift` - Changelog and updates

---

### 14. Privacy and Security
**Privacy-focused design**

- Privacy manifests (`PrivacyInfo.xcprivacy`)
- Minimal data collection
- User data stored locally
- Transparent privacy policies in `docs/policies/`

---

### 15. Keyboard Extension Architecture
**Efficient and responsive keyboard implementation**

**Key architectural components:**
- `KeyboardViewController.swift` - Entry point, loads UI
- `KeyboardActionManager` - Manages user interactions
- `InputManager` - Handles conversion and input state
- SwiftUI-based modern UI implementation
- Shared code between MainApp and Keyboard for consistency

---

## Development Features

### Testing Infrastructure
- Unit tests in `azooKeyTests/`
- UI tests in `MainAppUITests/`
- See [tests.md](docs/tests.md) for testing guidelines

### Modular Architecture
- Swift Package Manager for shared code
- Clean separation of concerns
- Reusable components

### Open Source
- MIT License
- Active community on [Discord](https://discord.gg/dY9gHuyZN5)
- Contributions welcome
- See [CONTRIBUTING.md](docs/CONTRIBUTING.md)

---

## Platform Support

- **iOS** - iPhone support
- **iPadOS** - iPad-optimized layouts
- **macOS** - See [azooKey-Desktop](https://github.com/azooKey/azooKey-Desktop) for the macOS version

---

## Distribution

- Available on [App Store](https://apps.apple.com/jp/app/azookey-%E8%87%AA%E7%94%B1%E8%87%AA%E5%9C%A8%E3%81%AA%E3%82%AD%E3%83%BC%E3%83%9C%E3%83%BC%E3%83%89%E3%82%A2%E3%83%97%E3%83%AA/id1542709230)
- Beta versions available via [TestFlight](https://testflight.apple.com/join/x6TKEeB2)
- GitHub Sponsors for project support
