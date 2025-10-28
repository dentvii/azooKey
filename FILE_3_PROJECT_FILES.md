# azooKey Project Files Reference

This document provides a reference for important files in the azooKey project and their purposes.

## Root Level Files

### `README.md`
**Project overview and quick start guide**

The main readme file providing:
- Project description (in Japanese)
- App Store and TestFlight links
- Build instructions
- Contribution guidelines
- Links to documentation

---

### `LICENSE`
**MIT License**

azooKey is licensed under the MIT License. Copyright (c) 2020-2025 Keita Miwa (ensan).

---

### `.gitignore`
**Git ignore rules**

Specifies files and directories to exclude from version control (build artifacts, user-specific files, etc.).

---

### `.gitmodules`
**Git submodules configuration**

Defines the dictionary storage submodules:
- `azooKey_dictionary_storage`
- `azooKey_emoji_dictionary_storage`

---

### `.swiftlint.yml`
**SwiftLint configuration**

Code style and linting rules for maintaining consistent Swift code quality.

---

## AzooKeyCore Files

### `AzooKeyCore/Package.swift`
**Swift Package Manager manifest**

Defines the AzooKeyCore package structure:
- Package dependencies
- Target definitions
- Platform requirements
- Module exports

---

### `AzooKeyCore/README.md`
**AzooKeyCore documentation**

Documentation specific to the shared core library modules.

---

## MainApp Key Files

### `MainApp/MainApp.swift`
**Application entry point**

The main SwiftUI `@main` App structure that launches the MainApp.

**Key responsibilities:**
- App lifecycle management
- Initial setup
- Root view configuration

---

### `MainApp/ContentView.swift`
**Main application view**

The primary view displayed when users open the app.

**Features:**
- Navigation structure
- Main menu/dashboard
- Access to all settings and features

---

### `MainApp/UpdateInformationView.swift`
**Update changelog and information**

Displays what's new in recent updates, changelog, and version information.

**Size:** ~44KB - contains extensive update history

---

### `MainApp/Info.plist`
**App configuration**

iOS app configuration including:
- Bundle identifier
- Version information
- Required permissions
- Supported devices
- Background modes

---

### `MainApp/azooKey.entitlements`
**App entitlements**

Declares app capabilities and permissions required by the main app.

---

### `MainApp/PrivacyInfo.xcprivacy`
**Privacy manifest**

Declares privacy-related information and data usage for App Store compliance.

---

## Keyboard Extension Key Files

### `Keyboard/Display/KeyboardViewController.swift`
**Keyboard extension entry point**

The main view controller for the keyboard extension. This is where the keyboard lifecycle begins.

**Key methods:**
- `viewDidLoad()` - Initializes keyboard UI and managers
- Entry point for all keyboard functionality

**Size:** ~25KB

---

### `Keyboard/Display/KeyboardActionManager.swift`
**Action handling and coordination**

Manages all user interactions with the keyboard.

**Responsibilities:**
- Handle key presses
- Coordinate with InputManager
- Manage keyboard state
- Process user actions

**Size:** ~35KB - Core keyboard logic

---

### `Keyboard/Display/InputManager.swift`
**Input and conversion management**

Handles text input and manages the conversion process.

**Key functions:**
- Interact with KanaKanjiConverter API
- Manage conversion state
- Handle displayed text through DisplayedTextManager
- Process input through LiveConversionManager

**Size:** ~52KB - Largest file in Display/

---

### `Keyboard/Display/LiveConversionManager.swift`
**Live conversion functionality**

Manages real-time conversion as users type.

**Size:** ~7KB

---

### `Keyboard/Display/PredictionManager.swift`
**Prediction and suggestions**

Handles predictive text and completion suggestions.

**Size:** ~3KB

---

### `Keyboard/Display/ReportSubmissionHelper.swift`
**Error reporting and diagnostics**

Helps collect and submit error reports and diagnostic information.

**Size:** ~19KB

---

### `Keyboard/Info.plist`
**Keyboard extension configuration**

Extension-specific configuration:
- Extension point identifier
- Principal class
- Required settings

---

### `Keyboard/Keyboard.entitlements`
**Keyboard extension entitlements**

Permissions and capabilities for the keyboard extension.

---

## Resources Files

### `Resources/Localizable.xcstrings`
**Localized strings catalog**

All user-facing text in multiple languages using the new string catalog format (.xcstrings).

**Size:** ~281KB - Contains extensive translations

---

### `Resources/InfoPlist.xcstrings`
**Localized Info.plist strings**

