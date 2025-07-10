# 🐍 Contribution Snake Setup Guide

## What is the Contribution Snake?

The contribution snake is an animated visualization of your GitHub contribution graph that creates a snake-like pattern eating your contributions. It's a fun and unique way to display your GitHub activity!

## Setup Instructions

### 1. Create a Special Repository

Create a new repository with the same name as your GitHub username (e.g., if your username is `johndoe`, create a repository named `johndoe`).

### 2. Add the Snake Workflow

Create the following file structure in your repository:

```
your-username/
├── .github/
│   └── workflows/
│       └── snake.yml
└── README.md
```

### 3. Create the Workflow File

Create `.github/workflows/snake.yml` with this content:

```yaml
name: Generate Snake

on:
  schedule:
    - cron: "0 */12 * * *"  # Runs every 12 hours
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2

      - uses: Platane/snk@master
        id: snake-gif
        with:
          github_user_name: ${{ github.repository_owner }}
          svg_out_path: dist/github-contribution-grid-snake-dark.svg
          snake_color: 'blue'

      - uses: crazy-max/ghaction-github-pages@v2.1.3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}

      - uses: actions/upload-artifact@v2
        with:
          name: contribution-grid-snake
          path: dist/github-contribution-grid-snake-dark.svg
```

### 4. Update Your README

In your main README.md file, replace the contribution snake section with:

```markdown
## 🐍 Contribution Snake

<div align="center">
  <img src="https://github.com/YOUR_USERNAME/YOUR_USERNAME/blob/output/github-contribution-grid-snake-dark.svg" alt="Contribution Snake" />
</div>
```

### 5. Enable GitHub Pages

1. Go to your repository settings
2. Scroll down to "Pages" section
3. Set source to "Deploy from a branch"
4. Select "output" branch
5. Save

### 6. Customization Options

You can customize the snake by modifying the workflow:

- **Colors**: Change `snake_color` to any color (e.g., 'green', 'red', 'purple')
- **Schedule**: Modify the cron expression to run at different intervals
- **Theme**: The snake automatically adapts to dark/light themes

### 7. Alternative: Use a Different Snake Service

If you prefer not to set up the workflow, you can use an external service:

```markdown
## 🐍 Contribution Snake

<div align="center">
  <img src="https://github.com/YOUR_USERNAME/YOUR_USERNAME/blob/output/github-contribution-grid-snake-dark.svg" alt="Contribution Snake" />
</div>
```

Or use a different service:

```markdown
<div align="center">
  <img src="https://github-readme-activity-graph.vercel.app/graph?username=YOUR_USERNAME&theme=react-dark&hide_border=true&area=true" alt="Contribution Graph" />
</div>
```

## Troubleshooting

1. **Snake not appearing**: Make sure the workflow has run at least once
2. **Wrong username**: Double-check that your repository name matches your GitHub username exactly
3. **No output branch**: The workflow creates the output branch automatically on first run
4. **Permission issues**: Ensure the workflow has write permissions to the repository

## Tips

- The snake updates every 12 hours by default
- You can manually trigger the workflow from the Actions tab
- The snake color can be customized to match your profile theme
- Consider adding a loading state while the snake generates

## Credits

This setup uses the [Platane/snk](https://github.com/Platane/snk) action to generate the contribution snake. 