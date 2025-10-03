# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an Expo React Native application using:
- **Expo SDK ~54.0** with the new architecture enabled
- **React 19.1.0** and **React Native 0.81.4**
- **Expo Router ~6.0** for file-based navigation with typed routes
- **TypeScript** with strict mode enabled
- **React Compiler** experimental feature enabled

## Common Commands

### Development
- `npm install` - Install dependencies
- `npx expo start` - Start the development server
- `npm run android` - Start on Android emulator
- `npm run ios` - Start on iOS simulator
- `npm run web` - Start web version
- `npm run lint` - Run ESLint

### Project Reset
- `npm run reset-project` - Moves starter code to app-example/ and creates blank app/ directory

## Architecture

### Routing Structure
The app uses Expo Router's file-based routing with a tab-based navigation pattern:
- `app/_layout.tsx` - Root layout with ThemeProvider and Stack navigator
- `app/(tabs)/_layout.tsx` - Tab navigation layout with haptic feedback
- `app/(tabs)/index.tsx` - Home screen
- `app/(tabs)/explore.tsx` - Explore screen
- `app/modal.tsx` - Modal screen
- `unstable_settings.anchor` set to '(tabs)' for deep linking anchor

### Theming System
The app has a comprehensive theming system:
- **Theme definition**: `constants/theme.ts` exports `Colors` object with light/dark variants
- **Color hook**: `hooks/use-color-scheme.ts` (.web.ts variant exists) detects system color scheme
- **Theme color hook**: `hooks/use-theme-color.ts` provides theme-aware color selection
- **Themed components**: `components/themed-*.tsx` automatically adapt to light/dark mode
- ThemeProvider wraps the app at root level using @react-navigation/native themes

### Component Organization
- `components/` - Reusable components
  - `themed-*.tsx` - Components with automatic theme support (ThemedView, ThemedText)
  - `haptic-tab.tsx` - Custom tab button with haptic feedback
  - `parallax-scroll-view.tsx` - Scroll view with parallax effect
  - `ui/` - UI primitives (IconSymbol with iOS-specific variant, Collapsible)
- Path alias `@/*` maps to root directory for clean imports

### Platform-Specific Code
- Platform-specific files use `.ios.tsx`, `.web.ts` extensions
- `components/ui/icon-symbol.ios.tsx` - iOS-specific icon implementation
- `hooks/use-color-scheme.web.ts` - Web-specific color scheme detection
- `constants/theme.ts` uses Platform.select for platform-specific fonts

### Configuration
- **TypeScript**: Extends expo/tsconfig.base with strict mode, uses path alias `@/*`
- **ESLint**: Uses expo flat config, ignores dist/
- **Expo config**: Located in app.json with plugins for router and splash screen
- **React Compiler**: Enabled in experiments
- **Typed Routes**: Enabled in experiments for type-safe navigation
