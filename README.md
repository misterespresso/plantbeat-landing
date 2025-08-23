# PlantBeat Landing Page

Simple, standalone landing page for PlantBeat with email signup and legal documents.

## Files

- `index.html` - Main landing page with email signup and image carousel
- `privacy.html` - Privacy policy page
- `terms.html` - Terms and conditions page  
- `about.html` - About PlantBeat page

## Deployment

This is a simple static site that can be deployed to any web hosting service:

### Option 1: GitHub Pages
1. Create a new repository or use existing one
2. Upload all HTML files to repository
3. Enable GitHub Pages in Settings > Pages
4. Site will be available at `https://[username].github.io/[repo-name]/`

### Option 2: Netlify (Drop & Deploy)
1. Visit https://app.netlify.com/drop
2. Drag and drop the `landing` folder
3. Get instant URL

### Option 3: Vercel
1. Install Vercel CLI: `npm i -g vercel`
2. Run `vercel` in the landing directory
3. Follow prompts

### Option 4: Traditional Web Hosting
1. Upload all HTML files via FTP/cPanel
2. Files should be in public_html or www directory
3. index.html will be served as homepage

## Features

- Mobile responsive design
- Auto-rotating image carousel (5 second intervals)
- Email signup form (currently stores to console - connect to backend as needed)
- Clean, professional design matching PlantBeat brand colors
- No dependencies - pure HTML/CSS/JavaScript
- Legal pages included (Privacy, Terms, About)

## Customization

To connect email signup to a backend:
1. Modify the `handleSubmit` function in index.html
2. Add fetch/axios call to your API endpoint
3. Handle response accordingly

To change images:
- Replace Unsplash URLs in carousel with your own image URLs
- Images should be 800x400 minimum for best quality