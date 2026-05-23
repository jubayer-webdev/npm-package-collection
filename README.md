What is npm?

npm (Node Package Manager) is a package manager for JavaScript that allows developers to share and reuse code. It hosts thousands of packages, which are pieces of reusable code, that you can easily integrate into your projects to extend functionality.
You can access it at [npmjs.com](https://www.npmjs.com/).

---

## 📚 Table of Contents

1. [📄 Documents](#-documents)
2. [📦 Packages List](#-packages-list)
3. [🌀 Create Your First Vite Project](#-create-your-first-vite-project)
4. [⚙️ Setup Prettier for React / Next.js](#%EF%B8%8F-setup-prettier-for-react--nextjs)
5. [⚠️ Tailwind Class Sorting Not Working?](#%EF%B8%8F-tailwind-class-sorting-not-working)
6. [🟦 Show TypeScript red squiggles in the editor](#-show-typescript-red-squiggles-in-the-editor)

---

## 📄 Documents

- [axios](https://axios.rest/)

### Prettier

- [prettier install](https://prettier.io/docs/install)
- [prettier options](https://prettier.io/docs/options)

### Tailwind CSS

- [Tailwind CSS Installation Using-Vite](https://tailwindcss.com/docs/installation/using-vite)
- [Automatic Class Sorting with Prettier](https://tailwindcss.com/blog/automatic-class-sorting-with-prettier)

---

## 📦 Packages List

- [axios](https://www.npmjs.com/package/axios)

---

- [prettier-plugin-tailwindcss](https://www.npmjs.com/package/prettier-plugin-tailwindcss)
- [eslint-config-prettier](https://www.npmjs.com/package/eslint-config-prettier) `npm install --save-dev eslint-config-prettier`

- [prettier-plugin-organize-imports](https://www.npmjs.com/package/prettier-plugin-organize-imports)`npm install --save-dev prettier-plugin-organize-imports`

---

- [use-debounce](https://www.npmjs.com/package/use-debounce?activeTab=readme)
- [react-intersection-observer](https://www.npmjs.com/package/react-intersection-observer)

---

- [react-feather](https://github.com/feathericons/react-feather) `Reference: lws 5.6 React Lazy Load explained`
- [remarkable](https://www.npmjs.com/package/remarkable) Reference: [Lazy-loading components with Suspense](https://react.dev/reference/react/lazy#suspense-for-code-splitting)

---

- Reference: [Internationalization (nextjs)](https://nextjs.org/docs/app/guides/internationalization#routing-overview)
    - [@formatjs/intl-localematcher](https://www.npmjs.com/package/@formatjs/intl-localematcher)
    - [negotiator](https://www.npmjs.com/package/negotiator)

---

## 🌀 Create Your First Vite Project

- [npm create vite@latest](https://vite.dev/guide/#scaffolding-your-first-vite-project)

---

## ⚙️ Setup Prettier for React / Next.js

Prettier is a code formatter. It keeps files such as JavaScript, TypeScript, JSX, TSX, CSS, JSON, and Markdown consistently formatted.

The `prettier` npm package you installed only works from the terminal (e.g., `npx prettier --write .`). It does **not** make the editor format on save by itself. For that, you need two things:

1.  Install the Prettier extension in Cursor/VS Code
2.  Enable "Format on Save"

To set up Prettier so that it automatically formats your code every time you save, you need to configure both your project and your editor.

### 🛠️ Step 1: Install the Prettier Extension in your Editor

For your editor to know how to format on save, it needs the Prettier extension.

1. Open the Extensions panel (`Ctrl+Shift+X` or `Cmd+Shift+X`).
2. Search for **Prettier - Code formatter** (by Esben Petersen) and install it.

### 📦 Step 2: Install Prettier in your Project

It's best practice to install Prettier locally in your project so everyone working on it uses the same version. Run this in your terminal:

```bash
npm install --save-dev prettier
```

If your project uses **Tailwind CSS**, also install the official Tailwind Prettier plugin so class names get sorted automatically:

```bash
npm install --save-dev prettier-plugin-tailwindcss
```

### ✨ Step 3: Create a `.prettierrc` Config File

Create a file named [.prettierrc](https://gist.github.com/jubayer-webdev/5786179582e20cb04dd08cc544410612) in the root of your project. This tells Prettier what rules to follow.

Recommended config for React / Next.js:

create the file from the terminal (Git Bash / macOS / Linux):

```bash
node --eval "fs.writeFileSync('.prettierrc','{}\n')"
```

then set the rules

```json
{
    "printWidth": 120,
    "useTabs": false,
    "tabWidth": 4,
    "trailingComma": "es5",
    "semi": true,
    "singleQuote": false,
    "bracketSpacing": true,
    "arrowParens": "always",
    "jsxSingleQuote": false,
    "bracketSameLine": false,
    "endOfLine": "lf",
    "singleAttributePerLine": true
}
```

If you installed `prettier-plugin-tailwindcss`, add it to the same file:

```json
{
    "plugins": ["prettier-plugin-tailwindcss"]
}
```

### 💻 Step 4: Configure the Editor to "Format on Save"

You need to tell Cursor/VS Code to use Prettier as the default formatter and to trigger it when you save.

#### Option A: Project-specific settings (Recommended)

This ensures anyone who opens this project gets the same format-on-save behavior.

1. Create a folder named `.vscode` in your project root.
2. Inside it, create a file named `settings.json`.
3. Add the following configuration:

`.vscode/settings.json`

```json
{
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
}
```

Or create the same file from the terminal:

```bash
mkdir -p .vscode && printf '{\n    "editor.defaultFormatter": "esbenp.prettier-vscode",\n    "editor.formatOnSave": true\n}\n' > .vscode/settings.json
```

#### Option B: Global settings

If you want this to apply to **all** projects you open on your computer:

1. Open Settings (`Ctrl+,` or `Cmd+,`).
2. Search for **"Format On Save"** and check the box.
3. Search for **"Default Formatter"** and select **Prettier - Code formatter** from the dropdown.

#### 🤝 What to push vs ignore from `.vscode`

The `.vscode` folder can contain both personal preferences and shared workspace settings. You want to **share only the workspace settings** with your team.

Add this to your `.gitignore`:

```text
.vscode/*
!.vscode/settings.json
!.vscode/extensions.json
```

What this does:

- Push `.vscode/settings.json` — shared editor settings (default formatter, format-on-save)
- Push `.vscode/extensions.json` — recommended extensions for the team
- Ignore everything else inside `.vscode/` — personal/local-only preferences

This way, the whole team gets the same Prettier setup and consistent formatting automatically.

### 🚫 Step 5: (Optional) Add a `.prettierignore` file

You usually don't want Prettier to format build outputs or package folders. Create a `.prettierignore` file in your project root:

```text
node_modules
dist
build
.next
coverage
```

Use `dist` for Vite/React build output and `.next` for Next.js build output.

### 📜 Step 6: (Optional) Add a format script

Update your `package.json` to include a format script:

```json
{
    "scripts": {
        "format": "prettier --write .",
        "format:check": "prettier --check ."
    }
}
```

`npm run format` updates files. `npm run format:check` only checks whether files are already formatted.

You can also run Prettier on a single file directly with `npx`:

```bash
npx prettier path/to/file --check
npx prettier path/to/file --write
```

See the [Prettier CLI docs](https://prettier.io/docs/cli) for more options.

Running `npm run format` will:

- Scan your entire project
- Find all supported files (`.js`, `.ts`, `.jsx`, `.tsx`, `.json`, `.css`, `.md`, etc.)
- Format them automatically based on your `.prettierrc`
- Save the changes directly

### 🧹 Step 7: (Optional) Use Prettier with ESLint

If the project uses ESLint, install `eslint-config-prettier`:

```bash
npm install --save-dev eslint-config-prettier
```

`eslint-config-prettier` turns off ESLint formatting rules that conflict with Prettier, so ESLint handles **code quality** and Prettier handles **formatting**.

It must be the **last** config in the array so it can override formatting rules from earlier configs.

#### ⚛️ For React / Vite projects

Open `eslint.config.js` and add `eslint-config-prettier` at the end:

```js
import eslintConfigPrettier from "eslint-config-prettier";

export default [
    // other ESLint configs first
    eslintConfigPrettier,
];
```

#### ▲ For Next.js projects (15.5+ / 16)

Open `eslint.config.mjs` and add `eslint-config-prettier` after the Next.js configs:

```js
import { defineConfig, globalIgnores } from "eslint/config";
import nextVitals from "eslint-config-next/core-web-vitals";
import nextTs from "eslint-config-next/typescript";
import eslintConfigPrettier from "eslint-config-prettier";

const eslintConfig = defineConfig([
    ...nextVitals,
    ...nextTs,
    eslintConfigPrettier,
    // Override default ignores of eslint-config-next.
    globalIgnores([
        // Default ignores of eslint-config-next:
        ".next/**",
        "out/**",
        "build/**",
        "next-env.d.ts",
    ]),
]);

export default eslintConfig;
```

> ⚠️ On older Next.js versions (below 15.5) the `eslint-config-next/core-web-vitals` and `eslint-config-next/typescript` subpaths do not exist. Use the `FlatCompat` approach instead.

---

### 📊 Prettier Setup Summary

| Piece                       | What it does                            |
| --------------------------- | --------------------------------------- |
| `prettier` npm package      | Lets you run Prettier from the terminal |
| `.prettierrc`               | Defines your formatting rules           |
| Prettier VS Code extension  | Runs Prettier inside the editor         |
| `editor.formatOnSave: true` | Automatically formats files on save     |

> ⚠️ **Note:** All four pieces must be configured for format-on-save to work properly.

> 💡 **Recommended workflow:** run `npm run format` first, then `npm run lint`. Prettier formats the code first, and ESLint checks for possible code problems after that.

### 🧠 How it works

When you press `Ctrl + S` (or `Cmd + S`):

1. ⌨️ VS Code triggers the formatter
2. 🪄 Prettier formats the file
3. ✅ File auto-updates instantly

---

## ⚠️ Tailwind Class Sorting Not Working?

If Tailwind classes are not being sorted automatically, the problem is usually the order of your Prettier plugins in `.prettierrc` file.

`prettier-plugin-tailwindcss` must be **last** in the `plugins` array.

```json
{
    ....,

    // ❌ Wrong
    "plugins": ["prettier-plugin-tailwindcss", "prettier-plugin-organize-imports"],
}
```

```json
{
    ....,

    // ✅ Correct
    "plugins": ["prettier-plugin-organize-imports", "prettier-plugin-tailwindcss"],
}
```

Why? Tailwind sorts classes during the final formatting step. If another Prettier plugin runs after it, Tailwind's output gets overridden.

---

## 🟦 Show TypeScript red squiggles in the editor

If TypeScript errors are not showing as red squiggles in Cursor/VS Code, make sure the built-in TypeScript validation is enabled. These squiggles come from the TypeScript language service, not ESLint.

To enable it from Settings:

1. Open Settings: `Ctrl + ,`
2. Search for `typescript validate`
3. Enable `TypeScript > Validate: Enable`

![TypeScript validate setting](./images/typescript-validate.png)

In `settings.json`, this setting should be missing or set to `true`:

```json
{
    "typescript.validate.enable": true
}
```

If you also want JavaScript files to show validation errors, enable this too:

```json
{
    "javascript.validate.enable": true
}
```

After changing the setting, restart the TypeScript server:

```bash
Ctrl + Shift + P → TypeScript: Restart TS Server
```

Then reopen the file or editor if needed. Type errors should now show as red squiggles in the editor.

Remember: ESLint and TypeScript validation are different. ESLint checks linting rules, while TypeScript validation checks type errors.

### 🧩 TypeScript: Restart TS Server Command Is Missing or Don't find `typescript validate` in settings

If the `TypeScript: Restart TS Server` command does not appear, the built-in TypeScript extension may be disabled.

To fix it:

1. Open the Extensions view (`Ctrl+Shift+X`).
2. Search for `@builtin typescript`.
3. Find **TypeScript and JavaScript Language Features**.
4. If it is disabled, click **Enable**.
5. If it is already enabled, disable it and enable it again to reset the extension.
