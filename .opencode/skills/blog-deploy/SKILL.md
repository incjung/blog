---
name: blog-deploy
description: Deploy blog to production via git push using environment token authentication
license: MIT
compatibility: opencode
metadata:
  audience: blog authors
  workflow: deployment
---

## What I do
- Check git status and stage all changes
- Commit with descriptive message
- Push to remote using `BLOG_GIT_TOKEN` environment variable
- Handle draft to published conversion
- Stop local Hugo server if running

## When to use me
Use this when you are ready to:
- Publish draft posts to production
- Deploy recent changes to Netlify
- Update the live blog

## Prerequisites
- `BLOG_GIT_TOKEN` environment variable must be set:
  ```bash
  export BLOG_GIT_TOKEN="ghp_your_token_here"
  ```
- Git remote must be configured for HTTPS with token auth
- Must be in `/home/incjjung/github/blog` directory

## Usage Workflow

### 1. Pre-deployment Check
1. Check if Hugo server is running on port 1313
2. If running, suggest stopping it first
3. Ask user about draft posts:
   - List all posts with `draft: true`
   - Ask which ones to publish (change to `draft: false`)

### 2. Draft to Published (Optional)
For each post the user wants to publish:
1. Read the file
2. Change `draft: true` to `draft: false`
3. Update date to current date if desired

### 3. Git Operations
1. `git status` to see changes
2. `git add .` to stage all changes
3. `git commit -m "message"` with descriptive message
4. Configure git to use token:
   - Option A: `git remote set-url origin https://${BLOG_GIT_TOKEN}@github.com/incjjung/blog.git`
   - Option B: Use credential.helper
5. `git push origin main`

### 4. Verify Deployment
- Check that push was successful
- Mention that Netlify will automatically build and deploy
- Provide Netlify site URL for verification

## Security Notes
- Token is never logged or displayed
- Token is used only for the current git operation
- User should never commit the token to the repository

## Example
```
User: "Deploy my changes"
→ Check for drafts to publish
→ Stage and commit changes
→ Push with token authentication
→ Confirm Netlify deployment triggered
```

## Error Handling
- Verify `BLOG_GIT_TOKEN` is set
- Check git remote configuration
- Handle authentication failures gracefully
- Ensure no uncommitted changes will be lost
- Handle merge conflicts if they occur

## Post-deployment
- Confirm deployment URL: https://incjjung.netlify.app/
- Suggest verifying the live site
- Remind user to clear browser cache if changes not visible
