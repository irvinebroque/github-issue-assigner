# GitHub Issue Auto-Assigner

This repository contains a GitHub Action that automatically assigns issues to Engineering Managers (EMs) and Product Managers (PMs) based on product team labels.

## How It Works

When a label is added to an issue, the action:
1. Checks if the label matches a configured product team
2. Looks up the assigned EM and PM for that team
3. Automatically assigns both users to the issue

## Supported Teams

The action currently supports the following product teams:

| Label | Engineering Manager | Product Manager |
|-------|-------------------|-----------------|
| TEST | irvinebroque | irvinebroque |

## Setup

The action is automatically enabled when you push this repository to GitHub. No additional setup is required.

### Requirements

- The action requires `issues: write` permissions (included in the workflow)
- Uses the default `GITHUB_TOKEN` (no additional secrets needed)

## Configuration

To add more teams or update assignments, modify the `TEAM_ASSIGNMENTS` object in `.github/workflows/assign-issues.js`:

```javascript
const TEAM_ASSIGNMENTS = {
  'TEST': {
    em: 'irvinebroque',
    pm: 'irvinebroque'
  },
  'YourLabel': {
    em: 'em-github-username',
    pm: 'pm-github-username'
  }
};
```

## Testing

To test the action:
1. Create an issue in your repository
2. Add the "TEST" label to the issue
3. The action should automatically assign `irvinebroque` to the issue

## Behavior

- **Trigger**: Only runs when labels are added to issues (not when removed)
- **Assignment**: Assigns both EM and PM if both are configured
- **Logging**: Provides detailed logs for debugging in the Actions tab
- **Graceful Handling**: Ignores unknown labels without errors

## Files

- `.github/workflows/auto-assign-issues.yml` - Main workflow configuration
- `.github/workflows/assign-issues.js` - Action logic and team mappings
- `.github/workflows/package.json` - Node.js dependencies

## Troubleshooting

1. **Action not triggering**: Ensure the label name exactly matches "TEST"
2. **User not assigned**: Verify that `irvinebroque` has access to the repository
3. **Permission errors**: Check that the action has `issues: write` permission

Check the Actions tab in your repository for detailed logs and error messages.