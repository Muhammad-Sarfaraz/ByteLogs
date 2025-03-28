# Hooks
Git hooks are scripts that Git executes automatically at different stages of the workflow. They help enforce policies, automate processes, and improve code quality. Hooks are stored in the `.git/hooks/` directory of a repository.

## Types of Git Hooks  
Git hooks are classified into **client-side** and **server-side** hooks:

### Client-Side Hooks  
Executed on a local machine before or after key Git operations.

- **pre-commit**: Runs before a commit is recorded (e.g., code linting, formatting checks).
- **prepare-commit-msg**: Runs before the commit message editor appears.
- **commit-msg**: Runs after the commit message is entered, allowing message validation.
- **pre-rebase**: Runs before a rebase operation.
- **post-commit**: Runs after a commit is completed (e.g., notifications or logging).
- **post-checkout**: Runs after `git checkout`, useful for environment setup.
- **post-merge**: Runs after a merge completes.
- **pre-push**: Runs before a push operation, commonly used for tests or code validation.

### Server-Side Hooks  
Executed on the remote repository (bare repository) when certain actions occur.

- **pre-receive**: Runs before Git updates the repository, used for policy enforcement.
- **update**: Similar to pre-receive, but runs for each branch being pushed.
- **post-receive**: Runs after the server has accepted a push, used for notifications.

## Example 1: Pre-Commit Hook (ESLint Check)  
Ensure code quality before committing changes.

1. Navigate to the hooks directory:
   ```bash
   cd .git/hooks
   ```
2. Create/edit the `pre-commit` file:
   ```bash
   nano pre-commit
   ```
3. Add the following script:
   ```bash
   #!/bin/sh
   set -e

   echo "Running ESLint..."
   npm run lint
   ```
4. Make it executable:
   ```bash
   chmod +x pre-commit
   ```

## Example 2: Pre-Push Hook (Run Tests Before Pushing)  
Prevent broken code from being pushed to the remote repository.

1. Create/edit the `pre-push` file:
   ```bash
   nano pre-push
   ```
2. Add the script to run tests:
   ```bash
   #!/bin/sh
   set -e

   echo "Running tests before push..."
   npm test
   ```
3. Make it executable:
   ```bash
   chmod +x pre-push
   ```

## Example 3: Commit Message Hook (Enforce Message Format)  
Ensure commit messages follow a specific format.

1. Create/edit the `commit-msg` file:
   ```bash
   nano commit-msg
   ```
2. Add validation logic:
   ```bash
   #!/bin/sh
   commit_msg=$(cat "$1")

   if ! echo "$commit_msg" | grep -qE "^JIRA-[0-9]+: .{10,}$"; then
       echo "Commit message must start with a JIRA ticket (e.g., JIRA-123: Fix bug)"
       exit 1
   fi
   ```
3. Make it executable:
   ```bash
   chmod +x commit-msg
   ```

## Example 4: Post-Receive Hook (Notify Team on Slack)  
Send notifications after a push is received.

1. Create/edit the `post-receive` file on the server:
   ```bash
   nano post-receive
   ```
2. Add a script to send a Slack notification:
   ```bash
   #!/bin/sh
   curl -X POST -H 'Content-type: application/json' \
   --data '{"text":"New code pushed to repository!"}' \
   https://hooks.slack.com/services/YOUR_SLACK_WEBHOOK_URL
   ```
3. Make it executable:
   ```bash
   chmod +x post-receive
   ```

