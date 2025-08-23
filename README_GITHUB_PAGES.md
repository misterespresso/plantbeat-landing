# Deploying to GitHub Pages

## Quick Setup

### 1. Create a New Repository
```bash
# Navigate to landing folder
cd landing

# Initialize git
git init

# Add all files
git add .

# Commit
git commit -m "Initial landing page"

# Create a new repo on GitHub (via browser or gh CLI)
# Then add remote:
git remote add origin https://github.com/YOUR_USERNAME/plantbeat-landing.git

# Push to main branch
git push -u origin main
```

### 2. Enable GitHub Pages
1. Go to your repository on GitHub
2. Click **Settings** → **Pages** (in left sidebar)
3. Under "Source", select **Deploy from a branch**
4. Choose **main** branch and **/ (root)** folder
5. Click **Save**

Your site will be available at:
- `https://YOUR_USERNAME.github.io/plantbeat-landing/`

## Custom Domain (Optional)

### Using a Custom Domain
1. Add a file named `CNAME` in the landing folder with your domain:
```
landing.plantbeat.com
```

2. In your domain's DNS settings, add:
   - For apex domain (plantbeat.com):
     - A records pointing to GitHub's IPs:
       - 185.199.108.153
       - 185.199.109.153
       - 185.199.110.153
       - 185.199.111.153
   
   - For subdomain (landing.plantbeat.com):
     - CNAME record pointing to `YOUR_USERNAME.github.io`

3. In GitHub repo settings → Pages → Custom domain:
   - Enter your domain
   - Check "Enforce HTTPS"

## Project Structure for GitHub Pages

```
plantbeat-landing/
├── index.html          # Main landing page (automatically served)
├── privacy.html        # Privacy policy
├── terms.html          # Terms & conditions
├── about.html          # About page
├── CNAME              # (Optional) Custom domain
├── .nojekyll          # Prevents Jekyll processing
└── README.md          # This file
```

## Automated Deployment with GitHub Actions

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy Landing Page

on:
  push:
    branches: [ main ]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
      
      - name: Setup Pages
        uses: actions/configure-pages@v4
      
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: '.'
      
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

## Important Notes

1. **Email Collection**: The Edge Function URL is hardcoded in `index.html`. It will work from any domain thanks to CORS headers set to `*`.

2. **Free Hosting**: GitHub Pages is completely free for public repositories.

3. **HTTPS**: GitHub Pages automatically provides HTTPS for both github.io domains and custom domains.

4. **Updates**: Any push to the main branch will automatically update the live site (takes 2-10 minutes).

5. **Edge Function**: Make sure your Supabase Edge Function (`waitlist-signup`) is deployed with `--no-verify-jwt` flag.

## Testing Locally

```bash
# Simple Python server
python -m http.server 8000

# Or Node.js
npx http-server

# Or Live Server VS Code extension
```

Then visit http://localhost:8000

## Monitoring

- Check deployment status: Repository → Actions tab
- View site metrics: Repository → Insights → Traffic
- Email collection: Check Supabase dashboard → Table Editor → email_waitlist