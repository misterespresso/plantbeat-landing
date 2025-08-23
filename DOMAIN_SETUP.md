# Setting up plantbeat.net with GitHub Pages

## Step 1: DNS Configuration

Go to your domain registrar's DNS settings (where you bought plantbeat.net) and add these records:

### For plantbeat.net (apex domain):
Add these 4 A records:
- `185.199.108.153`
- `185.199.109.153`
- `185.199.110.153`
- `185.199.111.153`

### For www.plantbeat.net (optional):
Add a CNAME record:
- Name: `www`
- Value: `YOUR_GITHUB_USERNAME.github.io`

## Step 2: Deploy to GitHub

```bash
cd landing

# Initialize git if not already done
git init

# Add all files (including CNAME file)
git add .

# Commit
git commit -m "Add PlantBeat landing page with custom domain"

# Create repo on GitHub named "plantbeat-landing" or any name you prefer
# Then add remote:
git remote add origin https://github.com/YOUR_USERNAME/plantbeat-landing.git

# Push
git push -u origin main
```

## Step 3: Enable GitHub Pages

1. Go to your repository on GitHub
2. Settings → Pages
3. Source: Deploy from branch → main → / (root)
4. Custom domain: Enter `plantbeat.net`
5. Check "Enforce HTTPS" (may take a few minutes to be available)

## Step 4: Wait for Propagation

- DNS changes: 5 minutes to 48 hours (usually within 1 hour)
- GitHub Pages setup: 10-30 minutes
- HTTPS certificate: Up to 24 hours (usually within 1 hour)

## Verify Setup

Once DNS propagates, your site will be available at:
- `https://plantbeat.net`
- `https://www.plantbeat.net` (if you set up www)

## Common DNS Providers Instructions

### GoDaddy
1. Go to DNS Management
2. Add A records with @ as name
3. Add CNAME with www as name

### Namecheap
1. Advanced DNS
2. Add A records with @ as host
3. Add CNAME with www as host

### Cloudflare
1. DNS → Records
2. Add A records with @ as name (proxy OFF for GitHub Pages)
3. Add CNAME with www as name

### Google Domains
1. DNS → Manage custom records
2. Add A records with @ as host name
3. Add CNAME with www as host name

## Troubleshooting

If site doesn't load after 24 hours:
1. Check DNS propagation: https://dnschecker.org/#A/plantbeat.net
2. Verify CNAME file exists in repo
3. Check GitHub Pages settings shows "Your site is published at https://plantbeat.net"
4. Try clearing browser cache or incognito mode

## Email Collection Still Works!

The Supabase Edge Function at `https://xvnlxsawllvyrorrrxki.supabase.co/functions/v1/waitlist-signup` will work perfectly from plantbeat.net - no changes needed!