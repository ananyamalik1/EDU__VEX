# EduVexa Deployment Guide

Deploy your EduVexa app to Vercel in minutes!

## Prerequisites

- GitHub account
- Vercel account (free at vercel.com)
- Project committed to GitHub

## Deployment Steps

### 1. Push to GitHub

\`\`\`bash
git init
git add .
git commit -m "Initial EduVexa commit"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/eduvexa.git
git push -u origin main
\`\`\`

### 2. Connect to Vercel

1. Visit [vercel.com/new](https://vercel.com/new)
2. Click "Import Git Repository"
3. Paste your GitHub repo URL
4. Click "Import"

### 3. Configure Project

- **Framework**: Next.js
- **Root Directory**: ./
- **Build Command**: `npm run build`
- **Output Directory**: `.next`
- **Install Command**: `npm install`

### 4. Set Environment Variables (Optional)

If you add real integrations later:

\`\`\`
DATABASE_URL=your_database_url
API_KEY=your_api_key
\`\`\`

### 5. Deploy

1. Click "Deploy"
2. Wait 2-3 minutes
3. Get your live URL!

---

## Production Optimizations

### Add Real Database (Supabase Example)

\`\`\`bash
npm install @supabase/supabase-js
\`\`\`

Then update API routes to use Supabase instead of mock data.

### Add Video Hosting (Vercel Blob Example)

\`\`\`bash
npm install @vercel/blob
\`\`\`

Update reel player to use actual video URLs.

### Enable Analytics

Add to `app/layout.tsx`:

\`\`\`typescript
import { Analytics } from '@vercel/analytics/next'

// In return statement
<Analytics />
\`\`\`

---

## Custom Domain

1. In Vercel dashboard, go to Settings → Domains
2. Add your custom domain
3. Update DNS settings
4. Verify domain

---

## Environment Variables

### Local Development
Create `.env.local`:
\`\`\`
NEXT_PUBLIC_API_URL=http://localhost:3000
\`\`\`

### Production
Add in Vercel dashboard → Settings → Environment Variables

---

## Monitoring

### Check Deployment Status
- Visit Vercel dashboard
- Click your project
- View recent deployments

### View Logs
\`\`\`bash
vercel logs
\`\`\`

### Monitor Performance
- Use Vercel Analytics
- Check Core Web Vitals
- Monitor API response times

---

## Troubleshooting

### Build Fails
\`\`\`bash
# Clear cache and rebuild
npm run build
vercel --prod
\`\`\`

### Environment Variables Not Working
- Verify added to Vercel dashboard
- Rebuild deployment
- Check variable names (case-sensitive)

### Videos Not Playing
- Verify video URLs are public
- Check CORS headers
- Use Vercel Blob for hosting

### Theme Not Persisting
- Ensure localStorage is enabled
- Check cookie settings
- Clear browser cache

---

## Scaling Considerations

### As User Base Grows:

1. **Database**: Migrate to Supabase/Neon
2. **Videos**: Use Vercel Blob or AWS S3
3. **Caching**: Add Redis with Upstash
4. **Analytics**: Implement Vercel Analytics
5. **Auth**: Use NextAuth.js or Supabase Auth

### Performance Tips:

- Enable ISR (Incremental Static Regeneration)
- Optimize images with next/image
- Use Edge Functions for API routes
- Implement CDN caching headers

---

## CI/CD with GitHub Actions

Create `.github/workflows/deploy.yml`:

\`\`\`yaml
name: Deploy to Vercel

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v2
      - uses: vercel/action@master
        with:
          vercel-token: \${{ secrets.VERCEL_TOKEN }}
          vercel-org-id: \${{ secrets.VERCEL_ORG_ID }}
          vercel-project-id: \${{ secrets.VERCEL_PROJECT_ID }}
\`\`\`

---

## Rollback

If deployment breaks:

1. Go to Vercel dashboard
2. Select project
3. Click "Deployments"
4. Find previous working deployment
5. Click three dots → "Promote to Production"

---

## SEO Setup

Update `app/layout.tsx`:

\`\`\`typescript
export const metadata: Metadata = {
  title: "EduVexa - Bite-Sized Learning",
  description: "Learn faster with TikTok-style video lessons",
  openGraph: {
    type: "website",
    locale: "en_US",
    url: "https://yourdomain.com",
  },
}
\`\`\`

---

## Performance Checklist

- [x] Images optimized with next/image
- [x] CSS minified (Tailwind)
- [x] JavaScript code-split
- [x] API routes responding < 200ms
- [x] Videos using public URLs
- [x] No console errors in production
- [x] Lighthouse score > 90

---

## Backup Strategy

1. Regular GitHub commits
2. Database backups (if using real DB)
3. Video backups (if using cloud storage)
4. Daily Vercel deployments logged

---

## Support & Resources

- **Vercel Docs**: https://vercel.com/docs
- **Next.js Docs**: https://nextjs.org/docs
- **GitHub Issues**: Report bugs in repo
- **Community**: Next.js Discord

---

**Happy Deploying!**

Your EduVexa app is now live to the world.
\`\`\`
