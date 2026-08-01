# 04 - Multi-Platform Development Guide

## Build Once, Deploy Everywhere Intelligently

> "The best platform strategy is the one that reaches every user without multiplying your effort."

---

## Table of Contents

1. [Platform Strategy Overview](#1-platform-strategy-overview)
2. [Web Development (PWA + SSR)](#2-web-development-pwa--ssr)
3. [Android Development](#3-android-development)
4. [Windows Development](#4-windows-development)
5. [Linux Development (All Distros)](#5-linux-development-all-distros)
6. [Cross-Platform Frameworks](#6-cross-platform-frameworks)
7. [Shared Architecture Patterns](#7-shared-architecture-patterns)
8. [Platform-Specific Security](#8-platform-specific-security)
9. [Distribution and Updates](#9-distribution-and-updates)
10. [Multi-Platform Checklist](#10-multi-platform-checklist)

---

## 1. Platform Strategy Overview

### 1.1 Decision Matrix

| Factor | Web (PWA) | Native Mobile | Native Desktop | Cross-Platform |
|--------|-----------|---------------|----------------|----------------|
| Reach | Maximum | High | Medium | High |
| Performance | Good | Best | Best | Good-Excellent |
| Hardware Access | Limited | Full | Full | Good |
| Offline Support | Good (SW) | Best | Best | Good |
| Development Cost | Lowest | High | High | Medium |
| Maintenance | Lowest | Medium | Medium | Low-Medium |
| Update Speed | Instant | Store review | Store/manual | Varies |
| Install Friction | None | Low | Medium | Low |

### 1.2 Recommended Strategy

For maximum reach with minimum cost:

1. Primary: Progressive Web App (PWA) - reaches everyone
2. Mobile: Native Android (Kotlin) + Native iOS (Swift) OR Flutter
3. Desktop: Tauri 2.0 (Rust backend + Web frontend)
4. Shared: Core business logic in Rust/Go compiled to all targets

### 1.3 Architecture Layers

Layer 1 - Core Logic (Shared): Business rules, data models, algorithms
Layer 2 - Platform Adapters: OS-specific APIs, hardware access
Layer 3 - UI Layer: Platform-native or framework-based rendering
Layer 4 - Distribution: Platform-specific packaging and updates

---

## 2. Web Development (PWA + SSR)

### 2.1 Modern Web Stack

| Layer | Recommended | Why |
|-------|------------|-----|
| Framework | Next.js 15 (App Router) | SSR, SSG, ISR, RSC, best DX |
| Language | TypeScript 5.x | Type safety, better DX |
| Styling | Tailwind CSS 4 | Utility-first, fast, consistent |
| State | Zustand / Jotai | Lightweight, performant |
| Data Fetching | TanStack Query v5 | Caching, dedup, background refetch |
| Forms | React Hook Form + Zod | Performance, validation |
| Animation | Framer Motion / Motion One | GPU-accelerated, declarative |
| Testing | Vitest + Playwright | Fast unit + E2E testing |
| Build | Turbopack / Vite | Fast builds, HMR |

### 2.2 PWA Requirements

A proper PWA must have:

- Service Worker for offline support and caching
- Web App Manifest with all icon sizes
- HTTPS (mandatory)
- Responsive design (mobile-first)
- Fast loading (under 3 seconds on 3G)
- Installable (add to home screen)
- Push notifications (Web Push API)
- Background sync for offline actions
- App-like navigation (no browser chrome)

### 2.3 Service Worker Strategy

Cache strategy by resource type:

| Resource | Strategy | Cache Duration |
|----------|----------|---------------|
| App Shell (HTML, CSS, JS) | Cache First | Until new version |
| API Responses | Network First, fallback cache | 5 minutes |
| Images | Cache First + LRU | 30 days |
| Fonts | Cache First | 1 year |
| Analytics | Network Only | No cache |

### 2.4 Web Performance Targets

| Metric | Target |
|--------|--------|
| Largest Contentful Paint (LCP) | Under 2.0s |
| First Input Delay (FID) | Under 100ms |
| Cumulative Layout Shift (CLS) | Under 0.05 |
| Time to First Byte (TTFB) | Under 200ms |
| Total Blocking Time (TBT) | Under 200ms |
| Lighthouse Score | 95+ all categories |

### 2.5 Web Security Headers

Every web app must send these headers:

- Strict-Transport-Security (HSTS)
- Content-Security-Policy (CSP)
- X-Content-Type-Options: nosniff
- X-Frame-Options: DENY
- Referrer-Policy: strict-origin-when-cross-origin
- Permissions-Policy (restrict camera, mic, geolocation)
- Cross-Origin-Opener-Policy: same-origin
- Cross-Origin-Embedder-Policy: require-corp

---

## 3. Android Development

### 3.1 Modern Android Stack

| Layer | Recommended | Why |
|-------|------------|-----|
| Language | Kotlin 2.x | Official, modern, safe |
| UI | Jetpack Compose | Declarative, modern, Google-backed |
| Architecture | MVVM + Clean Architecture | Testable, maintainable |
| DI | Hilt (Dagger) | Compile-time, Android-optimized |
| Networking | Retrofit + OkHttp + Ktor | Type-safe, interceptors |
| Database | Room (SQLite) | ORM, compile-time verification |
| Async | Kotlin Coroutines + Flow | Structured concurrency |
| Image Loading | Coil 3 | Kotlin-first, Compose support |
| Navigation | Compose Navigation | Type-safe, deep linking |
| Testing | JUnit 5 + MockK + Compose Test | Comprehensive coverage |

### 3.2 Android Security Best Practices

- Use Android Keystore for cryptographic keys
- Enable certificate pinning (OkHttp CertificatePinner)
- Encrypt SharedPreferences (EncryptedSharedPreferences)
- Use ProGuard/R8 for code obfuscation
- Disable USB debugging in release builds
- Implement root/tamper detection (SafetyNet/Play Integrity)
- Use BiometricPrompt for biometric auth
- Enable network security config (cleartext traffic disabled)
- Implement app attestation for API calls
- Use ContentProvider permissions correctly

### 3.3 Android Performance

- Use Baseline Profiles for faster startup
- Implement lazy loading (LazyColumn, LazyRow)
- Use WorkManager for background tasks
- Optimize APK size (App Bundle, resource shrinking)
- Profile with Android Studio Profiler
- Use StrictMode in development
- Implement proper lifecycle management
- Avoid memory leaks (use WeakReference, lifecycle-aware components)

### 3.4 Distribution

- Google Play Store (primary)
- F-Droid (for open-source)
- Direct APK download (with auto-update via in-app update API)
- Samsung Galaxy Store (optional)
- Amazon Appstore (optional)

---

## 4. Windows Development

### 4.1 Modern Windows Stack

| Layer | Recommended | Why |
|-------|------------|-----|
| Framework | WinUI 3 / Windows App SDK | Modern, Fluent Design |
| Alternative | Tauri 2.0 (Rust + Web) | Cross-platform, tiny binary |
| Language | C# (.NET 9) / Rust | Performance, safety |
| UI | XAML / WebView2 | Native look, web tech |
| Database | SQLite / LiteDB | Embedded, zero-config |
| Installer | MSIX / WiX / Inno Setup | Modern packaging |
| Auto-Update | Squirrel / Velopack | Seamless updates |

### 4.2 Windows Security

- Use Windows Hello for authentication
- Implement DPAPI for data protection
- Sign executables with code signing certificate
- Enable Windows Defender SmartScreen compatibility
- Use AppContainer for sandboxing
- Implement proper UAC manifest
- Encrypt sensitive data with AES-256
- Validate all file paths (prevent path traversal)
- Use Windows Credential Manager for secrets
- Implement AMSI (Antimalware Scan Interface) integration

### 4.3 Windows Performance

- Use WinRT APIs for async operations
- Implement virtualization for long lists
- Use native AOT compilation (.NET 9)
- Minimize startup time (lazy initialization)
- Use memory-mapped files for large data
- Profile with Windows Performance Analyzer
- Implement proper disposal (IDisposable pattern)
- Use Span and Memory for zero-copy operations

### 4.4 Distribution

- Microsoft Store (MSIX package)
- Winget (Windows Package Manager)
- Chocolatey (package manager)
- Scoop (package manager)
- Direct download (with auto-updater)
- GitHub Releases

---

## 5. Linux Development (All Distros)

### 5.1 Modern Linux Stack

| Layer | Recommended | Why |
|-------|------------|-----|
| Toolkit | GTK4 + libadwaita | GNOME-native, modern |
| Alternative | Qt6 / QML | KDE-native, cross-platform |
| Alternative | Tauri 2.0 | Web tech, tiny binary |
| Language | Rust / C / Vala / C++ | Performance, native |
| Package | Flatpak + AppImage + .deb + .rpm | Universal coverage |
| Build | Meson / CMake / Cargo | Standard build systems |
| IPC | D-Bus | Linux standard |
| Config | GSettings / XDG directories | Standard locations |

### 5.2 Distro Compatibility

Support all major distros:

| Distro Family | Package Format | Examples |
|--------------|----------------|----------|
| Debian/Ubuntu | .deb | Ubuntu, Debian, Linux Mint, Pop!_OS |
| Red Hat/Fedora | .rpm | Fedora, RHEL, CentOS, openSUSE |
| Arch | PKGBUILD (AUR) | Arch, Manjaro, EndeavourOS |
| Universal | Flatpak | All distros (Flathub) |
| Universal | AppImage | All distros (no install needed) |
| Universal | Snap | Ubuntu-focused, works elsewhere |
| Nix | Nix package | NixOS, any distro |

### 5.3 Linux Security

- Use seccomp for system call filtering
- Implement AppArmor / SELinux profiles
- Use D-Bus permissions for IPC security
- Store secrets in libsecret / GNOME Keyring / KWallet
- Set proper file permissions (0600 for secrets)
- Use XDG directories (never hardcode paths)
- Implement Wayland compatibility (no X11-only APIs)
- Use namespaces for sandboxing
- Validate all environment variables
- Implement proper signal handling

### 5.4 Linux Performance

- Use io_uring for async I/O
- Implement proper memory management (Rust ownership / RAII)
- Use Wayland-native rendering
- Implement D-Bus activation (lazy start)
- Use GSettings for configuration (cached)
- Minimize dependencies (static linking where possible)
- Profile with perf, Valgrind, sysprof
- Use epoll for event-driven architecture

### 5.5 Distribution

- Flathub (Flatpak) - Primary universal method
- Snap Store - Ubuntu ecosystem
- AppImage - Portable, no installation
- AUR (Arch User Repository) - Arch ecosystem
- COPR (Fedora) - Fedora/RHEL ecosystem
- PPA (Ubuntu) - Ubuntu-specific
- Nix packages - NixOS ecosystem
- Direct download (.deb, .rpm, tar.gz)

---

## 6. Cross-Platform Frameworks

### 6.1 Framework Comparison

| Framework | Platforms | Language | Performance | Binary Size |
|-----------|-----------|----------|-------------|-------------|
| Tauri 2.0 | Win, Mac, Linux, iOS, Android | Rust + Web | Excellent | 3-10 MB |
| Flutter | All platforms | Dart | Excellent | 15-30 MB |
| React Native | iOS, Android, (Web) | JavaScript | Good | 30-50 MB |
| Electron | Win, Mac, Linux | JavaScript | Fair | 80-200 MB |
| .NET MAUI | Win, Mac, iOS, Android | C# | Good | 30-60 MB |
| Kotlin Multiplatform | Android, iOS, Web, Desktop | Kotlin | Good | Varies |
| Compose Multiplatform | Android, iOS, Desktop, Web | Kotlin | Good | 20-40 MB |

### 6.2 Recommended: Tauri 2.0

Why Tauri for desktop + mobile:

- Tiny binary size (3-10MB vs 150MB+ Electron)
- Rust backend (memory-safe, fast)
- Web frontend (reuse React/Vue/Svelte skills)
- Native OS APIs via plugins
- Mobile support (iOS + Android) in v2
- Built-in updater
- Strong security model (allowlist-based API access)
- Active development, growing ecosystem

### 6.3 Recommended: Flutter

Why Flutter for mobile-first projects:

- Single codebase for iOS + Android
- Excellent performance (compiled to native ARM)
- Rich widget library (Material + Cupertino)
- Hot reload for fast development
- Desktop support (Windows, macOS, Linux)
- Web support (improving)
- Large package ecosystem (pub.dev)
- Google-backed, strong community

---

## 7. Shared Architecture Patterns

### 7.1 Core Logic Sharing

Strategies for sharing business logic across platforms:

1. Rust Core (Recommended)
   - Write core logic in Rust
   - Compile to native library per platform
   - Bindings: UniFFI (mobile), napi-rs (Node), C FFI (desktop)
   - Benefits: Memory safety, performance, single source of truth

2. Kotlin Multiplatform
   - Share Kotlin code across Android, iOS, Web, Desktop
   - Platform-specific implementations via expect/actual
   - Benefits: Single language, JetBrains-backed

3. WebAssembly (WASM)
   - Compile Rust/Go/C to WASM
   - Run in browser, Node.js, and WASM runtimes
   - Benefits: Universal binary, sandboxed execution

4. API-First (Backend sharing)
   - All logic server-side, clients are thin
   - OpenAPI spec generates client SDKs
   - Benefits: Single implementation, instant updates

### 7.2 Design Token Sharing

Maintain visual consistency across platforms:

- Define tokens in JSON/YAML (single source of truth)
- Generate platform-specific files:
  - CSS custom properties (Web)
  - XML resources (Android)
  - Swift asset catalog (iOS)
  - XAML resources (Windows)
  - GTK CSS (Linux)
- Automate generation in CI/CD pipeline
- Tools: Style Dictionary, Figma Tokens

### 7.3 API Contract Sharing

- Define API in OpenAPI 3.1 specification
- Generate TypeScript types (Web)
- Generate Kotlin data classes (Android)
- Generate Swift structs (iOS)
- Generate C# models (Windows)
- Generate Rust structs (Linux/Tauri)
- Validate all implementations against spec in CI

---

## 8. Platform-Specific Security

### 8.1 Mobile Security (Android + iOS)

- Certificate pinning for all API calls
- Biometric authentication (fingerprint, face)
- Hardware-backed keystore (Android Keystore, iOS Secure Enclave)
- App attestation (Play Integrity, DeviceCheck)
- Jailbreak/root detection
- Code obfuscation (ProGuard/R8, Swift obfuscation)
- Screenshot prevention for sensitive screens
- Clipboard clearing for sensitive data
- App switcher blur (hide content in recents)

### 8.2 Desktop Security (Windows + Linux)

- Code signing (Authenticode on Windows, GPG on Linux)
- Sandboxing (AppContainer, Flatpak sandbox, Firejail)
- Auto-update with signature verification
- Secure storage (DPAPI, libsecret, Keyring)
- Input validation for file operations
- ASLR, DEP/NX, stack canaries (compiler flags)
- Minimal permissions (request only what is needed)

### 8.3 Web Security (PWA)

- Content Security Policy (strict)
- Subresource Integrity (SRI) for CDN scripts
- Service Worker scope restriction
- CORS configuration (strict origins)
- Cookie security (HttpOnly, Secure, SameSite)
- Web Crypto API for client-side encryption
- Permissions Policy (restrict browser features)

---

## 9. Distribution and Updates

### 9.1 Auto-Update Strategy

| Platform | Mechanism |
|----------|-----------|
| Web (PWA) | Service Worker update (automatic) |
| Android | Play Store auto-update + In-App Updates API |
| iOS | App Store auto-update |
| Windows | Velopack / Squirrel / MSIX auto-update |
| Linux | Flatpak auto-update / AppImage Update |
| Tauri | Built-in updater (signed updates) |

### 9.2 Release Channels

Implement staged rollouts:

1. Internal (team testing)
2. Alpha/Beta (opt-in testers)
3. Canary (5 percent of users)
4. Stable (100 percent rollout)

### 9.3 Version Strategy

Use Semantic Versioning (SemVer): MAJOR.MINOR.PATCH

- MAJOR: Breaking changes
- MINOR: New features (backward compatible)
- PATCH: Bug fixes

---

## 10. Multi-Platform Checklist

### Architecture
- Core business logic separated from UI
- Platform adapters for OS-specific features
- Shared API contract (OpenAPI spec)
- Design tokens synchronized across platforms
- Consistent error handling strategy

### Web (PWA)
- Service Worker implemented and tested
- Web App Manifest complete (all icon sizes)
- Offline functionality working
- Push notifications configured
- Lighthouse score 95+
- All security headers present
- Responsive at all breakpoints

### Android
- Jetpack Compose UI implemented
- Certificate pinning active
- ProGuard/R8 enabled for release
- Biometric auth integrated
- Play Integrity check implemented
- Baseline Profile generated
- App Bundle (AAB) for distribution

### Windows
- WinUI 3 / Tauri UI implemented
- Code signing configured
- MSIX package created
- Auto-updater integrated
- Windows Hello support
- SmartScreen compatible

### Linux
- GTK4 / Qt6 / Tauri UI implemented
- Flatpak manifest created
- AppImage build configured
- .deb and .rpm packages generated
- Wayland compatible
- D-Bus integration working
- Desktop entry file (.desktop) created

### Cross-Platform
- Visual consistency verified across all platforms
- Keyboard shortcuts per platform convention
- File paths use OS-standard locations
- Notifications use native APIs
- Deep linking works on all platforms
- Accessibility tested per platform standards

---

## References

- Next.js: https://nextjs.org/
- Jetpack Compose: https://developer.android.com/jetpack/compose
- Tauri: https://tauri.app/
- Flutter: https://flutter.dev/
- GTK4: https://www.gtk.org/
- WinUI 3: https://learn.microsoft.com/en-us/windows/apps/winui/
- Flatpak: https://flatpak.org/
- web.dev: https://web.dev/

---

*Last Updated: August 2026*
*Version: 2.0.0*
*Author: Shoumik Bala Somu*
