# Elmo — Pacific Bim Engineering Services

Static website for permit drafting business in Hawaii. Domain: onlydrafting.com

## Stack
- Pure static site: HTML/CSS/JS served by nginx
- No backend, no database, no Node.js runtime
- Container: Alpine + nginx with brotli and headers-more modules
- Deploy: Coolify auto-deploy on git push to main

## Structure
```
public/
  index.html         # Main landing page (52KB)
  dashboard.html     # Dashboard page (40KB)
  estimator.html     # Cost estimator (32KB)
  portfolio.html     # Portfolio showcase (31KB)
  robots.txt
Dockerfile           # Alpine + nginx
nginx.conf           # Server block (onlydrafting.com)
nginx-main.conf      # Main nginx config (workers, brotli)
security-headers.conf  # CSP, HSTS, X-Frame-Options (includes unpkg.com, tawk.to)
```

## Key Patterns
- Security headers in separate file, included by nginx.conf in multiple locations
- CSP allows: self, unsafe-inline, unpkg.com, tawk.to, Google Fonts
- HTML: no-cache policy. Static assets: 1-day cache
- www → non-www redirect configured in nginx

## Deploy
Git push to main → Coolify auto-deploy:
```bash
cd /projects/Elmo && git add -A && git commit -m "message" && git push origin main
```
Coolify container name varies (Coolify-managed).
