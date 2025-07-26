# yarn

## Initialization

```bash
yarn init                # Interactive package.json setup
yarn init -y             # Default setup
```

---

## Installing Packages

```bash
yarn add <package>               # Add to dependencies
yarn add <package>@<version>     # Add specific version
yarn add <package> --dev         # Add to devDependencies
yarn add <package> --peer        # Add to peerDependencies
yarn add <package> --optional    # Add to optionalDependencies

yarn install                     # Install all dependencies
yarn install --force             # Force re-download
yarn install --production        # Only production dependencies

yarn global add <package>        # Install package globally
```

---

## Updating & Removing Packages

```bash
yarn upgrade <package>           # Upgrade to latest version
yarn upgrade <package>@<version> # Upgrade to specific version
yarn upgrade-interactive         # Interactive upgrade of dependencies

yarn remove <package>            # Remove a package
yarn global remove <package>     # Remove global package
```

---

## Listing & Info

```bash
yarn list                        # List installed packages
yarn list --depth=0              # Top-level only
yarn info <package>              # Package details
yarn why <package>               # Why a package is installed
yarn outdated                    # Show outdated packages
```

---

## Scripts

```json
"scripts": {
  "start": "node app.js",
  "test": "jest",
  "build": "webpack"
}
```

```bash
yarn run <script>                # Run any script
yarn start                       # Shortcut for "start"
yarn test                        # Shortcut for "test"
```

---

## Versioning

```bash
yarn version                     # Interactive version update
yarn version --patch             # Patch update (1.0.0 → 1.0.1)
yarn version --minor             # Minor update (1.0.0 → 1.1.0)
yarn version --major             # Major update (1.0.0 → 2.0.0)
```

---

## Workspaces

```bash
yarn workspaces list             # List all workspaces
yarn workspace <name> <cmd>      # Run command in workspace
```

---

## Cleaning & Diagnostics

```bash
yarn cache clean                 # Clear Yarn cache
yarn check                       # Verify dependency versions
yarn doctor                      # Check for common issues
yarn audit                       # Security check
yarn audit --groups dependencies # Audit only dependencies
```

---

## Lockfile

- **yarn.lock**: Automatically maintained. Commit this file for consistent installs.

---

## Miscellaneous

```bash
yarn help                        # Show Yarn help
yarn config list                 # Show Yarn config
yarn config set <key> <value>    # Set config value
yarn global bin                  # Show global binary path
yarn bin                         # Show binary path for local project
```

---

## Publishing Packages

```bash
yarn publish                     # Publish package to registry
```

---

## Yarn vs npm

- `yarn add` = `npm install`
- `yarn remove` = `npm uninstall`
- `yarn upgrade` = `npm update`
- `yarn run` = `npm run`
- `yarn global add` = `npm install -g`
- Yarn is faster and offers better dependency resolution.

---

**Tip:** Use [Yarn 2+](https://yarnpkg.com/) for advanced features like Plug'n'Play, zero-install, etc.
