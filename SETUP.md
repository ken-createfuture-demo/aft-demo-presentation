# Quick Setup Instructions

## You're Ready to Upload!

This folder contains everything you need for your GitHub presentation.

## What's Inside

```
aft-presentation-upload/
├── README.md              # Main readme (EDIT THIS - add your details)
├── presentation.html      # Your presentation
├── SETUP.md              # This file
├── slides/               # Individual markdown slides
│   ├── 00-prerequisites.md
│   ├── 01-introduction.md
│   ├── 02-architecture.md
│   ├── 03-workflow.md
│   ├── 04-customisations.md
│   ├── 05-demo.md
│   └── 06-work-done.md
└── assets/               # Your screenshots go here
    └── README.md         # Instructions for what images to add
```

## Setup Steps

### 1. Edit README.md

Open `README.md` and replace:
- `YOUR-USERNAME` with your GitHub username
- `YOUR-REPO` with your repo name (probably `aft-presentation`)
- Add links to your other AFT repos
- Add your name and date at the bottom

### 2. Add Your Screenshots

Copy your pipeline screenshots into the `assets/` folder. See `assets/README.md` for the list.

### 3. Create GitHub Repo

1. Go to github.com
2. Click "New repository"
3. Name: `aft-presentation`
4. Make it **Public**
5. Don't tick "Add README" (you already have one)
6. Create repository

### 4. Upload Everything

```bash
# Navigate to this folder
cd aft-presentation-upload

# Initialise git
git init

# Add your remote (replace YOUR-USERNAME)
git remote add origin https://github.com/YOUR-USERNAME/aft-presentation.git

# Add all files
git add .

# Commit
git commit -m "Initial commit: AFT presentation"

# Push
git branch -M main
git push -u origin main
```

### 5. Enable GitHub Pages

1. Go to your repo on GitHub
2. Settings → Pages
3. Source: Deploy from a branch
4. Branch: main
5. Folder: / (root)
6. Save

Wait 2-3 minutes, then your presentation will be at:
`https://YOUR-USERNAME.github.io/aft-presentation/presentation.html`

## Your URLs

Once setup:

**Presentation:**
```
https://YOUR-USERNAME.github.io/aft-presentation/presentation.html
```

**Repository:**
```
https://github.com/YOUR-USERNAME/aft-presentation
```

**Slides:**
```
https://github.com/YOUR-USERNAME/aft-presentation/tree/main/slides
```

## During Your Presentation

### Tab Setup

Have these tabs open:

1. Your presentation repo (start here)
2. The HTML presentation (for slides)
3. Your aft-account-request repo (for code examples)
4. Your aft-global-customisations repo
5. Your aft-account-customisations repo
6. Your aft-account-provisioning-customisations repo

### Presentation Flow

1. Start at your repo, show the README (overview)
2. Open presentation.html (the slides)
3. Present through slides 1-15 (intro and prerequisites)
4. Switch to your code repos when showing AFT deployment
5. Walk through the account request example
6. Show the three customisation repos
7. Back to presentation for results and summary

### Key Message

When you get to Control Tower:

> "Control Tower creates the Log Archive and Audit accounts automatically. 
> You don't provision them yourself. You just provide two email addresses, 
> and Control Tower creates these AWS accounts for you."

## Testing

Before presenting:

- [ ] Check presentation loads on GitHub Pages
- [ ] Navigate through a few slides
- [ ] Verify diagrams render (need internet)
- [ ] Test switching between tabs
- [ ] Make sure all your AFT repos are public

## Backup Plan

If GitHub Pages doesn't work:

1. Open `presentation.html` locally in your browser
2. Or navigate through markdown slides directly on GitHub

## Need Help?

- Check your README is correct (username, repo name)
- Make sure GitHub Pages is enabled
- Wait 5 minutes after enabling Pages
- Try incognito window if it won't load

---

That's it! You're ready to present.
