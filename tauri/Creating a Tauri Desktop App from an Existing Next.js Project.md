# Creating a Tauri Desktop App from an Existing Next.js Project

This document summarizes the steps to create a Tauri desktop application from an existing Next.js project.

## 1. Install Tauri CLI

```bash
npm install --save-dev @tauri-apps/cli
# or
yarn add --dev @tauri-apps/cli
# or
pnpm add -D @tauri-apps/cli
```

## 2. Initialize Tauri

Navigate to your Next.js project root and run:

```bash
npx tauri init
# or
yarn tauri init
# or
pnpm tauri init
```

Answer the prompts as follows:

* **App name:** Your desired app name.
* **Setup:** `Cargo.toml (Rust)`.
* **Web assets URL/folder:** `../.next`.
* **Dev server command:** `npm run dev` (or `yarn dev`, `pnpm dev`).
* **Build command:** `npm run build` (or `yarn build`, `pnpm build`).

## 3. Configure `tauri.conf.json`

Modify the `src-tauri/tauri.conf.json` file:

```json
{
  "build": {
    "beforeBuildCommand": "npm run build",
    "beforeDevCommand": "npm run dev",
    "devPath": "../.next",
    "distDir": "../.next"
  },
  "tauri": {
    // ... other configurations
    "windows": [
      {
        "url": "index.html",
      }
    ]
  }
}
```

* Set `build.beforeBuildCommand` and `build.beforeDevCommand` to your Next.js build and dev commands.
* Set `build.devPath` and `build.distDir` to `../.next`.
* Ensure `tauri.windows[0].url` is set to `"index.html"`.

## 4. (Optional) Update `tsconfig.json`

For TypeScript projects, exclude Tauri build directories:

```json
{
  "exclude": ["node_modules", ".next", "out", "src-tauri/target", "src-tauri/Cargo.lock"]
}
```

## 5. Run in Development

```bash
npm run tauri dev
# or
yarn tauri dev
# or
pnpm tauri dev
```

## 6. Build for Production

```bash
npm run tauri build
# or
yarn tauri build
# or
pnpm tauri build
```

## Key Considerations

* **Routing:** Client-side routing in Next.js should generally work. Server-side rendering (SSR) and API routes won't function directly.
* **Desktop Features:** Use `@tauri-apps/api` to access native desktop functionalities.
* **API Routes:** Consider rewriting backend logic in Rust or hosting API routes separately.
* **Rendering:** Static Site Generation (SSG) is generally better suited for desktop apps with Tauri.
* **Assets:** Ensure static assets are included in the `.next` build.
* **Security:** Use Tauri's allowlist to control access to desktop APIs.
