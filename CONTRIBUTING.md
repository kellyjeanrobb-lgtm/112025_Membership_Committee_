# Contributing to Membership Dashboard

Welcome! This guide will help you get started with developing and contributing to the Membership Dashboard.

## Table of Contents

- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Development Setup](#development-setup)
- [Making Changes](#making-changes)
- [Code Standards](#code-standards)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)

## Getting Started

### Prerequisites

This project is a single-page application that runs entirely in the browser. No build tools or package managers are required!

**Required:**
- A modern web browser (Chrome, Firefox, Safari, or Edge)
- A text editor (VS Code, Sublime Text, etc.)
- Basic knowledge of HTML, JavaScript, and React

**Optional but helpful:**
- Git for version control
- A local web server for testing (see [Development Setup](#development-setup))

### Quick Start

1. **Clone the repository:**
   ```bash
   git clone https://github.com/kellyjeanrobb-lgtm/112025_Membership_Committee_.git
   cd 112025_Membership_Committee_
   ```

2. **Open the dashboard:**
   - Option 1: Simply open `index.html` in your web browser
   - Option 2: Use a local web server (recommended)

## Project Structure

```
.
├── index.html          # Main application file (contains all code)
├── README.md           # Project overview and business context
└── CONTRIBUTING.md     # This file - developer guide
```

### Architecture Overview

The dashboard is a **single-file React application** with the following structure:

```
index.html
├── <head>
│   ├── Meta tags (SEO, Open Graph, accessibility)
│   ├── External dependencies (React, Recharts, Tailwind, Lucide)
│   └── Inline styles
├── <body>
│   ├── #root div (React mount point)
│   ├── Loading indicator
│   ├── Noscript fallback
│   └── <script type="text/babel">
│       ├── Library imports
│       ├── ErrorBoundary component
│       ├── MembershipDashboard component
│       │   ├── Data definitions
│       │   ├── State management
│       │   └── UI rendering
│       └── Application initialization
```

## Development Setup

### Method 1: Direct File Opening (Simplest)

1. Navigate to the project directory
2. Double-click `index.html` or right-click and open with your browser
3. **Note:** Some browsers may restrict certain features when opening files directly

### Method 2: Local Web Server (Recommended)

Using a local server ensures all features work correctly and mimics production behavior.

**Using Python (most systems have this pre-installed):**
```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

**Using Node.js (if installed):**
```bash
npx serve .
```

**Using VS Code:**
- Install the "Live Server" extension
- Right-click `index.html` and select "Open with Live Server"

**Using PHP (if installed):**
```bash
php -S localhost:8000
```

Then open your browser to: `http://localhost:8000`

### Browser Developer Tools

Use browser developer tools to debug and inspect the application:

- **Console:** View logs, errors, and warnings
- **Elements/Inspector:** Inspect DOM and styles
- **Network:** Monitor resource loading
- **React DevTools:** Install the React DevTools extension for enhanced debugging

## Making Changes

### Editing the Dashboard

All code is in `index.html`. Here's how to modify different aspects:

#### 1. Updating Data

Find the data definitions in the `MembershipDashboard` component (starting around line 200):

```javascript
const fluxData = [ /* ... */ ];
const pipelineData = [ /* ... */ ];
const financials = [ /* ... */ ];
```

**To update data:**
1. Locate the relevant data array
2. Modify values while maintaining the same structure
3. Save and refresh your browser

#### 2. Styling Changes

**Tailwind CSS Classes:**
Most styling uses Tailwind utility classes inline in JSX:
```jsx
<div className="bg-white p-6 rounded-xl shadow-lg">
```

**Custom Styles:**
Add custom CSS in the `<style>` block in the `<head>` section.

#### 3. Adding New Components

Add new React components within the `<script type="text/babel">` block:

```javascript
const NewComponent = () => {
    return (
        <div className="...">
            {/* Your component code */}
        </div>
    );
};
```

Then use it in the `MembershipDashboard` component.

#### 4. Modifying Layout

The dashboard uses a responsive grid layout. Find the main container structure and adjust:

```jsx
<div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
    {/* Add or modify sections here */}
</div>
```

### Testing Your Changes

1. **Save your file** after making changes
2. **Refresh your browser** (⌘+R on Mac, Ctrl+R on Windows/Linux)
3. **Check the browser console** for any errors
4. **Test responsive behavior** by resizing the browser window
5. **Test in multiple browsers** if making significant changes

## Code Standards

### JavaScript/React Style

- Use **const** for variables that don't change, **let** for those that do
- Use **arrow functions** for consistency: `const myFunc = () => { }`
- Use **template literals** for string interpolation: `` `${value}` ``
- Keep components **focused and readable**
- Add **comments** for complex logic

### Naming Conventions

- **Components:** PascalCase (e.g., `MembershipDashboard`)
- **Variables/Functions:** camelCase (e.g., `fluxData`, `handleClick`)
- **Constants:** UPPER_SNAKE_CASE for true constants (e.g., `MAX_ITEMS`)
- **CSS Classes:** Use Tailwind utilities; custom classes use kebab-case

### Code Organization

- Keep related code together
- Use section comments to delineate major blocks:
  ```javascript
  // --- SECTION NAME ---
  ```
- Maintain consistent indentation (4 spaces used in this project)
- Keep lines under 100 characters when reasonable

### Accessibility

- Include ARIA labels for interactive elements
- Ensure proper semantic HTML structure
- Maintain sufficient color contrast
- Test keyboard navigation
- Provide text alternatives for visual content

## Testing

### Manual Testing Checklist

Before committing changes, verify:

- [ ] Page loads without console errors
- [ ] All charts render correctly
- [ ] Data displays accurately
- [ ] Responsive layout works on mobile/tablet/desktop
- [ ] Loading indicator shows briefly
- [ ] Error boundary catches test errors (see Troubleshooting)
- [ ] No broken icons or missing resources
- [ ] Console shows no warnings or errors

### Browser Compatibility

Test in these browsers when making significant changes:

- ✅ Chrome/Edge (Chromium) - Latest version
- ✅ Firefox - Latest version
- ✅ Safari - Latest version (macOS/iOS)

### Accessibility Testing

1. **Keyboard Navigation:** Tab through the page - all interactive elements should be reachable
2. **Screen Reader:** Test with VoiceOver (Mac), NVDA (Windows), or JAWS
3. **Color Contrast:** Use browser DevTools or online contrast checkers
4. **Zoom:** Test at 200% browser zoom - content should remain readable

## Troubleshooting

### Common Issues

#### 1. Page Shows "Loading..." Forever

**Causes:**
- JavaScript error preventing React from rendering
- External library failed to load
- Browser blocking scripts

**Solutions:**
1. Open browser console (F12) and check for errors
2. Check network tab - ensure all scripts loaded (200 status)
3. Try hard refresh: Ctrl+Shift+R (Windows/Linux) or ⌘+Shift+R (Mac)
4. Disable browser extensions that might block scripts
5. Check that you're using a modern browser version

#### 2. Charts Don't Render

**Causes:**
- Recharts library didn't load
- Data structure mismatch
- Missing ResponsiveContainer

**Solutions:**
1. Verify Recharts loaded in Network tab
2. Check console for Recharts-related errors
3. Validate data structure matches component expectations
4. Ensure chart is wrapped in `<ResponsiveContainer>`

#### 3. Icons Don't Appear

**Causes:**
- Lucide React library didn't load
- Icon name typo
- Component destructuring error

**Solutions:**
1. Check that lucide-react loaded in Network tab
2. Verify icon names match Lucide documentation
3. Ensure `window.lucideReact` is defined before use

#### 4. Styles Look Wrong

**Causes:**
- Tailwind CSS didn't load
- Class name typos
- Browser cache showing old styles

**Solutions:**
1. Verify Tailwind loaded from CDN (check Network tab)
2. Hard refresh browser to clear cache
3. Check className spelling (it's `className`, not `class` in React)
4. Inspect element in DevTools to see applied styles

#### 5. Testing Error Boundary

To verify the error boundary works:

1. Temporarily add this line inside `MembershipDashboard`:
   ```javascript
   throw new Error('Test error for error boundary');
   ```
2. Refresh the page - you should see the error UI
3. Remove the line after testing

### Browser-Specific Issues

**Safari:**
- May have stricter CORS policies - use local server if issues arise
- Some ES6+ features may need polyfills for older versions

**Firefox:**
- Excellent standards compliance - few issues expected

**Chrome/Edge:**
- Generally most permissive and best DevTools

### Getting Help

If you encounter issues not covered here:

1. **Check the browser console** - most errors are logged here
2. **Search GitHub Issues** - your issue may already be reported
3. **Create a new issue** with:
   - Browser and version
   - Steps to reproduce
   - Console error messages
   - Screenshots if applicable

## Dependencies

This project uses CDN-hosted libraries (no npm install needed):

| Library | Version | Purpose |
|---------|---------|---------|
| React | 18 | UI framework |
| React DOM | 18 | React rendering |
| Babel Standalone | Latest | JSX transformation |
| Recharts | Latest | Data visualization |
| Lucide React | Latest | Icons |
| Tailwind CSS | Latest | Styling framework |

### Updating Dependencies

To update a library version, change the CDN URL in the `<head>` section:

```html
<!-- Example: Update React -->
<script crossorigin src="https://unpkg.com/react@18/umd/react.production.min.js"></script>
```

**Warning:** Version changes may introduce breaking changes. Test thoroughly after updating.

### Pinning Versions

For production stability, consider pinning specific versions:

```html
<!-- Instead of @latest -->
<script src="https://unpkg.com/lucide-react@0.294.0/dist/umd/lucide-react.min.js"></script>
```

## Deployment

This is a static site that can be deployed anywhere that serves HTML files:

- **GitHub Pages:** Automatically deploys from the repository
- **Netlify/Vercel:** Drag and drop the file
- **S3/Cloud Storage:** Upload and serve as static content
- **Any web server:** Just serve the index.html file

No build process required!

## Performance Considerations

- All libraries load from CDN (cached by browser)
- Single file minimizes HTTP requests
- React production builds used for performance
- Charts use virtualization for large datasets
- CSS is utility-based (Tailwind) for small footprint

## Security Considerations

- All external scripts loaded from trusted CDNs
- No server-side code or database connections
- No user authentication or data submission
- Client-side only - no sensitive data exposed
- All resources loaded over HTTPS

## Future Improvements

Ideas for future enhancements:

- [ ] Add data export functionality (CSV/PDF)
- [ ] Implement data filtering and date ranges
- [ ] Add print-friendly styles
- [ ] Create reusable chart components
- [ ] Add unit tests using Jest/React Testing Library
- [ ] Migrate to a build system for better performance
- [ ] Add real-time data updates
- [ ] Implement user preferences storage

## Questions?

Feel free to open an issue or reach out to the maintainers. Happy coding! 🚀
