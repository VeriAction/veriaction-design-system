# CLAUDE.md - VeriAction Design System

## Repository Purpose

Shared design system for ALL VeriAction applications. Single source of truth for:
- **Design tokens** (colors, typography, spacing) in `tokens/`
- **Web components** (React/shadcn/ui) in `web/`
- **iOS tokens** (SwiftUI Color extensions) in `ios/`
- **Android tokens** (Jetpack Compose theme) in `android/`

## Key Rules

1. **Tokens are the source of truth** - All color/spacing/typography values come from `tokens/*.json`
2. **Platform parity** - Every token must exist in web, iOS, AND Android outputs
3. **Brand compliance** - All tokens must align with `Intenteon/brand_guidelines`
4. **No app-specific code** - This repo contains ONLY shared components and tokens

## Repository Relationships

### Brand Guidelines (Upstream)
- **Repo**: [Intenteon/brand_guidelines](https://github.com/Intenteon/brand_guidelines)
- **Local**: `/Users/stevenjob/gitrepos/intenteon-brand-guidelines/`
- **VeriAction tokens**: `brands/enterprise/veriaction/guidelines/`
- **Shared Intenteon tokens**: `_shared/design-tokens/tokens.json`

### Consumers (Downstream)
| Repo | Consumes | Package |
|---|---|---|
| `veriaction-dashboard` | Web components | `@veriaction/ui` |
| `veriaction-admin` | Web components | `@veriaction/ui` |
| `veriaction-portal` | Web components | `@veriaction/ui` |
| Future iOS app | iOS tokens | VeriActionUI (Swift Package) |
| Future Android app | Android tokens | veriaction-ui (Gradle) |

### Figma Reference (Read-Only)
These repos contain Figma-exported React code for visual reference:
- `Veriactionweb` - Dashboard/admin screens
- `Veriactionlanding` - Landing page
- `Veriactionios`, `Veriactionandroid` - Mobile screen reference (web code, NOT native)

### Architecture Doc
See: [veriaction-dashboard/docs/REPOSITORY-ARCHITECTURE.md](https://github.com/VeriAction/veriaction-dashboard/blob/main/docs/REPOSITORY-ARCHITECTURE.md)

## Directory Structure

```
tokens/                    # Platform-agnostic design tokens (W3C format)
├── colors.json            # Color palette + semantic colors
├── typography.json        # Font families, sizes, weights
├── spacing.json           # Spacing, border-radius, shadows
└── platforms/             # Generated platform outputs
    ├── web/               # CSS custom properties
    ├── ios/               # Swift Color extensions
    └── android/           # Compose Color.kt

web/                       # npm: @veriaction/ui
├── src/components/ui/     # shadcn/ui components (54+)
├── src/lib/utils.ts       # cn() utility
└── src/hooks/             # Custom React hooks

ios/Sources/               # Swift Package: VeriActionUI
android/src/               # Gradle module: veriaction-ui
docs/                      # Architecture docs, Storybook
```

## Tech Stack

- **Token Format**: W3C Design Tokens (JSON)
- **Web Components**: React 18+, shadcn/ui, Radix UI, TailwindCSS 4
- **iOS**: SwiftUI, Swift 5.9+
- **Android**: Jetpack Compose, Kotlin 1.9+

## VeriAction Color System

### Decision Colors (Core Differentiator)
| Token | Hex | Usage |
|---|---|---|
| `allow` | `#10B981` | ALLOW decisions, success |
| `block` | `#EF4444` | BLOCK decisions, errors |
| `challenge` | `#F59E0B` | CHALLENGE decisions, warnings |

### Badge Pattern
Decision badges use: 10% bg opacity + colored text + 20% border opacity
```css
.badge-allow { background: rgba(16,185,129,0.1); color: #10B981; border-color: rgba(16,185,129,0.2); }
```
