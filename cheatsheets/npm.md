# npm

## Basic Commands

```bash
# Initialize a new project
npm init          # Interactive setup
npm init -y       # Default setup

# Install dependencies
npm install <package>         # Install latest version
npm install <package>@<ver>   # Install specific version
npm install                   # Install all dependencies from package.json

# Install as dev dependency
npm install <package> --save-dev

# Install globally
npm install -g <package>

# Uninstall package
npm uninstall <package>

# Update package
npm update <package>

# List installed packages
npm list
npm list --depth=0            # Top-level only

# Check outdated packages
npm outdated

# View package info
npm view <package>
```

---

## Package Scripts

```json
"scripts": {
  "start": "node app.js",
  "test": "jest",
  "build": "webpack --config webpack.config.js"
}
```

```bash
npm run <script>    # Run custom script (e.g. npm run build)
npm start           # Shortcut for "start" script
npm test            # Shortcut for "test" script
```

---

## Versioning

```bash
npm version patch      # Increase patch version (1.0.0 → 1.0.1)
npm version minor      # Increase minor version (1.0.0 → 1.1.0)
npm version major      # Increase major version (1.0.0 → 2.0.0)
```

---

## Dependency Types

- **dependencies**: Needed for production
- **devDependencies**: Needed for development only
- **peerDependencies**: Needed if your package expects host to use a specific version
- **optionalDependencies**: Not required, but used if available

---

## Package.json Quick Reference

```json
{
  "name": "project-name",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {},
  "keywords": [],
  "author": "",
  "license": "ISC",
  "dependencies": {},
  "devDependencies": {}
}
```

---

## Useful Commands

```bash
npm cache clean --force    # Clean npm cache
npm audit                  # Security audit
npm audit fix              # Fix vulnerabilities
npm ci                     # Clean install (from lockfile)
npm prune                  # Remove extraneous packages
npm rebuild                # Rebuild packages
```

---

## Publishing Packages

```bash
npm login                  # Log into npm registry
npm publish                # Publish your package
npm unpublish              # Remove your package
```

---

## Miscellaneous

```bash
npm help                   # Show npm help
npm config list            # Show npm config
npm config set <key> <val> # Set npm config
npm root                   # Show root path of node_modules
```

---

**Tip:** Use `npx <package>` to run a package without installing it globally.
