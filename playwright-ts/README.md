# Playwright TypeScript Development Container

A complete development environment for browser automation and end-to-end testing with Playwright and TypeScript, managed with pnpm.

## 🎯 Purpose

This dev container is designed for:

- End-to-end testing across Chromium, Firefox, and WebKit
- Browser automation and web scraping scripts
- API testing and monitoring
- Headless and headed browser automation workflows

## 🛠️ Included Tools & Features

### Runtime & Package Manager

- **Node.js 22 LTS**: Latest Long-Term Support Node.js release
- **pnpm**: Fast, disk-efficient package manager (replaces npm)
- **TypeScript 5.x**: Statically typed JavaScript with strict mode
- **ts-node**: Run TypeScript files directly without a compile step

### Testing & Automation

- **Playwright**: Cross-browser automation supporting Chromium, Firefox, and WebKit
- **@playwright/test**: Playwright's built-in test runner with parallelism, retries, and HTML reports

### Code Quality

- **ESLint** + **@typescript-eslint**: TypeScript-aware linting
- **Prettier**: Opinionated code formatter
- **EditorConfig**: Consistent editor settings across machines

## 📦 VS Code Extensions

### Playwright
- **Playwright Test for VS Code**: Run, debug, and record tests from the editor sidebar; open the Trace Viewer directly in VS Code

### Code Quality
- **ESLint**: Real-time lint feedback with auto-fix on save
- **Prettier**: Format on save
- **Error Lens**: Display errors and warnings inline

### Productivity
- **Path IntelliSense**: Auto-complete file paths in imports
- **GitLens**: Advanced Git integration with blame and history
- **Todo Tree**: Surface TODO/FIXME comments across the project
- **Bookmarks**: Mark and navigate key locations in code
- **EditorConfig**: Apply `.editorconfig` rules automatically

## 🚀 Getting Started

### Prerequisites

- [Visual Studio Code](https://code.visualstudio.com/)
- [Docker Desktop](https://www.docker.com/products/docker-desktop)
- [Dev Containers extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Setup Instructions

1. **Clone or create your project**
   ```bash
   mkdir my-playwright-project
   cd my-playwright-project
   ```

2. **Add the dev container configuration**
   - Copy the `.devcontainer` folder to your project root
   - Copy `playwright.config.ts`, `.eslintrc.json`, `.prettierrc`, `.editorconfig`, `.npmrc`, and `package.json`

3. **Open in VS Code**
   ```bash
   code .
   ```

4. **Reopen in Container**
   - Press `F1` or `Ctrl+Shift+P` (Windows/Linux) / `Cmd+Shift+P` (Mac)
   - Select: `Dev Containers: Reopen in Container`
   - The container builds and `pnpm install && playwright install --with-deps` runs automatically

5. **Verify the setup**
   ```bash
   pnpm --version
   pnpm exec playwright --version
   ```

## 💻 Usage Examples

### Running Tests

```bash
# Run all tests (all browsers)
pnpm test

# Run tests in a specific browser
pnpm exec playwright test --project=chromium

# Run tests matching a pattern
pnpm exec playwright test auth

# Run in headed mode (visible browser window)
pnpm test:headed

# Open interactive UI mode
pnpm test:ui

# Debug a single test
pnpm test:debug tests/example.spec.ts
```

### Viewing Reports

```bash
# Open the HTML report after a test run
pnpm test:report
```

Port **9323** is forwarded so the report is accessible at `http://localhost:9323`.

### Recording Tests

Use the Playwright VS Code extension sidebar:
1. Click **Record new** to record a new test by interacting with a browser
2. Click **Pick locator** to inspect elements and copy selectors

Or from the terminal:
```bash
pnpm exec playwright codegen https://example.com
```

### Managing Dependencies with pnpm

```bash
# Install all dependencies
pnpm install

# Add a runtime dependency
pnpm add axios

# Add a dev dependency
pnpm add -D some-library

# Remove a dependency
pnpm remove some-library

# Update all dependencies
pnpm update
```

### Code Quality

```bash
# Lint
pnpm lint

# Lint and auto-fix
pnpm lint:fix

# Format
pnpm format

# Check formatting without writing
pnpm format:check

# Type-check without emitting
pnpm typecheck
```

## 🏗️ Project Structure

```
my-playwright-project/
├── .devcontainer/
│   ├── devcontainer.json
│   └── Dockerfile
├── src/
│   └── app.ts                  # Entry point for automation scripts
├── tests/
│   ├── example.spec.ts         # Playwright test files
│   └── api.spec.ts
├── .editorconfig
├── .eslintrc.json
├── .gitignore
├── .npmrc
├── .prettierrc
├── package.json
├── playwright.config.ts
└── tsconfig.json
```

### Example Test File

```typescript
// tests/example.spec.ts
import { test, expect } from '@playwright/test';

test('homepage has correct title', async ({ page }) => {
  await page.goto('https://example.com');
  await expect(page).toHaveTitle(/Example Domain/);
});

test('can click a link', async ({ page }) => {
  await page.goto('https://example.com');
  await page.getByRole('link', { name: 'More information...' }).click();
  await expect(page).toHaveURL(/iana\.org/);
});
```

### Example Automation Script

```typescript
// src/app.ts
import { chromium } from 'playwright';

async function main() {
  const browser = await chromium.launch();
  const page = await browser.newPage();

  await page.goto('https://example.com');
  const title = await page.title();
  console.log(`Page title: ${title}`);

  await browser.close();
}

main();
```

## ⚙️ Configuration

### Playwright Config (`playwright.config.ts`)

The default configuration runs tests against Chromium, Firefox, and WebKit. To target a single browser:

```typescript
projects: [
  {
    name: 'chromium',
    use: { ...devices['Desktop Chrome'] },
  },
],
```

To set a base URL for all tests:

```typescript
use: {
  baseURL: 'http://localhost:3000',
  trace: 'on-first-retry',
},
```

### pnpm Version

The `packageManager` field in `package.json` pins the pnpm version via Corepack. To update it:

```bash
# Check current version
pnpm --version

# Update the packageManager field to match
# "packageManager": "pnpm@<new-version>"
```

## 🐛 Troubleshooting

### Playwright extension not finding tests
- Ensure `playwright.config.ts` exists at the project root
- Check the Output panel → Playwright for errors
- Reload VS Code: `Ctrl+Shift+P` → `Developer: Reload Window`

### Browser launch fails
- Run `pnpm exec playwright install --with-deps` to reinstall browsers
- Check if system deps were installed: `pnpm exec playwright install-deps`

### pnpm command not found
- Verify pnpm is installed: `which pnpm`
- Rebuild the container: `Dev Containers: Rebuild Container`

### ESLint errors about project config
- Ensure `tsconfig.json` exists and `parserOptions.project` in `.eslintrc.json` points to it

### HTML report port not accessible
- Verify port 9323 is forwarded in VS Code's Ports panel
- Run `pnpm exec playwright show-report` and open the URL shown

## 📚 Additional Resources

- [Playwright Documentation](https://playwright.dev/)
- [Playwright VS Code Extension](https://playwright.dev/docs/getting-started-vscode)
- [pnpm Documentation](https://pnpm.io/)
- [TypeScript ESLint](https://typescript-eslint.io/)
- [Prettier](https://prettier.io/)

## 🤝 Contributing

Suggestions for additional tools or improvements are welcome! Consider adding:
- Allure report integration
- Visual regression testing (pixelmatch, Applitools)
- Accessibility testing (axe-playwright)
- API mocking (MSW)

## 📄 License

This dev container configuration is available under the MIT License.

---

**Happy Testing!** 🎭
