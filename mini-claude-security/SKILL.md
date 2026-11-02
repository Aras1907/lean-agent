---
name: mini-claude-security
description: Security, privacy, and anti-hallucination rules for coding agents. Covers secrets, input handling, auth, security headers, supply chain and fake packages, SEO spam and site hacks, personal data, and Cloudflare protection. Use when writing or reviewing web apps, APIs, auth, forms, file uploads, dependencies, deployment config, or anything that handles user data.
---

# Mini Claude: security and privacy

Security works in layers. If one layer fails, the next one should still stop the attack. Apply every layer below that fits the project, and tell the user about any layer you skipped.

This skill is in a testing phase. It doesn't replace a professional security review, and no results are guaranteed.

More detail is in these reference files:

- `references/cloudflare.md` for sites and apps behind Cloudflare
- `references/seo-spam.md` for stopping SEO spam and site hacks
- `references/privacy.md` for personal data

## 1. Think about attackers first

Before writing code that touches users, data, or the network, answer in a few lines:

- What is worth stealing or breaking here? Accounts, personal data, money, admin access, the site's search ranking.
- Where does untrusted input come in? Forms, URLs, headers, cookies, file uploads, webhooks, third-party APIs, AI model output.
- Who should be allowed to do what?

Use the answers to decide which of the layers below matter most.

## 2. Don't make things up (anti-hallucination)

Made-up facts are a security problem too. Attackers register package names that AI tools tend to invent, so installing a package that doesn't really exist can run their code.

- Before adding a dependency, check that the package exists on the official registry (npm, PyPI, crates.io, and so on), has the exact name you expect, a real maintainer, a history of releases, and reasonable download numbers. Watch for names that differ by one letter from a popular package.
- Never invent CVE numbers, security advisories, config options, header names, or API fields. If you can't confirm one, say so.
- When you state a security fact, point to where it came from: the official docs, the installed source, or the advisory.
- Mark anything you didn't verify as unverified.

## 3. Secrets

- Never put secrets in code, config files that get committed, logs, error messages, URLs, or client-side code.
- Load secrets from environment variables or a secrets manager. Make sure `.env` and similar files are in `.gitignore` before the first commit.
- If you find a secret that was committed, tell the user it must be rotated. Deleting it from the latest commit is not enough, because it stays in git history.
- Don't ask the user to paste secrets into chat. Ask them to set an environment variable instead.

## 4. Input and output

- Validate all input on the server, with an allow list of accepted values where you can. Client-side checks are for user experience only.
- Use parameterized queries or the ORM. Never build SQL with string concatenation.
- Never pass user input to a shell. If you must run a command, pass arguments as a list.
- Escape output for where it goes: HTML, attributes, URLs, JavaScript. Use the framework's escaping and avoid raw HTML features like `innerHTML` and `dangerouslySetInnerHTML`. If user HTML must be allowed, clean it with a maintained sanitizer such as DOMPurify.
- For file paths built from user input, resolve the final path and confirm it stays inside the allowed folder.
- For URLs the server fetches, block internal addresses (localhost, private IP ranges, cloud metadata addresses) to prevent SSRF.
- Redirects should only go to your own paths or a fixed allow list. Open redirects are used for phishing and SEO spam.
- Treat AI model output as untrusted input. Validate it before you run it, store it, or show it as HTML.

## 5. Authentication and access

- Use a well-known auth library or provider. Don't write your own password hashing or session system.
- Hash passwords with Argon2id, bcrypt, or scrypt.
- Check permissions on the server for every request, including that the user owns the record they're asking for. Hidden buttons are not access control.
- Session cookies get `HttpOnly`, `Secure`, and `SameSite=Lax` or `Strict`.
- Protect state-changing requests from CSRF with the framework's built-in protection.
- Rate limit login, signup, password reset, and other expensive endpoints. Add a bot check such as Cloudflare Turnstile to public forms.
- Use a cryptographically secure random generator for tokens (`crypto.randomUUID()`, `crypto.getRandomValues()`, Python's `secrets`), never `Math.random()`.
- Compare secrets and tokens with a constant-time comparison.

## 6. Security headers

Set these on HTML responses, adjusted to the app:

- `Content-Security-Policy`: start strict (`default-src 'self'`), list the outside sources you actually use, and add `frame-ancestors 'none'` or `'self'`.
- `Strict-Transport-Security: max-age=31536000; includeSubDomains`, only once the whole domain works over HTTPS.
- `X-Content-Type-Options: nosniff`
- `Referrer-Policy: strict-origin-when-cross-origin`
- `Permissions-Policy` turning off features the site doesn't use, such as camera, microphone, and geolocation.
- CORS: allow only the origins that need access. Never pair `Access-Control-Allow-Origin: *` with credentials.

## 7. Dependencies and supply chain

- Commit the lockfile. Install with the lockfile in CI (`npm ci`, `pip install` with hashes, `cargo build --locked`).
- Run the ecosystem's audit tool (`npm audit`, `pip-audit`, `cargo audit`) and report what it finds.
- Pin versions of scripts loaded from a CDN and add a Subresource Integrity (`integrity`) hash.
- Prefer fewer dependencies. A few lines of your own code are safer than a tiny unmaintained package.
- In CI, pin third-party GitHub Actions to a commit SHA and give workflows the smallest permissions they need.

## 8. Files and uploads

- Check the file type by its content, not only its extension. Limit file size.
- Rename uploaded files and store them outside the web root, or in object storage served from a separate domain.
- Never serve user uploads as HTML from your main domain. Attackers use that to host spam and phishing pages on your site.

## 9. Errors and logging

- Show users a generic error. Keep stack traces and internal details in server logs only.
- Never log passwords, tokens, full card numbers, or other secrets. Mask personal data in logs.
- Log security events: logins, failed logins, permission changes, and admin actions.

## 10. Search ranking and spam (SEO hacking)

Hacked sites are often used to host spam pages or hidden links that ride on the site's search ranking. The main defenses are in `references/seo-spam.md`. In short:

- Add `rel="ugc nofollow"` to links in user content, and sanitize user HTML.
- Don't let user content, search pages, or uploads create new indexable pages without review.
- Never show search engines different content than visitors (cloaking), and check that your server doesn't either.
- Watch for pages, files, or redirects you didn't create.

## 11. Privacy

Collect as little personal data as possible, keep it only as long as needed, and protect what you keep. Details are in `references/privacy.md`.

## 12. Cloudflare

If the site runs behind Cloudflare or the user is open to it, follow `references/cloudflare.md`. It covers the WAF, rate limiting, Turnstile, TLS settings, hiding the origin server, Zero Trust access for admin pages, and Workers secrets.

## 13. Before you finish

- [ ] No secrets in code, logs, or commits.
- [ ] All untrusted input is validated on the server, and output is escaped.
- [ ] Every request checks permissions on the server.
- [ ] Each new dependency was confirmed to exist and be the real package.
- [ ] Security headers and cookie flags are set.
- [ ] User content can't create spam links or indexable spam pages.
- [ ] Personal data is minimized, protected, and not logged.
- [ ] You told the user which layers you applied, which you skipped, and why.
