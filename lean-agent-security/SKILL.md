---
name: lean-agent-security
description: Security and privacy rules for web apps and APIs. Use when writing or reviewing auth, login, forms, file uploads, user data, redirects, dependencies, security headers, deployment config, or Cloudflare setup. Also covers fake packages and SEO spam.
---

# Security rules

Security works in layers. If one layer fails, the next one stops the attack. Apply every rule that fits the task. At the end, tell the user which rules you skipped and why.

This is not a professional security review.

## Read more only when needed

The files are in `references/` next to this file.

- Site or app behind Cloudflare: read `references/cloudflare.md`.
- Public site with comments, search, uploads, or redirects: read `references/seo-spam.md`.
- Code that stores names, emails, IPs, or other personal data: read `references/privacy.md`.

## 1. Don't trust invented facts

- Before adding a package, check it exists on the official registry with that exact name. Attackers publish packages under names AI models often invent.
- Look for names one letter away from a popular package.
- Never invent CVE numbers, header names, or config options. If you can't confirm one, say so.

## 2. Secrets

- Never put secrets in code, committed config, logs, URLs, or browser code.
- Read secrets from environment variables. Make sure `.env` is in `.gitignore`.
- If a secret was committed, tell the user to rotate it. Deleting the file is not enough. It stays in git history.
- Don't ask the user to paste secrets into chat.

## 3. Input and output

- Validate all input on the server. Browser checks are only for user experience.
- Use parameterized queries. Never build SQL from strings.
- Never pass user input to a shell.
- Escape output for HTML. Don't use `innerHTML` or `dangerouslySetInnerHTML` with user data. If user HTML is needed, use DOMPurify.
- For file paths from user input, check the final path stays inside the allowed folder.
- When the server fetches a URL, block `localhost`, private IP ranges, and cloud metadata addresses.
- Redirect only to your own paths or a fixed allow list.
- Treat AI model output as untrusted input.

## 4. Login and permissions

- Use a known auth library. Don't write your own.
- Hash passwords with Argon2id, bcrypt, or scrypt.
- Check permissions on the server on every request. Check the user owns the record.
- Session cookies: `HttpOnly`, `Secure`, `SameSite=Lax`.
- Use the framework's CSRF protection.
- Rate limit login, signup, and password reset. Add a bot check like Cloudflare Turnstile to public forms.
- Make tokens with `crypto.randomUUID()`, `crypto.getRandomValues()`, or Python `secrets`. Never `Math.random()`.
- Compare secrets with a constant-time function.

## 5. Headers

Set these on HTML responses:

```
Content-Security-Policy: default-src 'self'; frame-ancestors 'none'
Strict-Transport-Security: max-age=31536000; includeSubDomains
X-Content-Type-Options: nosniff
Referrer-Policy: strict-origin-when-cross-origin
Permissions-Policy: camera=(), microphone=(), geolocation=()
```

Add to the CSP only the outside sources the site really uses. Turn on HSTS only when the whole domain works on HTTPS. For CORS, allow only the origins that need it. Never use `*` with credentials.

## 6. Dependencies

- Commit the lockfile. Use `npm ci` or the locked install in CI.
- Run `npm audit`, `pip-audit`, or `cargo audit` and report the results.
- Scripts from a CDN get an exact version and an `integrity` hash.
- Pin GitHub Actions to a commit SHA. Give workflows the smallest permissions.

## 7. Uploads

- Check the file type by its content. Limit the size.
- Rename files. Store them outside the web root or on a separate domain.
- Never serve uploads as HTML from the main domain.

## 8. Errors and logs

- Users see a generic error. Details stay in server logs.
- Never log passwords, tokens, or card numbers. Mask emails and other personal data.
- Log logins, failed logins, and admin actions.

## 9. Search spam

- Add `rel="ugc nofollow"` to links in user content.
- Add `noindex` to site search result pages.
- Never show search engines different content than visitors.

## 10. Privacy

- Collect only the data the feature needs.
- Delete it when it's no longer needed.
- No personal data in URLs or logs.
- No tracking scripts unless the user asks for them.

## Final check

- [ ] No secrets in code, logs, or commits.
- [ ] Input validated on the server. Output escaped.
- [ ] Permissions checked on the server.
- [ ] New packages confirmed real.
- [ ] Headers and cookie flags set.
- [ ] Personal data kept to a minimum and not logged.
- [ ] Told the user what you skipped.
