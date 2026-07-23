# Adaptive Icon Assets for Android (Play Store)

Two new files are included:
- `adaptive-icon-background.png` — solid brand-color background layer
- `adaptive-icon-foreground.png` — the ledger glyph, transparent background, sized to Android's "safe zone"

## Why these exist

Android displays app icons in different shapes depending on the phone (circle, rounded square, squircle, etc.) using something called an "adaptive icon" — a background layer + a foreground layer that Android combines and masks automatically. Play Store requires this format for your app listing icon.

## How to use them

When you get to [pwabuilder.com](https://pwabuilder.com) to package your app for Android:
1. Enter your live GitHub Pages URL and let it generate the Android package
2. In the packaging options, look for an icon/image section — it may auto-generate an adaptive icon from your existing `icon-512.png`, which is often good enough
3. If it asks for background/foreground layers specifically (or if the auto-generated icon looks cropped oddly), upload `adaptive-icon-background.png` as the background and `adaptive-icon-foreground.png` as the foreground

If PWABuilder handles it automatically without asking, you likely won't need to manually upload these — but they're here in case you (or I) need to fine-tune it later, or if you ever move to building a fully native Android project in Android Studio.
