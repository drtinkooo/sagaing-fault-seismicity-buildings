# Contributing to Sagaing Fault Seismicity & Building Exposure Map

Thank you for your interest in contributing to this project! This document provides guidelines for contributing.

## Table of Contents

1. [Code of Conduct](#code-of-conduct)
2. [How Can I Contribute?](#how-can-i-contribute)
3. [Development Setup](#development-setup)
4. [Pull Request Process](#pull-request-process)
5. [Style Guidelines](#style-guidelines)
6. [Reporting Bugs](#reporting-bugs)
7. [Suggesting Features](#suggesting-features)

---

## Code of Conduct

This project is dedicated to providing a welcoming environment for everyone. Please be respectful and constructive in all interactions.

### Our Standards

- Use welcoming and inclusive language
- Be respectful of differing viewpoints
- Accept constructive criticism gracefully
- Focus on what is best for the community
- Show empathy towards other community members

---

## How Can I Contribute?

### Types of Contributions

1. **Bug Reports**: Found something that doesn't work? Let us know!
2. **Feature Requests**: Have an idea for improvement? We'd love to hear it!
3. **Code Contributions**: Fix bugs, add features, or improve documentation
4. **Data Updates**: Help keep earthquake data current
5. **Translations**: Help translate the interface to other languages
6. **Documentation**: Improve or expand existing documentation

### Good First Issues

Look for issues labeled `good first issue` - these are great starting points for new contributors:

- Documentation improvements
- UI text corrections
- Minor bug fixes
- Code comments and cleanup

---

## Development Setup

### Prerequisites

- Modern web browser (Chrome, Firefox, Safari, Edge)
- Text editor or IDE
- Git
- (Optional) Python 3.x for local server
- (Optional) Node.js for advanced development

### Getting Started

```bash
# 1. Fork the repository on GitHub

# 2. Clone your fork
git clone https://github.com/YOUR-USERNAME/sagaing-fault-seismicity-buildings.git
cd sagaing-fault-seismicity-buildings

# 3. Add upstream remote
git remote add upstream https://github.com/drtinkooo/sagaing-fault-seismicity-buildings.git

# 4. Create a feature branch
git checkout -b feature/your-feature-name

# 5. Start a local server (optional but recommended)
python -m http.server 8000
# Visit http://localhost:8000

# 6. Make your changes
# Edit index.html or other files

# 7. Test your changes in multiple browsers

# 8. Commit your changes
git add .
git commit -m "Add: Brief description of changes"

# 9. Push to your fork
git push origin feature/your-feature-name

# 10. Create a Pull Request on GitHub
```

### Project Structure

```
sagaing-fault-seismicity-buildings/
├── index.html          # Main application file
├── README.md           # Project documentation
├── LICENSE             # License file
├── CITATION.cff        # Citation metadata
├── CONTRIBUTING.md     # This file
├── preview.png         # Map preview image
└── docs/
    ├── DATA.md         # Data documentation
    └── CHANGELOG.md    # Version history
```

---

## Pull Request Process

### Before Submitting

1. **Update from upstream**: Ensure your branch is up-to-date
   ```bash
   git fetch upstream
   git rebase upstream/main
   ```

2. **Test thoroughly**: Check your changes work in multiple browsers

3. **Follow style guidelines**: See [Style Guidelines](#style-guidelines)

4. **Update documentation**: If your changes require it

### PR Checklist

- [ ] Code follows the project's style guidelines
- [ ] Changes have been tested in Chrome, Firefox, and Safari
- [ ] Documentation has been updated (if applicable)
- [ ] Commit messages are clear and descriptive
- [ ] PR title and description clearly explain the changes

### PR Title Format

Use these prefixes:
- `Add:` New features
- `Fix:` Bug fixes
- `Update:` Updates to existing features
- `Docs:` Documentation changes
- `Style:` Code style/formatting changes
- `Refactor:` Code refactoring

Examples:
- `Add: Time-lapse animation for earthquake sequence`
- `Fix: Building layer not loading on mobile devices`
- `Docs: Improve data source documentation`

### Review Process

1. Submit your PR
2. Maintainers will review within 1-2 weeks
3. Address any requested changes
4. Once approved, your PR will be merged

---

## Style Guidelines

### HTML/CSS

```html
<!-- Use semantic HTML5 elements -->
<header>, <main>, <section>, <article>, <footer>

<!-- CSS class naming: kebab-case -->
<div class="layer-control-panel">

<!-- Indent with 4 spaces -->
<div class="container">
    <div class="content">
        ...
    </div>
</div>
```

### JavaScript

```javascript
// Use camelCase for variables and functions
const earthquakeLayer = L.geoJSON(...);
function formatDate(timestamp) { ... }

// Use const for constants, let for variables
const API_URL = 'https://...';
let currentZoom = map.getZoom();

// Use arrow functions for callbacks
map.on('click', (e) => {
    console.log(e.latlng);
});

// Add comments for complex logic
// Calculate magnitude-based marker radius
// Larger earthquakes get bigger markers
function getMarkerRadius(magnitude) {
    ...
}
```

### Commit Messages

```
# Format
<type>: <subject>

<body>

# Examples
Add: Magnitude filter slider

- Added range input for filtering earthquakes
- Updates display count in real-time
- Preserves filter state on layer toggle

Fix: Popup not closing on mobile tap

The popup was not closing when tapping outside
on mobile devices. Fixed by adding touchend
event listener.
```

---

## Reporting Bugs

### Before Submitting

1. **Check existing issues**: Someone may have already reported it
2. **Test in multiple browsers**: Is it browser-specific?
3. **Clear cache**: Try hard refresh (Ctrl+Shift+R)

### Bug Report Template

```markdown
## Bug Description
A clear description of what the bug is.

## Steps to Reproduce
1. Go to '...'
2. Click on '...'
3. Scroll down to '...'
4. See error

## Expected Behavior
What you expected to happen.

## Actual Behavior
What actually happened.

## Screenshots
If applicable, add screenshots.

## Environment
- Browser: [e.g., Chrome 120]
- OS: [e.g., Windows 11]
- Device: [e.g., Desktop/Mobile]

## Additional Context
Any other relevant information.
```

---

## Suggesting Features

### Feature Request Template

```markdown
## Feature Description
A clear description of the feature you'd like.

## Use Case
Why would this feature be useful? Who would benefit?

## Proposed Solution
How do you envision this working?

## Alternatives Considered
Other solutions you've thought about.

## Additional Context
Mockups, examples from other projects, etc.
```

### Feature Ideas We're Interested In

- 🎬 Time-lapse animation of earthquake sequence
- 🌏 Multi-language support (Myanmar, Thai, Chinese)
- 📊 Statistical analysis tools
- 📱 Progressive Web App (PWA) support
- 🖨️ Print/export functionality
- 🔔 Real-time earthquake alerts

---

## Questions?

Feel free to:
- Open an issue with the `question` label
- Contact the maintainer: [@drtinkooo](https://github.com/drtinkooo)

---

Thank you for contributing! 🙏
