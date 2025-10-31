# GitHub Repository Setup Instructions

## Step 1: Configure Git (if not done already)

Run these commands in your terminal:

```bash
git config --global user.name "Arshia Jafari"
git config --global user.email "Arshiajfri@gmail.com"
```

## Step 2: Create Initial Commit

The repository has already been initialized. Run:

```bash
cd /Users/arshiajfri/Documents/UTMS/Semester3/Pattern/Projects/Project1
git add .gitignore README.md Main.ipynb continuum_removal/ Data/groundTruth_Cuprite_end12/ requirements.txt
git commit -m "Initial commit: Spectral Signature Continuum Removal project"
```

## Step 3: Create GitHub Repository

1. Go to [GitHub](https://github.com) and log in
2. Click the "+" icon in the top right corner
3. Select "New repository"
4. Repository name: `spectral-continuum-removal` (or any name you prefer)
5. Description: "Object-oriented spectral signature continuum removal using convex hull method"
6. Keep it **Public** or **Private** (your choice)
7. **DO NOT** initialize with README, .gitignore, or license (we already have them)
8. Click "Create repository"

## Step 4: Connect Local Repository to GitHub

After creating the repository on GitHub, run these commands:

```bash
cd /Users/arshiajfri/Documents/UTMS/Semester3/Pattern/Projects/Project1

# Add remote repository (replace YOUR_USERNAME with your actual GitHub username)
git remote add origin https://github.com/YOUR_USERNAME/spectral-continuum-removal.git

# Rename branch to main (if not already)
git branch -M main

# Push to GitHub
git push -u origin main
```

## Step 5: Verify Upload

- Go to your GitHub repository page
- You should see:
  - README.md
  - Main.ipynb
  - continuum_removal/ folder
  - Data/groundTruth_Cuprite_end12/ folder
  - requirements.txt

## What's Included

The following files have been staged for commit:
- ✅ README.md - Comprehensive project documentation
- ✅ Main.ipynb - Main analysis notebook
- ✅ continuum_removal/ - OOP module directory
  - continuum_removal.py - Main ContinuumRemoval class
  - Main.ipynb - Module notebook
- ✅ Data/groundTruth_Cuprite_end12/ - Ground truth data
  - groundTruth_Cuprite_nEnd12.mat - Spectral data
  - All mineral reference images (#1-#12)
- ✅ requirements.txt - Python dependencies
- ✅ .gitignore - Git ignore rules

## Large Files Note

The following files are NOT tracked (too large for GitHub):
- Data/CupriteS1_R188.mat
- Data/Cuprite_f970619t01p02_r02_sc03.a.rfl.mat
- Data/groundTruth_Cuprite_end12.zip

These can be added later using Git LFS if needed.

## Next Steps

After uploading:
1. Add topics/tags to your repository: `spectroscopy`, `hyperspectral`, `continuum-removal`, `python`, `machine-learning`
2. Enable GitHub Pages if you want to display the notebook
3. Add collaborators if working in a team
4. Set up GitHub Actions for automated testing (optional)

