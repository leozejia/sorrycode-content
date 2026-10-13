# Redirect Configuration for Deleted Documents

This document lists the redirect rules needed for deleted documentation pages.

## Required 301 Redirects

### 1. gpt-5-6-sol → models/how-to-query

**Old URLs**:
- `/docs/runtime/gpt-5-6-sol`
- `/docs/runtime/gpt-5-6-sol/`

**New URL**:
- `/docs/models/how-to-query`

**Reason**: Model version documentation becomes outdated quickly. Users should query dynamically instead of reading static model lists.

### 2. codex-multi-model → magpie

**Old URLs**:
- `/docs/runtime/codex-multi-model`
- `/docs/runtime/codex-multi-model/`

**New URL**:
- `/docs/runtime/magpie#multi-model`

**Reason**: magpie provides a better multi-model management solution. The old manual configuration method is obsolete.

### 3. current-lineup → how-to-query

**Old URLs**:
- `/docs/models/current-lineup`
- `/docs/models/current-lineup/`

**New URL**:
- `/docs/models/how-to-query`

**Reason**: Static model lists become outdated. Users should learn to query dynamically.

## Implementation

### For Next.js / React Router

```javascript
// next.config.js or similar
module.exports = {
  async redirects() {
    return [
      {
        source: '/docs/runtime/gpt-5-6-sol/:path*',
        destination: '/docs/models/how-to-query',
        permanent: true, // 301 redirect
      },
      {
        source: '/docs/runtime/codex-multi-model/:path*',
        destination: '/docs/runtime/magpie',
        permanent: true,
      },
      {
        source: '/docs/models/current-lineup/:path*',
        destination: '/docs/models/how-to-query',
        permanent: true,
      },
    ]
  },
}
```

### For Nginx

```nginx
# In your nginx.conf or site config

# Redirect gpt-5-6-sol
location ~ ^/docs/runtime/gpt-5-6-sol {
    return 301 /docs/models/how-to-query;
}

# Redirect codex-multi-model
location ~ ^/docs/runtime/codex-multi-model {
    return 301 /docs/runtime/magpie;
}

# Redirect current-lineup
location ~ ^/docs/models/current-lineup {
    return 301 /docs/models/how-to-query;
}
```

### For Apache

```apache
# In your .htaccess or httpd.conf

# Redirect gpt-5-6-sol
RedirectMatch 301 ^/docs/runtime/gpt-5-6-sol(.*)$ /docs/models/how-to-query

# Redirect codex-multi-model
RedirectMatch 301 ^/docs/runtime/codex-multi-model(.*)$ /docs/runtime/magpie

# Redirect current-lineup
RedirectMatch 301 ^/docs/models/current-lineup(.*)$ /docs/models/how-to-query
```

## Testing Redirects

After implementing redirects, test them:

```bash
# Test gpt-5-6-sol redirect
curl -I https://sorrycode.com/docs/runtime/gpt-5-6-sol
# Should return: HTTP/1.1 301 Moved Permanently
# Location: /docs/models/how-to-query

# Test codex-multi-model redirect
curl -I https://sorrycode.com/docs/runtime/codex-multi-model
# Should return: HTTP/1.1 301 Moved Permanently
# Location: /docs/runtime/magpie

# Test current-lineup redirect
curl -I https://sorrycode.com/docs/models/current-lineup
# Should return: HTTP/1.1 301 Moved Permanently
# Location: /docs/models/how-to-query
```

## Update Internal Links

Search and replace internal links in remaining documentation:

### Search patterns:

```bash
# Find references to deleted docs
grep -r "gpt-5-6-sol" articles/
grep -r "codex-multi-model" articles/
grep -r "current-lineup" articles/
```

### Replace with:

- `/docs/runtime/gpt-5-6-sol` → `/docs/models/how-to-query`
- `/docs/runtime/codex-multi-model` → `/docs/runtime/magpie`
- `/docs/models/current-lineup` → `/docs/models/how-to-query`

## Monitoring

After deployment, monitor:

1. **404 errors** - Check if any pages still link to deleted docs
2. **Redirect chains** - Ensure redirects go directly to final destination
3. **User feedback** - Users reporting broken links

## Notes

- All redirects are **permanent (301)** - tells search engines pages have moved
- Old URLs will eventually be deindexed by search engines
- Keep redirects active for at least 6-12 months
- Update sitemaps to reflect new structure
