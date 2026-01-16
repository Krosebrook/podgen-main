# 🚀 Vite Build & Optimization

This document details the Vite configuration and optimization strategies used in NanoGen Studio.

---

## Table of Contents

1. [Vite Configuration](#vite-configuration)
   - [`vite.config.ts`](#viteconfigts)
   - [TypeScript Integration](#typescript-integration)
   - [Environment Variables](#environment-variables)
2. [Build Optimization](#build-optimization)
   - [Code Splitting](#code-splitting)
   - [Tree Shaking](#tree-shaking)
   - [Minification](#minification)
   - [Production Build](#production-build)
3. [Development Server](#development-server)
   - [Hot Module Replacement (HMR)](#hot-module-replacement-hmr)
   - [Proxying](#proxying)
4. [Performance Analysis](#performance-analysis)
   - [Bundle Analysis](#bundle-analysis)
   - [Sourcemaps](#sourcemaps)

---

## Vite Configuration

Our Vite setup is configured in `vite.config.ts` for both development and production environments.

### `vite.config.ts`

Key settings include:

- **Plugins**: We use `@vitejs/plugin-react` for React support.
- **Resolve Alias**: Path aliases like `@/` are configured for cleaner imports.
- **Build Target**: We target modern browsers that support ES modules.

### TypeScript Integration

Vite handles TypeScript compilation out of the box. Our `tsconfig.json` is configured with `"isolatedModules": true` as required by Vite's esbuild-based transpilation.

### Environment Variables

We use `.env` files for environment-specific variables. Only variables prefixed with `VITE_` are exposed to the client-side code.

---

## Build Optimization

### Code Splitting

Vite automatically performs code splitting based on dynamic imports. We leverage this in `App.tsx`:

```typescript
const ImageEditor = React.lazy(() => import('./features/editor/components/ImageEditor'));
```

This creates separate chunks for our heavy components, which are only loaded when needed.

### Tree Shaking

Vite uses esbuild for tree shaking, which automatically removes unused code. To ensure this is effective, we:

- Use ES modules (`import`/`export`).
- Avoid side effects in modules where possible.

### Minification

For production builds, Vite uses Terser to minify the JavaScript output, significantly reducing bundle size.

### Production Build

Running `npm run build` triggers the production build, which includes all the optimizations mentioned above.

---

## Development Server

### Hot Module Replacement (HMR)

Vite's HMR provides near-instant feedback during development without requiring a full page reload.

### Proxying

We can configure a proxy in `vite.config.ts` to avoid CORS issues when making API requests to a separate backend server during development.

---

## Performance Analysis

### Bundle Analysis

We will use `rollup-plugin-visualizer` to generate a visual representation of our bundle, helping us identify large or unnecessary dependencies.

### Sourcemaps

Sourcemaps are enabled for production builds (`sourcemap: true`), allowing us to debug issues in production by mapping the minified code back to the original source.

---

**Last Updated**: 2026-01-08
