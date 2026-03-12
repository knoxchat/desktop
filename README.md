## KnoxChat Desktop App

### Gatekeeper / "App is Damaged"

When downloading KnoxChat.app (or `.dmg`) from [Releases](https://github.com/knoxchat/desktop/releases), macOS adds a **quarantine** extended attribute. Since the app is not code-signed and notarized by Apple, Gatekeeper blocks it with:

> "KnoxChat.app" is damaged and can't be opened. You should move it to the Trash.

The app is **not actually damaged** — this is macOS blocking unsigned downloaded software.

#### Quick Fix (remove quarantine attribute)

```bash
# If the .app is in Downloads:
xattr -cr ~/Downloads/KnoxChat.app

# If the .app is in Applications:
xattr -cr /Applications/KnoxChat.app

# If you downloaded a .dmg, mount it first, then:
xattr -cr /Volumes/KnoxChat/KnoxChat.app
```

#### Alternative: Right-Click Open

1. Right-click (or Control-click) on **KnoxChat.app**
2. Select **Open**
3. Click **Open** in the confirmation dialog

This bypasses Gatekeeper for that specific app instance.

```bash
export APPLE_SIGNING_IDENTITY="Developer ID Application: Your Name (TEAM_ID)"
export APPLE_ID="your@email.com"
export APPLE_PASSWORD="app-specific-password"   # App-specific password from appleid.apple.com
export APPLE_TEAM_ID="YOUR_TEAM_ID"
npx tauri build
```

> **Note**: `xattr -cr` is a testing-only workaround. 
