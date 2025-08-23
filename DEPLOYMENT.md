# Landing Page & Email Collection Deployment

## Edge Function Deployment (IMPORTANT - Do this first!)

The email collection requires deploying the Edge Function with JWT verification disabled.

### Option 1: Using Supabase CLI (Recommended)
```bash
# Make sure you're linked to your project
supabase link --project-ref xvnlxsawllvyrorrrxki

# Deploy with --no-verify-jwt flag
supabase functions deploy submit-waitlist --no-verify-jwt
```

### Option 2: Manual Dashboard Update
If the CLI deployment doesn't work:
1. Go to Supabase Dashboard > Edge Functions
2. Find the `submit-waitlist` function
3. Click on it and look for settings/configuration
4. Disable "Verify JWT" or "Require Authentication"
5. Save changes

The function is already deployed but needs JWT verification disabled to work as a public endpoint.

## Testing the Email Collection

1. Open the landing page in your browser
2. Submit an email address
3. You should see "Thank you for joining our waitlist!"

To verify emails are being collected, run this in Supabase SQL Editor (with service role):
```sql
SELECT * FROM email_waitlist ORDER BY created_at DESC;
```

## Security Features Active

- ✅ Table has RLS enabled with NO policies (inaccessible from client)
- ✅ Rate limiting (5 attempts per hour per IP)
- ✅ Email validation and disposable domain blocking
- ✅ No email enumeration (same response for duplicates)
- ✅ Public Edge Function (no auth required, but secure)
- ✅ All access goes through the Edge Function

## Landing Page Deployment Options

### GitHub Pages
```bash
# Create a new repo and push the landing folder
cd landing
git init
git add .
git commit -m "Initial landing page"
git remote add origin YOUR_REPO_URL
git push -u origin main
# Enable GitHub Pages in Settings
```

### Netlify Drop
1. Visit https://app.netlify.com/drop
2. Drag the `landing` folder
3. Get instant URL

### Vercel
```bash
cd landing
vercel
```

### Traditional Hosting
Upload all files in the `landing` folder to your web host's public_html directory.

## Important Notes

- The Edge Function URL is hardcoded in index.html - update it if your project changes
- Consider restricting CORS to your actual domain in production (currently set to '*')
- Monitor the rate limit table and adjust limits if needed
- Set up email verification (double opt-in) before sending marketing emails