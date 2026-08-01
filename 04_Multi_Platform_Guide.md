# 04 - Multi-Platform Development Guide

## One Vision. Every Screen. Web, Android, Windows, Linux.

> Your users do not care what framework you used.
> They care that the app works beautifully on THEIR device.

---

## Table of Contents

1. [Platform Strategy](#1-strategy)
2. [Web Application](#2-web)
3. [Android Application](#3-android)
4. [Windows Application](#4-windows)
5. [Linux Application - All Distros](#5-linux)
6. [Cross-Platform Frameworks](#6-cross-platform)
7. [Shared Code Architecture](#7-shared-code)
8. [Distribution and Updates](#8-distribution)
9. [Platform-Specific UX Rules](#9-ux-rules)
10. [Multi-Platform Checklist](#10-checklist)

---

## 1. Platform Strategy

### Decision Matrix

| Question | If Yes | Recommendation |
|----------|--------|----------------|
| Need SEO / instant access? | Yes | Web first |
| Need camera, GPS, push? | Yes | Native Android |
| Need system tray, offline? | Yes | Desktop |
| Small team, all platforms? | Yes | Flutter / Tauri |
| Performance-critical? | Yes | Native per platform |

### Priority Order
1. Web (PWA) - reaches everyone
2. Android - largest mobile market
3. Windows - largest desktop market
4. Linux - developers and servers

---

## 2. Web Application

### Modern Stack (2025-2026)
    Framework:  Next.js 15+ / SvelteKit 2+ / Nuxt 4+
    Styling:    Tailwind CSS 4 + shadcn/ui
    State:      Zustand / Jotai / Svelte stores / Pinia
    API:        tRPC / REST+OpenAPI / GraphQL
    Auth:       Lucia / Clerk / Supabase Auth / Auth.js
    Deploy:     Cloudflare Pages / Vercel / Netlify

### PWA Essentials
- manifest.json with icons (192, 512, maskable).
- Service worker (Workbox) for offline.
- Web Push API. Install prompt (beforeinstallprompt).
- Lighthouse PWA score: 100.

### Performance
- LCP < 2.5s, INP < 200ms, CLS < 0.1
- JS bundle < 200KB gzipped initial.
- Code-split by route. WebP/AVIF images. Lazy load.

---

## 3. Android Application

### Native Stack (Recommended)
    Language:     Kotlin (100%)
    UI:           Jetpack Compose
    Architecture: MVVM + Clean Architecture
    DI:           Hilt
    Network:      Retrofit + OkHttp + Coroutines
    Local DB:     Room
    Async:        Coroutines + Flow
    Image:        Coil
    Crash:        Firebase Crashlytics / Sentry

### Requirements
- minSdk 26 (Android 8.0, covers 95%+)
- targetSdk 35
- Material You dynamic color. Edge-to-edge. Predictive back.

### Performance
- Cold start < 1.5s. Baseline Profiles.
- No main-thread work. LeakCanary for memory.
- App Bundle (.aab). R8. Compress resources.

### Distribution
- Google Play (primary). F-Droid (open source).
- Direct APK + GitHub Releases (beta).

---

## 4. Windows Application

### Options

| Option | Language | Best For |
|--------|----------|----------|
| WinUI 3 / Windows App SDK | C# / C++ | Modern UX, MSIX |
| WPF | C# | Enterprise, complex data |
| Tauri | Rust + Web | Tiny binary (3-10MB) |
| Electron | Node + Web | VS Code-like, web reuse |

### Windows UX Rules
- Light AND dark theme. Segoe UI Variable font.
- System accent color. Keyboard shortcuts.
- System tray for background apps. Right-click menus.
- Windows 11 snap layouts. MSIX packaging.

### Distribution
- Microsoft Store (MSIX). GitHub Releases (.exe via Inno Setup).
- winget manifest. Chocolatey / Scoop for dev tools.

---

## 5. Linux Application

### Toolkits

| Toolkit | Language | Ecosystem |
|---------|----------|-----------|
| GTK 4 + libadwaita | C / Rust / Python / JS | GNOME (Ubuntu, Fedora) |
| Qt 6 / KDE Frameworks | C++ / Python / Rust | KDE (Kubuntu, openSUSE) |
| Tauri | Rust + Web | Any distro |

### Packaging - Cover ALL Distros

| Format | Covers | Tool |
|--------|--------|------|
| AppImage | ALL distros | appimagetool |
| Flatpak | ALL distros (sandboxed) | flatpak-builder, Flathub |
| Snap | Ubuntu + others | snapcraft |
| .deb | Debian, Ubuntu, Mint | dpkg-deb |
| .rpm | Fedora, RHEL, openSUSE | rpmbuild |
| AUR | Arch, Manjaro | PKGBUILD |
| Nix | NixOS | flake.nix |

### Strategy
1. Build with Tauri or GTK/Qt.
2. AppImage + Flatpak (Flathub) + Snap.
3. .deb and .rpm for major distros.
4. AUR for Arch. GitHub Releases for all.

### Linux UX Rules
- Respect user theme. Wayland AND X11.
- freedesktop.org standards (icons, MIME, .desktop).
- D-Bus for IPC. XDG directories.
- No root required. Provide CLI alongside GUI.

---

## 6. Cross-Platform Frameworks

| Framework | Platforms | Language | Best For |
|-----------|-----------|----------|----------|
| Flutter | All | Dart | Beautiful custom UI |
| Tauri | Desktop (+mobile beta) | Rust+Web | Lightweight desktop |
| React Native | Mobile (+desktop) | JS/TS | Mobile-first, React skills |
| Kotlin Multiplatform | Mobile+Desktop+Web | Kotlin | Shared logic, native UI |
| .NET MAUI | Mobile+Desktop | C# | Enterprise, Microsoft |
| Electron | Desktop | JS/TS | Web reuse, large ecosystem |

### By Scenario
- Solo dev, all platforms: Flutter
- Web team, desktop only: Tauri
- Mobile first, React skills: React Native
- Enterprise, Microsoft: .NET MAUI
- Shared logic, native UI: Kotlin Multiplatform

---

## 7. Shared Code Architecture

### SHARE
- Business logic / domain layer
- API client / networking
- Data models / DTOs
- Validation rules
- Unit tests for logic

### DO NOT SHARE
- UI components (use native widgets)
- Platform APIs (camera, FS, notifications)
- Navigation patterns
- Platform-specific UX

### Architecture

    +-------------------+
    |   Platform UI     |  Native per platform
    +-------------------+
    |   View Models     |  Can be shared
    +-------------------+
    |   Domain Layer    |  SHARE: business rules
    +-------------------+
    |   Data Layer      |  SHARE: API, repos, models
    +-------------------+

---

## 8. Distribution and Updates

### Auto-Update

| Platform | Mechanism |
|----------|-----------|
| Web | CI/CD deploy = instant |
| Android | Play auto-update + in-app API |
| Windows | MSIX auto-update / Squirrel |
| Linux | Flatpak auto / Snap refresh / AppImageUpdate |

### CI/CD (GitHub Actions)
    on: push tag v*
    jobs:
      build-web:     Cloudflare Pages / Vercel
      build-android: AAB to Play Store (fastlane)
      build-windows: MSIX + EXE to GitHub Releases
      build-linux:   AppImage + Flatpak + deb + rpm

### Versioning
- Semantic: MAJOR.MINOR.PATCH
- Git tag every release. keep-a-changelog format.
- Show version in app settings.

---

## 9. Platform-Specific UX Rules

### Web
- URL-driven state. Browser back works. Keyboard shortcuts.
- Responsive 320px to 4K.

### Android
- Material Design 3. Predictive back. Pull-to-refresh.
- Bottom nav (max 5). Snackbar for transient, Dialog for decisions.

### Windows
- Fluent Design. Title bar controls. System tray.
- Ctrl+ shortcuts. Settings from hamburger menu.

### Linux
- GNOME HIG or KDE HIG. Header bar (GNOME) or menu bar (KDE).
- Keyboard-driven. XDG standards. Man page or --help.

---

## 10. Multi-Platform Checklist

- [ ] Works offline (or degrades gracefully)
- [ ] Dark mode tested
- [ ] Startup < 2 seconds
- [ ] Platform UX conventions followed
- [ ] Auto-update mechanism in place
- [ ] Crash reporting (Sentry / Crashlytics)
- [ ] Analytics (Umami / PostHog)
- [ ] Accessibility: screen reader, keyboard, contrast
- [ ] Localization: English + one other minimum
- [ ] CI/CD auto-builds on tag
- [ ] Clean install/uninstall
- [ ] App icon follows platform guidelines
- [ ] Privacy policy accessible in-app
- [ ] Feedback mechanism in settings

---

> Ship everywhere your users are.
> But ship NATIVE experience, not a lowest-common-denominator blob.
