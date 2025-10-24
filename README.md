# Azure AI ChatBot

> **Private Development Repository** - This is the private development repository. Public releases are published to [Jorbella-ai-public](https://github.com/Jordan-Fielding/Jorbella-ai-public).

A modern, feature-rich Windows desktop application for interacting with Azure OpenAI services. Built with WPF and .NET 9.0, featuring a beautiful gradient UI, customizable themes, and secure credential storage.

![Version](https://img.shields.io/badge/version-1.1.0-blue)
![.NET](https://img.shields.io/badge/.NET-9.0-purple)
![Platform](https://img.shields.io/badge/platform-Windows-lightgrey)
![Architecture](https://img.shields.io/badge/arch-x64%20%7C%20ARM64-green)

## Features

### 🤖 AI Chat Interface
- Real-time streaming responses with typewriter effect
- **Live message updates** in detail window while AI is typing
- Thinking indicator while AI processes requests
- Clean message bubbles with user/AI distinction
- Expandable detail view for longer responses
- Smooth animations and gradient backgrounds

### 🎨 Customizable Themes
- **6 Built-in Presets**:
  - Ocean Blue (Default) - Vibrant blue gradients
  - Dark Mode - Sleek dark interface
  - Purple Dream - Rich purple tones
  - Forest Green - Natural green palette
  - Sunset Orange - Warm orange hues
  - Jorbella - Dark with bright green accents
- **Custom Theme Editor** with live color preview
- **Consistent theme colors** across all UI elements
- 7 customizable color elements:
  - Title bar background
  - Window gradients (2 colors)
  - User message border & background
  - AI message border & background

### 🔒 Security & Privacy
- **Encrypted Storage**: API credentials encrypted using Windows DPAPI
- **Obfuscated Input**: API key displayed as bullets (●●●●●●)
- **Copy Protection**: API key field prevents copying
- **User-Specific**: Encryption tied to Windows user account
- **Local Storage**: Settings saved in `%AppData%\AzureAIChatBot`

### ⚙️ Settings Management
- Tabbed settings interface (API Config / Theme)
- First-run configuration wizard
- Live theme preview before saving
- Persistent settings across sessions
- Easy API credential updates

### 🔄 Auto-Update System
- **Automatic update checks** every 5 minutes
- **Manual update check** button (🔄 icon in title bar)
- **Update notifications** with release notes preview
- **One-click download** - opens browser to release page
- GitLab Releases API integration
- Version comparison and change detection

### 🎯 Modern UI/UX
- Borderless window with rounded corners
- Animated gradient backgrounds (30s loop)
- Drop shadows and blur effects
- **Fully draggable windows** (main, settings, and detail windows)
- Custom window controls (minimize, maximize, close)
- Responsive design

### 📎 File Attachments
- **Drag-and-drop** files anywhere in the input area
- Support for images and documents
- **Paste screenshots** directly from clipboard (Ctrl+V)
- Visual file preview with remove option
- 20MB file size limit

## System Requirements

- **OS**: Windows 10 or later (x64 or ARM64)
- **Runtime**: .NET 9.0 Runtime
- **Memory**: 100MB RAM minimum
- **Storage**: 50MB disk space

## Installation

**For end users:** Download the latest installer from the [Public Repository Releases](https://github.com/Jordan-Fielding/Jorbella-ai-public/releases)

**For developers:** See [Building from Source](#building-from-source) below.

## Configuration

### First Launch

1. Click the **⚙ Settings** icon in the title bar
2. Navigate to **API Configuration** tab
3. Enter your Azure OpenAI details:
   - **Endpoint URL**: Your Azure OpenAI endpoint
   - **API Key**: Your Azure OpenAI API key
   - **Deployment Name**: Your model deployment name
4. Click **Save**

### Azure OpenAI Setup

To use this application, you need an Azure OpenAI resource:

1. Go to [Azure Portal](https://portal.azure.com)
2. Create an **Azure OpenAI** resource
3. Deploy a model (e.g., GPT-4, GPT-3.5)
4. Copy the endpoint URL and API key
5. Enter these in the app settings

## Usage

### Chatting with AI

1. Type your message in the input box at the bottom
2. **Drag and drop files** or **paste screenshots** (Ctrl+V) to attach
3. Press **Enter** to send
4. Watch the AI response appear with typewriter effect
5. Click any AI message to view in detail window
6. Detail window updates **live** while AI is typing

### Changing Themes

1. Open **Settings** → **Theme** tab
2. Select a preset from the dropdown, or
3. Customize individual colors using color pickers
4. See live preview of color changes
5. Click **Save** to apply

### Auto-Updates

The app automatically checks the **public repository** for updates:
1. Checks [Jorbella-ai-public](https://github.com/Jordan-Fielding/Jorbella-ai-public) every 5 minutes
2. Click the **🔄** icon in title bar to check manually
3. When an update is available, you'll see a notification with release notes
4. Click **Yes** to open the public release page in your browser
5. Download and run the new installer

### Keyboard Shortcuts

- **Enter**: Send message
- **Ctrl+V**: Paste screenshot from clipboard
- **Esc**: Close detail window
- **Alt+F4**: Close application

## Building from Source

### Prerequisites

- Visual Studio 2022 or later
- .NET 9.0 SDK
- Windows 10 SDK

### Build Steps

```powershell
# Clone the repository
git clone <repository-url>
cd "AI Bot"

# Restore dependencies
dotnet restore

# Build for x64
dotnet publish -c Release -r win-x64 --self-contained false

# Build for ARM64
dotnet publish -c Release -r win-arm64 --self-contained false

# Create installer (requires Inno Setup)
& "C:\Program Files (x86)\Inno Setup 6\ISCC.exe" installer.iss
```

### Output Locations

- **x64 Build**: `bin\Release\net9.0-windows\win-x64\publish\`
- **ARM64 Build**: `bin\Release\net9.0-windows\win-arm64\publish\`
- **Installer**: `installer_output\AzureAIChatBot-Setup-v1.0.x.exe`

## Release Process

### Overview

Releases are published to the **public repository** ([Jorbella-ai-public](https://github.com/Jordan-Fielding/Jorbella-ai-public)) where users download them. The app's auto-update system checks the public repo for new versions.

### Creating a New Release

#### 1. Update Version Numbers

Update the version in these files:
- `AzureAIChatBot.csproj` - `<Version>`, `<FileVersion>`, `<AssemblyVersion>`
- `installer.iss` - `#define MyAppVersion`

#### 2. Build the Application

```powershell
# Build for both architectures
dotnet publish -c Release -r win-x64 --self-contained false
dotnet publish -c Release -r win-arm64 --self-contained false
```

#### 3. Create the Installer

```powershell
# Run Inno Setup to create the installer
& "C:\Program Files (x86)\Inno Setup 6\ISCC.exe" installer.iss
```

This creates: `installer_output\AzureAIChatBot-Setup-v1.x.x.exe`

#### 4. Publish to Public Repository

```powershell
# Use the publish script to push to public repo
.\publish-release.ps1 -Version "1.2.0"
```

The script automatically:
- ✅ Clones/updates the public repository
- ✅ Copies the installer to `releases/` folder
- ✅ Creates/updates `version.txt`
- ✅ Copies the README
- ✅ Commits and pushes to public repo
- ✅ Creates a Git tag (e.g., `v1.2.0`)
- ✅ Provides instructions for creating the GitLab Release

#### 5. Create GitLab Release

After running the script, manually create the release:

1. Go to: `https://github.com/Jordan-Fielding/Jorbella-ai-public/releases/new`
2. **Tag name**: `v1.2.0` (select the tag created by the script)
3. **Release title**: `Version 1.2.0`
4. **Description**: Add release notes and changelog
5. **Add asset link**:
   - **URL**: `https://raw.githubusercontent.com/Jordan-Fielding/Jorbella-ai-public/main/releases/AzureAIChatBot-Setup-v1.2.0.exe`
   - **Link title**: `AzureAIChatBot-Setup-v1.2.0.exe`
   - **Link type**: `Package`
6. Click **Create release**

#### 6. Commit to Private Repo (Optional)

```powershell
# Commit version changes to private repo
git add AzureAIChatBot.csproj installer.iss
git commit -m "Bump version to 1.2.0"
git push origin main
```

### Auto-Update System

The app checks the **public repository** for updates using a simple version file:
- **Version File**: `https://raw.githubusercontent.com/Jordan-Fielding/Jorbella-ai-public/main/version.txt`
- **Check Interval**: Every 5 minutes automatically
- **Manual Check**: Click the 🔄 icon in the title bar
- **Version Comparison**: Compares current version with version in `version.txt`
- **User Notification**: Shows popup when newer version is available
- **Download**: Opens browser to public releases page
- **No Authentication**: Public file, no token required

**How it works:**
1. App fetches `version.txt` from public repo
2. Compares version numbers (e.g., `1.1.0` vs `1.0.9`)
3. If newer version found, shows update notification
4. User clicks "Yes" to open releases page in browser
5. User downloads and runs the new installer

### Repository Structure

```
Jorbella-ai/            # Private development repo (this repo)
├── Source code
├── installer_output/   # Build output (gitignored)
└── publish-release.ps1 # Script to publish to public repo

Jorbella-ai-public/     # Public distribution repo
├── releases/           # Installer executables
├── version.txt         # Latest version number
└── README.md           # Public documentation
```

## Project Structure

```
AI Bot/
├── Models/              # Data models
│   ├── AppSettings.cs
│   ├── AzureOpenAIConfig.cs
│   └── ThemeSettings.cs
├── Services/            # Business logic
│   ├── AzureOpenAIService.cs
│   ├── IAzureOpenAIService.cs
│   └── SettingsService.cs
├── Views/               # UI windows
│   ├── MainWindow.xaml
│   ├── SettingsWindow.xaml
│   └── MessageDetailWindow.xaml
├── Converters/          # XAML converters
│   └── ValueConverters.cs
├── App.xaml             # Application entry
├── icon.svg             # Application icon (source)
├── icon.ico             # Application icon (compiled)
└── installer.iss        # Inno Setup script
```

## Technologies Used

- **Framework**: .NET 9.0 / WPF
- **Language**: C# 12
- **UI**: XAML with custom styles
- **Security**: Windows DPAPI
- **Packaging**: Inno Setup
- **AI**: Azure OpenAI API

## Architecture

- **MVVM Pattern**: Separation of UI and business logic
- **INotifyPropertyChanged**: Live UI updates
- **Async/Await**: Non-blocking AI requests
- **Dependency Injection**: Service-based architecture
- **Resource Dictionaries**: Dynamic theme switching

## Security Notes

- API credentials are encrypted at rest using Windows DPAPI
- Encryption is user-specific (cannot be decrypted by other users)
- No credentials are stored in plain text
- Settings file location: `%AppData%\AzureAIChatBot\settings.json`
- API key is obfuscated in the UI

## Troubleshooting

### App won't start
- Ensure .NET 9.0 Runtime is installed
- Check Windows Event Viewer for errors
- Try running as administrator

### Can't save settings
- Check write permissions to `%AppData%`
- Ensure antivirus isn't blocking the app
- Try running as administrator

### AI responses fail
- Verify Azure OpenAI endpoint is correct
- Check API key is valid and not expired
- Ensure deployment name matches your Azure resource
- Check internet connection

### Theme not applying
- Try restarting the application
- Reset to default theme and try again
- Check settings file isn't corrupted

## Development

### Local Setup

1. Clone this repository
2. Open `AzureAIChatBot.sln` in Visual Studio 2022
3. Restore NuGet packages
4. Build and run (F5)

### Testing Updates

To test the auto-update system:
1. Build and install a version with a lower version number
2. Create a release in the public repo with a higher version
3. Run the app and wait for update notification (or click 🔄)

### Contributing

This is a private development repository. For contributions:
1. Create a feature branch
2. Make your changes
3. Test thoroughly
4. Submit a merge request

## License

This project is for personal and educational use.

## Author

**Jordan Fielding**

## Acknowledgments

- Azure OpenAI for AI capabilities
- Inno Setup for installer creation
- .NET team for the amazing framework

## Changelog

### Version 1.1.0 (2025-10-24)

- **Configurable API Version**: Added API Version field in settings to support different Azure OpenAI API versions
- **o3-mini Support**: Now compatible with o3-mini model (requires API version 2024-12-01-preview or later)
- **Settings Enhancement**: API version can be customized per deployment needs
- **Backward Compatibility**: Defaults to 2024-12-01-preview for new installations

### Version 1.0.8 (2025-10-23)

- **Auto-update system**: Automatic update checks every 5 minutes
- **Update notifications**: Shows release notes preview when updates available
- **Manual update check**: Click 🔄 icon in title bar
- **GitLab Releases integration**: Fetches latest version from GitLab API
- **One-click updates**: Opens browser to download page

### Version 1.0.7 (2025-10-23)

- Initial auto-update implementation
- GitLab Releases API integration
- Update notification system

### Version 1.0.4 (2025-10-23)

- **Live message updates**: Detail window now updates in real-time while AI is typing
- **Improved drag-and-drop**: Drop files anywhere in the input area
- **Theme consistency**: All UI elements now follow the selected theme
- **Fixed tab buttons**: Settings tabs now use dynamic theme colors
- **Better window dragging**: Settings window fully draggable from title bar
- Added Jorbella theme preset
- Added secret easter egg feature 👏

### Version 1.0.3 (2025-10-22)

- Chat history management
- Session persistence
- Auto-generated chat titles
- Translucency toggle

### Version 1.0.2 (2025-10-22)

- File attachment support
- Screenshot paste functionality
- Message detail window

### Version 1.0.1 (2025-10-22)

- Theme system improvements
- Settings window enhancements

### Version 1.0.0 (2025-10-22)

- Initial release
- Azure OpenAI integration
- 5 theme presets + custom themes
- Encrypted credential storage
- x64 and ARM64 support
- Professional installer
- Typewriter effect for responses
- Settings management system

## Support

For issues, questions, or feature requests, please open an issue on the repository.

---

**Made with ❤️ using .NET and Azure OpenAI**
