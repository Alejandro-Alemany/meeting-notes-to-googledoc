# GitHub Setup Instructions

This guide will help you publish this project to GitHub and get your Colab notebook working with the repository.

## Step 1: Create a GitHub Repository

1. Go to [GitHub](https://github.com) and log in
2. Click the "+" icon in the top right corner
3. Select "New repository"
4. Fill in the details:
   - **Repository name**: `meeting-notes-to-googledoc`
   - **Description**: "Convert markdown meeting notes to formatted Google Docs"
   - **Visibility**: Public (required for Colab badge)
   - **Initialize**: Do NOT check any boxes (we already have files)
5. Click "Create repository"

## Step 2: Push Your Code to GitHub

Open a terminal in your project directory and run:

```bash
# Initialize git repository
git init

# Add all files
git add .

# Create initial commit
git commit -m "Initial commit: Meeting notes to Google Docs converter"

# Add GitHub remote (replace YOUR_USERNAME with your GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/meeting-notes-to-googledoc.git

# Push to GitHub
git branch -M main
git push -u origin main
```

## Step 3: Update the README

1. Open `README.md`
2. Find the "Open in Colab" badge section
3. Replace `YOUR_USERNAME` with your actual GitHub username:
   ```markdown
   [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/meeting-notes-to-googledoc/blob/main/meeting_notes_to_googledoc.ipynb)
   ```
4. Commit and push the change:
   ```bash
   git add README.md
   git commit -m "Update Colab badge with actual username"
   git push
   ```

## Step 4: Test the Colab Integration

1. Go to your GitHub repository in a browser
2. Navigate to `meeting_notes_to_googledoc.ipynb`
3. Click the "Open in Colab" button that appears at the top
4. Or manually open: `https://colab.research.google.com/github/YOUR_USERNAME/meeting-notes-to-googledoc/blob/main/meeting_notes_to_googledoc.ipynb`

## Step 5: Share Your Repository Link

Your repository is now ready to share! The URL will be:
```
https://github.com/YOUR_USERNAME/meeting-notes-to-googledoc
```

## Optional: Add a Profile Picture and Description

1. Go to your repository on GitHub
2. Click the gear icon (⚙️) next to "About"
3. Add a description
4. Add topics: `python`, `google-docs`, `markdown`, `colab`, `notebook`
5. Add a website URL if you have one
6. Save changes

## Troubleshooting

### Git Authentication Issues

If you have trouble pushing to GitHub, you may need to:

1. **Use SSH instead of HTTPS**:
   ```bash
   git remote set-url origin git@github.com:YOUR_USERNAME/meeting-notes-to-googledoc.git
   ```

2. **Use a Personal Access Token**:
   - Go to GitHub Settings > Developer settings > Personal access tokens
   - Generate a new token with `repo` scope
   - Use the token as your password when pushing

### Colab Can't Find the Notebook

Make sure:
- Your repository is public
- The notebook file is named exactly `meeting_notes_to_googledoc.ipynb`
- The notebook is in the root directory (not in a subdirectory)

## Next Steps

Once published:
1. Test the notebook in Colab
2. Add any additional documentation
3. Share the repository link for your assessment
4. Consider adding GitHub Actions for automated testing (optional)

