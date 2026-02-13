# VeriAction Design System

Shared design system for all VeriAction applications. Single source of truth for design tokens, UI components, and platform-specific themes.

## Architecture

```
veriaction-design-system/
├── tokens/                    # Platform-agnostic design tokens (JSON)
│   ├── colors.json            # Color palette + semantic colors
│   ├── typography.json        # Font families, sizes, weights
│   ├── spacing.json           # Spacing scale
│   ├── shadows.json           # Elevation system
│   └── platforms/             # Generated platform-specific outputs
│       ├── web/               # CSS custom properties
│       ├── ios/               # Swift Color extensions
│       └── android/           # Compose Color.kt
├── web/                       # npm package: @veriaction/ui
│   ├── src/components/ui/     # shadcn/ui components (54+)
│   ├── src/lib/               # Utilities (cn, etc.)
│   └── src/hooks/             # Custom React hooks
├── ios/                       # Swift Package: VeriActionUI
│   └── Sources/               # SwiftUI color tokens + components
├── android/                   # Gradle module: veriaction-ui
│   └── src/                   # Jetpack Compose theme + components
└── docs/                      # Storybook, architecture, guides
```

## Consuming This Package

### Web (React/Next.js)
```bash
pnpm add @veriaction/ui
```

### iOS (Swift Package Manager)
```swift
.package(url: "https://github.com/VeriAction/veriaction-design-system.git", from: "1.0.0")
```

### Android (Gradle)
```kotlin
implementation("com.veriaction:ui:1.0.0")
```

## Repository Relationships

### Brand Guidelines (Source of Truth)
- **Repo**: [Intenteon/brand_guidelines](https://github.com/Intenteon/brand_guidelines)
- **Local**: `/Users/stevenjob/gitrepos/intenteon-brand-guidelines/`
- **VeriAction tokens**: `brands/enterprise/veriaction/guidelines/`
- **Shared Intenteon tokens**: `_shared/design-tokens/tokens.json`

### Figma Output Repos (Visual Reference)
These contain Figma-exported React code. They are **reference implementations**, NOT production code.

| Figma Repo | Purpose | Implementation Repo |
|---|---|---|
| [Veriactionweb](https://github.com/VeriAction/Veriactionweb) | Dashboard + Admin UI reference | `veriaction-dashboard`, `veriaction-admin` |
| [Veriactionlanding](https://github.com/VeriAction/Veriactionlanding) | Landing/portal page reference | `veriaction-portal` |
| [Veriactionios](https://github.com/VeriAction/Veriactionios) | iOS app visual reference (web export) | Future native iOS app |
| [Veriactionandroid](https://github.com/VeriAction/Veriactionandroid) | Android app visual reference (web export) | Future native Android app |
| [Veriactionwearableapple](https://github.com/VeriAction/Veriactionwearableapple) | watchOS visual reference (web export) | Future native watchOS app |
| [Veriactionwearableos](https://github.com/VeriAction/Veriactionwearableos) | Wear OS visual reference (web export) | Future native Wear OS app |

### Implementation Repos (Production Code)
| Repo | Platform | Consumes |
|---|---|---|
| [veriaction-dashboard](https://github.com/VeriAction/veriaction-dashboard) | Web (Next.js) | `@veriaction/ui` (web) |
| [veriaction-admin](https://github.com/VeriAction/veriaction-admin) | Web (Next.js) | `@veriaction/ui` (web) |
| [veriaction-portal](https://github.com/VeriAction/veriaction-portal) | Web (Next.js) | `@veriaction/ui` (web) |
| Future iOS app | iOS (SwiftUI) | VeriActionUI (Swift Package) |
| Future Android app | Android (Compose) | veriaction-ui (Gradle) |

## Token Pipeline

```
Brand Guidelines (tokens.json)
        ↓
Design Tokens (this repo: tokens/)
        ↓ (Style Dictionary / build script)
   ┌────┼────────┐
   ↓    ↓        ↓
  CSS  Swift   Kotlin
  vars  ext    Compose
   ↓    ↓        ↓
  Web   iOS   Android
  apps  apps    apps
```

## Color System

### Core Palette
| Token | Value | Usage |
|---|---|---|
| `primary` | `#3B82F6` | Primary actions, links, focus rings |
| `primary-hover` | `#2563EB` | Hover state for primary elements |
| `primary-light` | `#60A5FA` | Dark mode primary |

### Decision Colors (VeriAction-specific)
| Token | Value | Usage |
|---|---|---|
| `allow` / `success` | `#10B981` | Allowed decisions, success states |
| `block` / `error` | `#EF4444` | Blocked decisions, error states |
| `challenge` / `warning` | `#F59E0B` | Challenge decisions, warning states |

### Background Surfaces (Dark Mode Primary)
| Token | Value | Usage |
|---|---|---|
| `bg-primary` | `#0A1628` | Page background |
| `bg-secondary` | `#1A2744` | Card/surface background |
| `bg-tertiary` | `#243352` | Elevated surfaces, popovers |

## Contributing

1. Token changes go in `tokens/*.json`
2. Run the build to regenerate platform outputs
3. Web component changes go in `web/src/components/ui/`
4. All changes must maintain cross-platform parity
