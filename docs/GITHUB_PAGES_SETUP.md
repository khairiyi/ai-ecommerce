# GitHub Pages Setup Instructions

Your HTML files have been committed and are ready to be pushed to GitHub. Follow these steps to enable GitHub Pages:

## Step 1: Push to GitHub

Since authentication is required, please push manually using one of these methods:

**Option A: Using GitHub Desktop or your preferred Git client**
- Open your Git client
- Push the committed changes to `origin/main`

**Option B: Using command line**
```bash
git push origin main
```
(You'll be prompted for your GitHub credentials)

## Step 2: Enable GitHub Pages

1. Go to your GitHub repository: https://github.com/khairiyi/ai-ecommerce
2. Click on **Settings** (in the repository navigation bar)
3. Scroll down to **Pages** in the left sidebar
4. Under **Source**, select:
   - **Deploy from a branch**
   - **Branch**: `main`
   - **Folder**: `/docs`
5. Click **Save**

## Step 3: Access Your Hosted Files

After enabling Pages (takes 1-2 minutes to build), your files will be available at:

- **Presentation**: https://khairiyi.github.io/ai-ecommerce/presentation.html
- **Architecture Diagram**: https://khairiyi.github.io/ai-ecommerce/architecture-diagram.html

You can share these URLs directly with others!

## Notes

- GitHub Pages may take 1-2 minutes to build after enabling
- The URLs will be publicly accessible (anyone with the link can view)
- If you update the HTML files, just commit and push - Pages will automatically rebuild
- If you want a custom domain later, GitHub Pages supports that in the Settings → Pages section

## Troubleshooting

If your pages don't appear after a few minutes:
- Check the **Actions** tab in your GitHub repository for any build errors
- Ensure your HTML files are in the `/docs` folder
- Verify the branch is set to `main` (or `master` if that's your default branch)
