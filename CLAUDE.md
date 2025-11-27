# CLAUDE.md - AI Assistant Guide for marsan572

## Repository Overview

This repository hosts a Swagger UI static site, likely deployed via GitHub Pages. Swagger UI is a framework for visualizing and interacting with API documentation in OpenAPI (formerly Swagger) format.

**Repository**: victoria1915/marsan572
**Primary Purpose**: Static hosting of Swagger UI for API documentation
**Deployment Target**: GitHub Pages (based on .gitignore configuration)

## Repository Structure

```
marsan572/
├── .git/                      # Git repository metadata
├── .gitignore                 # Git ignore rules (GitHub Pages/Jekyll focused)
├── index.html                 # Main entry point for Swagger UI
├── snapcraft.yaml             # Snap package configuration
└── swagger-ui-5.29.0.zip      # Swagger UI distribution archive
```

### Key Files

#### index.html
- **Location**: `/index.html`
- **Purpose**: Main HTML entry point for the Swagger UI application
- **Dependencies**: References external assets:
  - `swagger-ui.css` - Main stylesheet
  - `index.css` - Custom styles
  - `favicon-32x32.png` and `favicon-16x16.png` - Favicons
  - `swagger-ui-bundle.js` - Main Swagger UI JavaScript bundle
  - `swagger-ui-standalone-preset.js` - Standalone preset
  - `swagger-initializer.js` - Initialization script
- **Note**: These referenced files are likely contained in `swagger-ui-5.29.0.zip`

#### snapcraft.yaml
- **Location**: `/snapcraft.yaml`
- **Purpose**: Configuration for building a Snap package
- **Version**: master
- **Runtime**: Nodejs-based with http-server
- **Port**: 8080 (localhost only)
- **Daemon**: Simple daemon mode
- **Build Command**: `npm run build`

#### .gitignore
- **Location**: `/.gitignore`
- **Purpose**: Git ignore patterns for GitHub Pages deployment
- **Ignores**:
  - Jekyll build artifacts (`_site/`, `.sass-cache/`, `.jekyll-cache/`, `.jekyll-metadata`)
  - Bundler vendor directory
  - `Gemfile.lock` (as per GitHub Pages best practices)

#### swagger-ui-5.29.0.zip
- **Location**: `/swagger-ui-5.29.0.zip`
- **Purpose**: Swagger UI v5.29.0 distribution archive
- **Size**: ~1.7 MB
- **Contents**: Pre-built Swagger UI assets (HTML, CSS, JS)

## Development Workflows

### Current State
This is a **minimal deployment repository** with limited development activity. The commit history shows:
1. Initial commit
2. File uploads (swagger-ui archive, index.html, snapcraft.yaml)
3. CNAME management (create then delete)

### Common Tasks for AI Assistants

#### 1. Updating Swagger UI Version
```bash
# Download new Swagger UI release
wget https://github.com/swagger-api/swagger-ui/archive/vX.X.X.zip -O swagger-ui-X.X.X.zip

# Extract and verify contents
unzip swagger-ui-X.X.X.zip

# Update index.html references if asset paths changed

# Commit changes
git add swagger-ui-X.X.X.zip index.html
git commit -m "Update Swagger UI to version X.X.X"
git push
```

#### 2. Extracting Swagger UI Assets
The `swagger-ui-5.29.0.zip` likely needs to be extracted for the site to function:

```bash
# Extract to current directory (or dist/ subdirectory)
unzip swagger-ui-5.29.0.zip
```

**Note**: The extracted files should be committed if they're needed for GitHub Pages deployment.

#### 3. Customizing the Swagger UI
To customize the Swagger UI (e.g., changing the API specification URL):

1. Extract `swagger-ui-5.29.0.zip` if not already done
2. Locate and modify `swagger-initializer.js` to point to your OpenAPI spec:
```javascript
window.ui = SwaggerUIBundle({
  url: "https://your-api-domain.com/openapi.yaml", // Change this
  dom_id: '#swagger-ui',
  // ...other config
})
```
3. Commit the modified file

