# Cloudflare security checklist

Use this when a site, app, or API runs behind Cloudflare. Feature names and plan limits change over time, so check the current [Cloudflare docs](https://developers.cloudflare.com/) before telling the user a setting exists on their plan.

For deeper, product-specific help, Cloudflare publishes its own agent skills at [github.com/cloudflare/skills](https://github.com/cloudflare/skills). Useful ones for security are `turnstile-spin` (bot checks on forms), `workers-best-practices`, and the WAF references inside the `cloudflare` skill.

## 1. Encryption

- Set SSL/TLS mode to Full (strict). Flexible mode leaves traffic between Cloudflare and your server unencrypted.
- Turn on Always Use HTTPS.
- Set the minimum TLS version to 1.2.
- Turn on HSTS only after every subdomain works over HTTPS, because browsers will refuse plain HTTP afterwards.

## 2. Hide and lock the origin server

Cloudflare only protects traffic that goes through it. If attackers find your server's real IP address, they can skip Cloudflare entirely.

- Best option: use Cloudflare Tunnel (`cloudflared`). The server then needs no open inbound ports.
- Otherwise, set the server's firewall to accept web traffic only from [Cloudflare's IP ranges](https://www.cloudflare.com/ips/), and consider Authenticated Origin Pulls so the server only accepts requests that really came from Cloudflare.
- Make sure web DNS records are proxied (orange cloud).
- Check for things that leak the origin IP: unproxied subdomains, mail records pointing to the same server, old DNS history, and the server answering requests sent straight to its IP.

## 3. DNS

- Turn on DNSSEC.
- Delete DNS records that point to services you no longer use. An attacker who claims the old service (an old cloud bucket or hosting app) can serve content on your subdomain. This is called subdomain takeover, and it is a common way to host spam on a trusted domain.

## 4. WAF (web application firewall)

- Turn on the managed rulesets your plan includes. Free plans get the Cloudflare Free Managed Ruleset. Paid plans add the Cloudflare Managed Ruleset and the OWASP Core Ruleset.
- Add custom rules for your own app, such as blocking access to admin paths from outside known countries or networks, or blocking methods your API doesn't use.
- When a rule blocks real users, fix that one rule with a narrow exception. Don't turn off whole rulesets.
- Rules run in a fixed order by phase. A skip rule only skips what it names. Check the security events log to see which rule actually acted on a request.

## 5. Rate limiting

- Add rate limiting rules for login, signup, password reset, contact forms, search, and expensive API endpoints.
- Counting by IP can block many users who share one IP, such as an office or a mobile network. Count by something more specific when your plan allows it, like a session cookie, API key, or header.

## 6. Bots and forms

- Turn on Bot Fight Mode on free plans, or Super Bot Fight Mode or Bot Management on plans that include them.
- Put Turnstile on public forms: signup, login, contact, comments, and password reset.
- Always verify the Turnstile token on the server by calling the Siteverify API (`https://challenges.cloudflare.com/turnstile/v0/siteverify`) with your secret key. Checking only in the browser does nothing, because a bot can skip the browser. Each token works once and expires after a few minutes. See [server-side validation](https://developers.cloudflare.com/turnstile/get-started/server-side-validation/).
- Keep the Turnstile secret key on the server only.

## 7. Admin pages

- Put admin panels, staging sites, and internal tools behind Cloudflare Access (Zero Trust), so users have to log in through your identity provider before the request reaches your app.
- This also protects admin pages of a CMS like WordPress from password guessing and plugin exploits.

## 8. Third-party scripts

- Use Cloudflare's client-side security feature (formerly Page Shield) where available to watch for new or changed scripts on your pages. Injected scripts are a common way to steal card data or add spam links.
- Add security headers (see the main skill) with Response Header Transform Rules or a Worker if the origin can't set them.

## 9. Workers and API tokens

- Store secrets with `wrangler secret put` or the Secrets Store. Never in `wrangler.toml`, `wrangler.jsonc`, or source code.
- Use `crypto.randomUUID()` or `crypto.getRandomValues()` for tokens, never `Math.random()`.
- Compare secrets with `crypto.subtle.timingSafeEqual`. Hash both values first so they have the same length, because returning early on a length mismatch leaks the length.
- Don't keep request data in variables at the module level. Workers reuse instances, so data can leak from one user's request to another's.
- Create API tokens with only the permissions and accounts they need. Don't use the Global API Key.

## 10. Caching

- Never cache pages that show personal data. Mark them with `Cache-Control: private, no-store`.
- Be careful with "Cache Everything" rules. They can cache a logged-in user's page and serve it to everyone.
