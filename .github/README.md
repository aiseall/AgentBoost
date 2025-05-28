# GitHub Actions & Dependabot Configuration

This directory contains the GitHub Actions workflows and Dependabot configuration for the AgentBoost repository.

## Workflows

### 1. Dependabot Auto-Merge (`dependabot-auto-merge.yml`)

This workflow automatically handles Dependabot pull requests:

**Features:**
- **Auto-approval**: Automatically approves patch and minor version updates
- **Auto-merge**: Automatically merges patch and minor updates when tests pass (or when no tests exist)
- **Manual review for major updates**: Major version updates require manual review due to potential breaking changes
- **Smart labeling**: Adds appropriate labels based on update type
- **Test awareness**: Waits for tests to pass before merging (if tests exist)

**Behavior:**
- ✅ **Patch updates** (e.g., 1.0.0 → 1.0.1): Auto-approved and auto-merged
- ✅ **Minor updates** (e.g., 1.0.0 → 1.1.0): Auto-approved and auto-merged
- ⚠️ **Major updates** (e.g., 1.0.0 → 2.0.0): Commented for manual review

### 2. Continuous Integration (`ci.yml`)

This workflow runs tests and linting for the project:

**Features:**
- **Multi-language support**: Detects and handles Python and Node.js projects
- **Multiple Python versions**: Tests against Python 3.8, 3.9, 3.10, and 3.11
- **Flexible test detection**: Automatically detects and runs various test frameworks
- **Linting support**: Runs linters if they're configured
- **Graceful fallback**: Provides helpful messages when no tests are found

**Supported test frameworks:**
- **Python**: pytest, unittest, tox
- **Node.js**: npm test
- **Linting**: flake8, black, isort (Python), eslint (Node.js)

## Dependabot Configuration (`dependabot.yml`)

Dependabot is configured to automatically check for updates:

**Update schedule**: Weekly on Mondays at 9:00 AM
**Supported ecosystems**:
- Python (pip)
- Node.js (npm)
- GitHub Actions
- Docker

**Settings**:
- Maximum 10 open PRs for package dependencies
- Maximum 5 open PRs for GitHub Actions and Docker
- Automatic assignment to repository owner
- Consistent commit message formatting
- Appropriate labeling

## Security Considerations

The auto-merge workflow includes several security measures:

1. **Limited scope**: Only runs for Dependabot PRs
2. **Version restrictions**: Only auto-merges patch and minor updates
3. **Test requirements**: Waits for tests to pass before merging
4. **Manual review for major changes**: Major updates require human review
5. **Proper permissions**: Uses minimal required GitHub token permissions

## Customization

To customize the behavior:

1. **Change auto-merge criteria**: Edit the conditions in `dependabot-auto-merge.yml`
2. **Add more test frameworks**: Extend the test detection logic in `ci.yml`
3. **Modify update schedule**: Change the schedule in `dependabot.yml`
4. **Add more reviewers**: Update the reviewers list in `dependabot.yml`

## Getting Started

1. **Enable Dependabot**: The configuration will automatically enable Dependabot for your repository
2. **Add tests**: When you add tests to your project, the CI workflow will automatically detect and run them
3. **Monitor PRs**: Dependabot will start creating PRs for dependency updates
4. **Review major updates**: Keep an eye on major version updates that require manual review

## Troubleshooting

**Auto-merge not working?**
- Check that the PR is from Dependabot
- Verify that tests are passing (if tests exist)
- Ensure the update is patch or minor (not major)
- Check the workflow logs for any errors

**Tests not running?**
- Ensure your test files follow standard naming conventions
- Add a `requirements.txt` or `package.json` file
- Check that your test framework is properly configured

**Need help?**
- Check the workflow run logs in the Actions tab
- Review the workflow files for configuration details
- Open an issue if you encounter problems