#### 4. Adding Custom Styling
Create or modify `index.css` to add custom styles:
```css
/* Example: Custom header color */
.swagger-ui .topbar {
  background-color: #your-color;
}
```

#### 5. Deploying to GitHub Pages

**Current Deployment Method**: Appears to be direct commit to main branch

To enable GitHub Pages:
```bash
# Ensure all assets are extracted and committed
git add .
git commit -m "Prepare for GitHub Pages deployment"
git push origin main
```

Then configure in GitHub repository settings:
- Settings → Pages
- Source: Deploy from branch (main)
- Folder: / (root)

## Git Workflow Conventions

### Branch Strategy
- **Main Branch**: Not specified in context, likely `main` or `master`
- **Feature Branches**: Use `claude/` prefix for AI-generated changes
- **Current Branch**: `claude/claude-md-mih9xb3kl1i9kjhi-01VNuLc4nzLkDg2DKGGSKLKD`

### Commit Message Guidelines
Based on the repository history, commits are simple and descriptive:
- Use imperative mood: "Add", "Update", "Delete", "Create"
- Be concise and clear
- Examples:
  - "Update Swagger UI to version 5.30.0"
  - "Add custom API specification"
  - "Delete CNAME"

### Push Protocol
Always use:
```bash
git push -u origin <branch-name>
```

Retry on network failures with exponential backoff (2s, 4s, 8s, 16s) up to 4 times.

## Key Conventions for AI Assistants

### File Operations
1. **Always read before modifying**: Never propose changes to files you haven't read
2. **Prefer editing over creating**: Only create new files when absolutely necessary
3. **No unnecessary improvements**: Don't add features, refactoring, or documentation unless requested

### Code Quality
1. **Security**: Ensure no XSS vulnerabilities when modifying HTML/JS
2. **Simplicity**: Keep solutions minimal and focused
3. **No over-engineering**: Don't add abstractions for one-time operations

### Documentation
1. **No unsolicited documentation**: Don't create README.md or other docs unless requested
2. **Code references**: Use `file:line` format (e.g., `index.html:7`)
3. **Concise responses**: Keep explanations brief and to-the-point

## Missing Elements & Recommendations

### Current Gaps
1. **No extracted Swagger UI assets**: The zip file needs to be extracted for the site to function
2. **No README.md**: Consider adding basic usage documentation
3. **No OpenAPI specification**: The Swagger UI needs an API spec to display
4. **No build process**: Currently just static files (which is fine for Swagger UI)
5. **Missing referenced assets**: Files like `swagger-ui.css`, `swagger-ui-bundle.js` are referenced but not in root

### Recommended Next Steps
1. **Extract Swagger UI**: Unzip `swagger-ui-5.29.0.zip` to make assets available
2. **Add API specification**: Either:
   - Create a local `openapi.yaml` or `swagger.json` file
   - Configure `swagger-initializer.js` to point to remote API spec
3. **Test deployment**: Verify GitHub Pages deployment works correctly
4. **Add README**: Basic documentation for users (only if requested)

## Environment Information

- **Platform**: Linux
- **Git**: Repository with remote at victoria1915/marsan572
- **Deployment**: Intended for GitHub Pages (based on .gitignore)
- **Snap Support**: Configured for Snapcraft packaging

## Quick Reference Commands

```bash
# Check repository status
git status

# View commit history
git log --oneline -10

# Extract Swagger UI
unzip swagger-ui-5.29.0.zip -d dist/

# Start local development server (if extracted)
cd dist/
python3 -m http.server 8080

# Commit and push changes
git add .
git commit -m "Descriptive message"
git push -u origin claude/<branch-name>
```

## Notes for AI Assistants

1. This is a **deployment repository**, not an active development project
2. Changes should be **minimal and purposeful**
3. The primary use case is **hosting Swagger UI for API documentation**
4. When making changes, ensure the **static site remains functional**
5. Consider whether files need to be **extracted from the zip archive** before use
6. All changes should be committed to the `claude/` prefixed branch before creating PRs

---

**Last Updated**: 2025-11-27
**Swagger UI Version**: 5.29.0
**Documentation Version**: 1.0
