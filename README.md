# React Icon Components Generator

A tool for transforming and optimizing SVG files into React components. Works seamlessly with both React and Next.js since it simply generates standard React components, avoiding any bundler-specific issues. You just pass your SVG files, and it generates ready-to-use, optimized React icon components—without needing complex configurations that depend on your bundler like Webpack, Turbopack, or Vite. This library is a preconfigured install-and-use solution that helps you avoid bundler issues effortlessly.

## 📦 Installation

```sh
npm install react-icon-components --save-dev
```

## 🚀 Usage

1. **Create a config file** in your project root:

   ```sh
   touch react-icon-components.json
   ```

2. **Define your settings** inside `react-icon-components.json`:

   ```json
   {
     "iconsPath": "icons",
     "outputDir": "src/ui-kit/icons",
     "jsxRuntime": "classic",
     "typescript": false,
     "useDefaultOptimization": true,
     "componentPrefix": "Icon"
   }
   ```

3. **Run the generator**:
   ```sh
   npx react-icon-components generate-icons
   ```

## ⚙️ Configuration Options

| Option                   | Type                        | Default              | Description                                                                                       |
| ------------------------ | --------------------------- | -------------------- | ------------------------------------------------------------------------------------------------- |
| `iconsPath`              | `string`                    | `"icons"`            | Path to the folder containing SVG files.                                                          |
| `outputDir`              | `string`                    | `"src/ui-kit/icons"` | Path where the generated React components will be saved.                                          |
| `jsxRuntime`             | `"classic"` / `"automatic"` | `"classic"`          | JSX runtime mode: `"classic"` requires `import React`, `"automatic"` removes the need for import. |
| `typescript`             | `boolean`                   | `false`              | If `true`, generates `.tsx` files instead of `.jsx`.                                              |
| `useDefaultOptimization` | `boolean`                   | `true`               | If `true`, applies pre-configured SVGO optimizations to SVG files.                                |
| `componentPrefix`        | `string`                    | `"Icon"`             | Prefix for component names (e.g., `"IconClose"`, `"IconArrow"`).                                  |

## 📌 Example

If you have **these SVG files** inside `icons/`:

```
icons/
 ├── close.svg
 ├── arrow.svg
```

And your `react-icon-components.json` looks like this:

```json
{
  "iconsPath": "icons",
  "outputDir": "src/ui-kit/icons",
  "jsxRuntime": "classic",
  "typescript": false,
  "useDefaultOptimization": true,
  "componentPrefix": "Icon"
}
```

Then **running the generator**:

```sh
npx react-icon-components generate-icons
```

Will generate:

```
src/ui-kit/icons/
 ├── IconClose.jsx
 ├── IconArrow.jsx
 ├── index.js
```

## 🛠 Example Generated Component (`IconClose.jsx`)

```jsx
import React from "react";

const IconClose = (props) => (
  <svg
    viewBox="0 0 24 24"
    fill="none"
    {...props}
    xmlns="http://www.w3.org/2000/svg"
  >
    <path
      d="M7 7L17 17M7 17L17 7"
      stroke="currentColor"
      strokeWidth={2.5}
      strokeLinecap="round"
      strokeLinejoin="round"
    />
  </svg>
);

export default IconClose;
```

## ❓ FAQ

### How do I generate TypeScript components?

Set `"typescript": true` in your `react-icon-components.json`:

```json
{
  "typescript": true
}
```

This will generate `.tsx` instead of `.jsx`.

### What if I have multi-color SVGs?

Multi-color SVGs **won't be changed**, but single-color SVGs **will automatically use `currentColor`** unless you disable it.

### How do I optimize SVGs differently?

Set "useDefaultOptimization": false and define "svgoConfig" (see [SVGO Plugin Documentation for details](https://svgo.dev/docs/plugins/)):

```json
{
  "useDefaultOptimization": false,
  "svgoConfig": {
    "plugins": [
      "removeDimensions",
      { "name": "convertColors", "params": { "currentColor": false } }
    ]
  }
}
```
