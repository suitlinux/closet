# GitHub Pages Setup Instructions

This document provides instructions for enabling GitHub Pages for the Closet repository.

## Prerequisites

- Repository must be on the `main` or `master` branch (or the workflow should be updated to match your default branch)
- Administrator access to the repository settings

## Steps to Enable GitHub Pages

### 1. Enable GitHub Pages in Repository Settings

1. Go to your repository on GitHub: https://github.com/suitlinux/closet
2. Click on **Settings** (⚙️ icon in the top menu)
3. In the left sidebar, scroll down and click on **Pages**
4. Under **Source**, select:
   - **Source**: GitHub Actions (recommended for this setup)
   - If "GitHub Actions" is not available, it will be enabled automatically when the workflow runs

### 2. Merge the Pull Request

Once you merge this pull request to the main branch, the GitHub Actions workflow will automatically:
- Deploy the repository to GitHub Pages
- Make it available at: https://suitlinux.github.io/closet/

### 3. Verify Deployment

After merging:
1. Go to the **Actions** tab in your repository
2. You should see a "Deploy to GitHub Pages" workflow running
3. Wait for it to complete (usually takes 1-2 minutes)
4. Visit https://suitlinux.github.io/closet/ to verify the site is live

### 4. Configure pacman to Use the Repository

Users can now add the repository to their Arch Linux systems by editing `/etc/pacman.conf`:

```ini
[closet]
Server = https://suitlinux.github.io/closet/$arch
SigLevel = Optional TrustAll
```

Then update package database:
```bash
sudo pacman -Sy
```

## Automatic Deployment

The GitHub Actions workflow is configured to automatically deploy on:
- Every push to the `main` or `master` branch
- Manual trigger via the Actions tab (workflow_dispatch)

## Troubleshooting

### Workflow Not Running
- Ensure GitHub Actions are enabled in repository settings
- Check that the workflow file is on the default branch

### 404 Error on GitHub Pages
- Verify GitHub Pages is enabled in repository settings
- Check that the workflow completed successfully in the Actions tab
- Wait a few minutes for DNS propagation

### Packages Not Accessible
- Ensure all package files (`.pkg.tar.zst`) are committed to the repository
- Verify the `x86_64` directory structure is correct
- Check that database files (`closet.db`, `closet.files`) are present

## Security Note

The current configuration uses `SigLevel = Optional TrustAll` for simplicity. For production use, consider:
1. Creating GPG keys for package signing
2. Signing all packages with `gpg --detach-sign`
3. Updating `SigLevel` to require signature verification
4. Providing the public key for users to import

## Files Created

This setup includes:
- `index.html` - Repository homepage
- `x86_64/index.html` - Package directory listing
- `.github/workflows/deploy-pages.yml` - GitHub Actions workflow
- `README.md` - Repository documentation
- `SETUP.md` - This file

## Maintenance

When adding new packages:
1. Add the `.pkg.tar.zst` file to the `x86_64/` directory
2. Run `./x86_64/mkrepo closet` to update the database
3. Update `x86_64/index.html` to include the new package (optional, for better UX)
4. Commit and push the changes
5. The GitHub Actions workflow will automatically deploy the updates
