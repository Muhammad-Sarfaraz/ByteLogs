# Husky

Husky helps automate Git hooks, allowing you to enforce rules and run scripts before pushing code.

## Installation

To install Husky, run the following commands:

```bash
npm install --save-dev husky --legacy-peer-deps
npx husky install
```

## Setting Up a Pre-Push Hook

1. Create a new hook file inside the `.husky` directory:

   ```bash
   npx husky add .husky/pre-push
   ```

2. Open the `.husky/pre-push` file and add your script:

   ```bash
   #!/bin/sh
   # Ensure the script exits if any command fails

   # Commands to execute before pushing
   echo "Running pre-push checks..."
   # Example: Run tests before pushing
   npm test
   ```

3. Make the script executable:

   ```bash
   chmod +x .husky/pre-push
   ```

## Ensuring Husky Runs Properly

To ensure Husky is correctly installed and configured in your project, add the following script to `package.json`:

```bash
npm pkg set scripts.prepare="husky install"
```

Then, reinstall Husky:

```bash
npm run prepare
```

## Creating Additional Git Hooks

Husky allows you to create different Git hooks. To add a new hook, use the following command:

```bash
npx husky add .husky/<hook-name>
```

For example, to create a `pre-commit` hook:

```bash
npx husky add .husky/pre-commit
```

Then edit the `.husky/pre-commit` file and add:

```bash
#!/bin/sh
set -e

# Example: Run linting before committing
npm run lint
```

## Uninstalling Husky

If you need to remove Husky from your project, run:

```bash
npm uninstall husky
rm -rf .husky
```
