# Cast Receiver for 2026 Countdown

This is a custom Cast receiver that displays the countdown to 2026 on your TV.

## Setup Instructions

### 1. Deploy to GitHub Pages

1. **Create a new GitHub repository** (e.g., `2026-countdown-cast-receiver`)
2. **Upload all files** from this folder to the repository:
   - `index.html`
   - `manifest.json`
   - `background.js`
3. **Enable GitHub Pages**:
   - Go to repository Settings → Pages
   - Select source: `main` branch (or `master`)
   - Click Save
4. **Note your GitHub Pages URL**: `https://yourusername.github.io/2026-countdown-cast-receiver/`
   - This URL must be accessible via HTTPS

### 2. Register Receiver in Google Cast Console

1. Go to [Google Cast Console](https://cast.google.com/publish)
2. Sign in with your Google account
3. Click **"Add New Application"**
4. Select **"Custom Receiver"**
5. Enter:
   - **Application Name**: 2026 Countdown
   - **Receiver URL**: `https://yourusername.github.io/2026-countdown-cast-receiver/index.html`
6. Click **"Save"**
7. **Copy the Application ID** (Receiver ID) - it looks like: `ABCD1234`

### 3. Update Android App

1. Open `app/src/main/java/com/kns/resolutions/cast/CastOptionsProvider.kt`
2. Replace `CastMediaControlIntent.DEFAULT_MEDIA_RECEIVER_APPLICATION_ID` with your Receiver ID:
   ```kotlin
   .setReceiverApplicationId("YOUR_RECEIVER_ID_HERE")
   ```
3. Rebuild and deploy the app

### 4. Test

1. Connect your phone and TV to the same Wi-Fi network
2. Open the app on your phone
3. Click the Cast icon
4. Select your TV
5. The countdown should now display on your TV!

## Files

- `index.html` - Main receiver HTML with countdown display
- `manifest.json` - Cast receiver manifest
- `background.js` - Background script (required but empty)

## Troubleshooting

- **TV shows Cast icon but no countdown**: Make sure the Receiver ID is correctly set in `CastOptionsProvider.kt`
- **Receiver not found**: Verify GitHub Pages is enabled and the URL is accessible
- **Countdown not updating**: Check that both devices are on the same Wi-Fi network