Localized versions of Info.plist keys.

---

### `Resources/AzooKeyIcon-Regular.otf`
**Custom icon font**

OpenType font file containing custom icons used throughout the app.

---

## Project Configuration Files

### `azooKey.xcodeproj/`
**Xcode project**

The Xcode project file that ties together all targets:
- MainApp target
- Keyboard extension target
- Test targets
- Build configurations
- Signing settings

**To open:** Double-click in Finder or run `open azooKey.xcodeproj`

---

## Documentation Files

### `docs/overview.md`
**Architecture overview (Japanese)**

Detailed explanation of project architecture:
- Component descriptions
- Data flow
- Key concepts and terminology
- Module relationships

**Size:** ~5KB

---

### `docs/CONTRIBUTING.md`
**Contribution guidelines**

How to contribute to the project:
- Development workflow
- Code standards
- PR process
- Testing requirements

---

### `docs/tests.md`
**Testing guide**

Instructions for running and writing tests.

---

### `docs/settings.md`
**Settings documentation**

Documentation of available settings and their effects.

---

### `docs/keyboard_layout_behavior.md`
**Keyboard layout behavior notes**

Technical notes on keyboard layout behavior and edge cases.

---

### `docs/clipboard_history.md`
**Clipboard history feature**

Documentation for the clipboard history feature.

---

### `docs/advice_for_azooKey_based_development.md`
**Development advice**

Tips and best practices for developing with or extending azooKey.

---

### `docs/view_controller_memory_leak.md`
**Memory leak documentation**

Known issues and solutions related to view controller memory management.

---

## Dictionary Data Files

### `Keyboard/Dictionary/louds/`
**LOUDS data structure files**

Contains dictionary data in LOUDS (Level-Order Unary Degree Sequence) format for efficient trie operations.

---

### `Keyboard/Dictionary/cb/`
**Callback dictionary data**

Dictionary callback data files.

---

### `Keyboard/Dictionary/p/`
**Prediction data**

Data files for text prediction functionality.

---

## Test Files

### `azooKeyTests/`
**Main test directory**

Contains unit and integration tests for keyboard functionality.

---

### `MainAppUITests/MainAppUITests.swift`
**UI tests**

Automated UI tests for the main application.

---

## Build and Configuration Files

### `.swiftpm/`
**Swift PM configuration** (in AzooKeyCore)

Swift Package Manager build configuration and resolved dependencies.

---

## File Naming Conventions

### Swift Files
- **PascalCase**: Class and struct names (e.g., `KeyboardViewController.swift`)
- **Descriptive names**: Files named after their primary class/component
- **Manager suffix**: Classes that coordinate functionality (e.g., `InputManager.swift`)
- **View suffix**: SwiftUI views (e.g., `ContentView.swift`)

### Resource Files
- **PascalCase**: Asset catalogs (e.g., `Assets.xcassets`)
- **lowercase with extension**: Standard resources (e.g., `.xcstrings`, `.plist`)

### Documentation Files
- **UPPERCASE**: Important docs (e.g., `README.md`, `LICENSE`, `CONTRIBUTING.md`)
- **snake_case**: Technical docs (e.g., `clipboard_history.md`)

---

## Finding Specific Files

### Quick reference by task:

**Modifying keyboard behavior:**
- Start with `Keyboard/Display/KeyboardActionManager.swift`
- Check `Keyboard/Display/InputManager.swift`

**Changing app UI:**
- Main app: `MainApp/ContentView.swift`
- Settings: `MainApp/Setting/`
- Keyboard UI: `AzooKeyCore/Sources/KeyboardViews/`

**Updating localization:**
- Modify `Resources/Localizable.xcstrings`

**Working with themes:**
- Theme system: `AzooKeyCore/Sources/KeyboardThemes/`
- Theme UI: `MainApp/Theme/`

**Adding tests:**
- Keyboard tests: `azooKeyTests/KeyboardTests/`
- UI tests: `MainAppUITests/`

**Documentation updates:**
- User docs: `docs/`
- Technical overview: `docs/overview.md`
- Contributing: `docs/CONTRIBUTING.md`

---

## File Sizes Reference

Largest source files:
1. `Keyboard/Display/InputManager.swift` - ~52KB
2. `MainApp/UpdateInformationView.swift` - ~44KB
3. `Keyboard/Display/KeyboardActionManager.swift` - ~35KB
4. `Keyboard/Display/KeyboardViewController.swift` - ~25KB

Largest resource:
- `Resources/Localizable.xcstrings` - ~281KB (all translations)
