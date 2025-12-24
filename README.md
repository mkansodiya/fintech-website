# Static Build Files

This directory contains the static HTML, CSS, and JavaScript files for the XTentPay website.

## Build Information
- **Build Date**: $(date)
- **Next.js Version**: 16.1.1
- **Build Type**: Static Export
- **Total Size**: ~1.7MB

## Directory Structure
```
static-build/
├── index.html          # Homepage
├── contact/            # Contact page
├── pay-in/             # Pay-in page
├── payouts/            # Payouts page
├── pricing/            # Pricing page
├── security/           # Security page
├── 404.html            # 404 error page
└── _next/              # Next.js assets (JS, CSS, images)
```

## Hosting Instructions

### Option 1: Static Hosting Services
Upload the entire `static-build` directory contents to:
- **Netlify**: Drag and drop the folder or use CLI
- **Vercel**: Use `vercel --prod` from this directory
- **GitHub Pages**: Push to `gh-pages` branch
- **AWS S3 + CloudFront**: Upload to S3 bucket
- **Cloudflare Pages**: Connect repository or upload folder

### Option 2: Web Server (Nginx/Apache)
1. Copy all files from `static-build/` to your web server's document root
2. Configure your server to serve `index.html` for all routes (SPA routing)
3. Example Nginx config:
```nginx
server {
    listen 80;
    server_name yourdomain.com;
    root /path/to/static-build;
    index index.html;

    location / {
        try_files $uri $uri/ $uri.html /index.html;
    }
}
```

### Option 3: Docker Static Server
```bash
docker run -d -p 8080:80 \
  -v $(pwd)/static-build:/usr/share/nginx/html \
  nginx:alpine
```

## Notes
- All pages are pre-rendered as static HTML
- Images are unoptimized (as required for static export)
- All animations and interactivity are preserved
- The site is fully responsive and works offline

## Testing Locally
```bash
# Using Python
python3 -m http.server 8080 -d static-build

# Using Node.js (http-server)
npx http-server static-build -p 8080

# Using PHP
php -S localhost:8080 -t static-build
```

Then visit: http://localhost:8080

