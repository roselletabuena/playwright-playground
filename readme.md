# Playwright Commands Reference

A comprehensive guide to the most useful Playwright commands for Node.js projects, organized by category for quick reference.

## Table of Contents
- [Installation & Setup](#installation--setup)
- [Test Execution](#test-execution)
- [Code Generation](#code-generation)
- [Debugging](#debugging)
- [Browser Management](#browser-management)
- [Configuration](#configuration)
- [Reporting](#reporting)
- [Screenshots & Videos](#screenshots--videos)
- [Mobile & Device Testing](#mobile--device-testing)
- [Advanced Features](#advanced-features)

---

## Installation & Setup

### Initial Installation
```bash
# Install Playwright
npm init playwright@latest

# Install Playwright with specific browsers
npm init playwright@latest -- --browser=chromium

# Add to existing project
npm install -D @playwright/test
npx playwright install
```

### Install Browsers
```bash
# Install all browsers
npx playwright install

# Install specific browser
npx playwright install chromium
npx playwright install firefox
npx playwright install webkit

# Install with dependencies (Linux)
npx playwright install-deps
```

---

## Test Execution

### Basic Test Running
```bash
# Run all tests
npx playwright test

# Run tests in specific file
npx playwright test tests/example.spec.js

# Run tests matching pattern
npx playwright test --grep "login"

# Run tests in headed mode (visible browser)
npx playwright test --headed

# Run tests in debug mode
npx playwright test --debug
```

### Browser-Specific Tests
```bash
# Run tests on specific browser
npx playwright test --project=chromium
npx playwright test --project=firefox
npx playwright test --project=webkit

# Run on multiple browsers
npx playwright test --project=chromium --project=firefox
```

### Parallel & Performance
```bash
# Run tests in parallel (specify workers)
npx playwright test --workers=4

# Run tests in serial (one at a time)
npx playwright test --workers=1

# Run with maximum workers
npx playwright test --workers=100%
```

---

## Code Generation

### Test Generation
```bash
# Generate tests by recording interactions
npx playwright codegen

# Generate tests for specific URL
npx playwright codegen https://example.com

# Generate tests with specific browser
npx playwright codegen --browser=firefox

# Generate tests with device emulation
npx playwright codegen --device="iPhone 12"

# Save generated test to file
npx playwright codegen --target=javascript -o tests/generated.spec.js
```

### Test Generation Options
```bash
# Generate with custom viewport
npx playwright codegen --viewport-size=1280,720

# Generate with authentication
npx playwright codegen --save-storage=auth.json

# Load existing authentication
npx playwright codegen --load-storage=auth.json
```

---

## Debugging

### Debug Commands
```bash
# Debug specific test
npx playwright test example.spec.js --debug

# Debug with Playwright Inspector
npx playwright test --debug --headed

# Debug from specific line
npx playwright test --debug --headed --grep "specific test"

# Show browser during test execution
npx playwright test --headed --slowMo=1000
```

### Trace & Inspector
```bash
# Show trace viewer
npx playwright show-trace trace.zip

# Show HTML report with traces
npx playwright show-report

# Open Playwright Inspector
npx playwright inspector
```

---

## Browser Management

### Browser Context
```bash
# List installed browsers
npx playwright list-browsers

# Check browser installation
npx playwright check

# Update browsers
npx playwright install --force

# Clean browser cache
npx playwright clear-cache
```

---

## Configuration

### Configuration Files
```bash
# Create configuration file
npx playwright init

# Run with specific config
npx playwright test --config=playwright.config.js

# Run with environment variables
PLAYWRIGHT_BROWSER=firefox npx playwright test
```

### Global Setup/Teardown
```bash
# Run global setup
npx playwright test --global-setup

# Run global teardown
npx playwright test --global-teardown
```

---

## Reporting

### Built-in Reports
```bash
# Generate HTML report
npx playwright test --reporter=html

# Generate JUnit XML report
npx playwright test --reporter=junit

# Generate JSON report
npx playwright test --reporter=json

# Multiple reporters
npx playwright test --reporter=html --reporter=junit
```

### Report Viewing
```bash
# Show HTML report
npx playwright show-report

# Show report from specific path
npx playwright show-report playwright-report/

# Generate and show report
npx playwright test --reporter=html && npx playwright show-report
```

---

## Screenshots & Videos

### Screenshot Commands
```bash
# Take screenshot during test
await page.screenshot({ path: 'screenshot.png' })

# Full page screenshot
await page.screenshot({ path: 'full-page.png', fullPage: true })

# Element screenshot
await element.screenshot({ path: 'element.png' })
```

### Video Recording
```bash
# Run tests with video recording
npx playwright test --video=on

# Record video only on failure
npx playwright test --video=retain-on-failure

# Record video with traces
npx playwright test --trace=on --video=on
```

---

## Mobile & Device Testing

### Device Emulation
```bash
# Test on mobile device
npx playwright codegen --device="iPhone 13"

# Test on tablet
npx playwright codegen --device="iPad Pro"

# List available devices
npx playwright list-devices
```

### Responsive Testing
```bash
# Test with custom viewport
npx playwright test --viewport=375x667

# Test multiple viewports
npx playwright test --project=mobile --project=desktop
```

---

## Advanced Features

### Authentication
```bash
# Save authentication state
npx playwright codegen --save-storage=state.json https://example.com

# Use saved authentication
npx playwright test --load-storage=state.json
```

### Performance Testing
```bash
# Enable performance tracing
npx playwright test --trace=on

# Network throttling
npx playwright test --network=slow3g
```

### API Testing
```bash
# Test API endpoints
npx playwright test api-tests/

# Run API tests only
npx playwright test --grep "@api"
```

---

## Useful Environment Variables

```bash
# Set browser
export PLAYWRIGHT_BROWSER=firefox

# Set headless mode
export PLAYWRIGHT_HEADLESS=false

# Set slow motion
export PLAYWRIGHT_SLOWMO=1000

# Set timeout
export PLAYWRIGHT_TIMEOUT=30000

# Enable debug logs
export DEBUG=pw:api
```

---

## Common Test Patterns

### Basic Test Structure
```javascript
// example.spec.js
import { test, expect } from '@playwright/test';

test('basic test', async ({ page }) => {
  await page.goto('https://example.com');
  await expect(page).toHaveTitle(/Example/);
});
```

### Page Object Model
```javascript
// pages/LoginPage.js
export class LoginPage {
  constructor(page) {
    this.page = page;
    this.usernameInput = page.locator('#username');
    this.passwordInput = page.locator('#password');
    this.loginButton = page.locator('#login');
  }

  async login(username, password) {
    await this.usernameInput.fill(username);
    await this.passwordInput.fill(password);
    await this.loginButton.click();
  }
}
```

---

## Tips & Best Practices

1. **Use meaningful test names**: Describe what the test does
2. **Leverage auto-waiting**: Playwright waits for elements automatically
3. **Use data-testid attributes**: More reliable than CSS selectors
4. **Run tests in CI/CD**: Integrate with GitHub Actions, Jenkins, etc.
5. **Use fixtures**: Share common setup across tests
6. **Enable tracing in CI**: Helps debug failed tests
7. **Use soft assertions**: Continue test execution after assertion failures

---

## Resources

- [Official Documentation](https://playwright.dev/)
- [API Reference](https://playwright.dev/docs/api/class-playwright)
- [Best Practices](https://playwright.dev/docs/best-practices)
- [GitHub Repository](https://github.com/microsoft/playwright)

---

*Happy Testing with Playwright! 🎭*