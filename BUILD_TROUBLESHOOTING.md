# Vercel Build Troubleshooting

## Common Build Errors & Solutions

### 1. TypeScript Errors
**Error:** `Type error: ...`
**Solution:** 
- Check TypeScript errors locally: `npx tsc --noEmit`
- Fix any type errors in the code

### 2. Missing Dependencies
**Error:** `Module not found: Can't resolve ...`
**Solution:**
- Make sure all dependencies are in `package.json`
- Run `npm install` locally to verify

### 3. ESLint Errors
**Error:** `ESLint errors found`
**Solution:**
- Check `.eslintrc` or `eslint.config.mjs`
- Temporarily disable ESLint in `next.config.ts`:
```typescript
const nextConfig = {
  eslint: {
    ignoreDuringBuilds: true,
  },
};
```

### 4. Environment Variables
**Error:** `Missing environment variable`
**Solution:**
- Add all required env vars in Vercel Settings → Environment Variables
- Make sure they're set for the correct environment (Production/Preview)

### 5. Build Timeout
**Error:** Build takes too long
**Solution:**
- Check for infinite loops in code
- Reduce bundle size
- Check for large dependencies

### 6. Tailwind CSS Issues
**Error:** `PostCSS` or `Tailwind` errors
**Solution:**
- Verify `postcss.config.mjs` is correct
- Check `globals.css` imports Tailwind

## How to Get Full Error Details

1. **In Vercel Dashboard:**
   - Go to your project
   - Click on the failed deployment
   - Scroll down to see full build logs
   - Look for red error messages

2. **Common Error Locations:**
   - After "Installing dependencies..."
   - After "Running build..."
   - TypeScript compilation errors
   - ESLint errors

## Quick Fixes to Try

### Disable ESLint During Build (Temporary)
Add to `next.config.ts`:
```typescript
const nextConfig = {
  eslint: {
    ignoreDuringBuilds: true,
  },
  typescript: {
    ignoreBuildErrors: false, // Keep this false to catch type errors
  },
};
```

### Check Node Version
Vercel uses Node 18+ by default. If you need a specific version, add to `package.json`:
```json
{
  "engines": {
    "node": ">=18.0.0"
  }
}
```

## What to Share for Help

If build still fails, share:
1. **Complete error message** from Vercel build logs
2. **Which step failed** (Installing, Building, etc.)
3. **Any TypeScript errors** shown
4. **Environment variables** status (are they set?)

