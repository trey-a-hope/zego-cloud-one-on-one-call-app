# ZEGOCLOUD Video Call App

A Flutter video-meeting app built on [ZEGOCLOUD's prebuilt Call UIKit](https://www.zegocloud.com/docs/uikit/callkit-flutter/overview) with [Clerk](https://clerk.com) for sign-in. Sign in, type a meeting ID, choose whether to join with audio and video on, and you're in a call with anyone else who entered the same ID.

## Features

- **Sign in / sign up / sign out** with Clerk's prebuilt `ClerkAuthentication` UI.
- **Join Meeting** screen: enter a meeting ID and toggle *Connect to audio* and *Turn on my video* before joining.
- **Meeting**: `ZegoUIKitPrebuiltCall` with the camera and mic set from those toggles, plus a top bar with minimize, member list and sound-effect buttons. Your email is used as the user ID and display name.

## How it works

```
lib/
├── main.dart                      # loads .env, wraps the app in ClerkAuth
├── data/config/env_config.dart    # singleton that reads ZEGO_APP_ID, ZEGO_APP_SIGN, CLERK_KEY
└── presentation/
    ├── login_page.dart            # Clerk sign-in
    ├── join_meeting_page.dart     # meeting ID + audio/video toggles
    └── meeting_page.dart          # ZegoUIKitPrebuiltCall
```

`ClerkAuthBuilder` shows the login page when signed out and the join page when signed in.

## Tech stack

- Flutter, Dart `^3.7.2`
- `zego_uikit_prebuilt_call` 4.16
- `clerk_flutter` (beta), `flutter_dotenv`, `gap`

## Getting started

### Environment variables

The app needs a `.env` file in the project root (it's bundled as an asset and isn't committed):

```
ZEGO_APP_ID="<your ZEGOCLOUD app ID>"
ZEGO_APP_SIGN="<your ZEGOCLOUD app sign>"
CLERK_KEY="<your Clerk publishable key>"
```

- Get the app ID and app sign from the ZEGOCLOUD console.
- Get the publishable key from your Clerk dashboard.
- Don't put spaces around the `=` signs, and never commit `.env`.

### Run

```sh
flutter pub get
flutter run
```

Video calls need camera and microphone permissions, so test on a real device or a desktop with a webcam.
