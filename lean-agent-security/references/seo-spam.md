# Stopping SEO spam and site hacks

Attackers break into sites to borrow their search ranking. They add spam pages, hidden links, or redirects, and often show the spam only to search engines so the owner doesn't notice. Google can then flag or drop the site from search results.

## How it usually looks

- Spam pages: Thousands of new pages full of keywords and links, sometimes made to look like a 404 page. One well-known version fills new folders with Japanese text selling counterfeit goods.
- Hidden links: Links added to existing pages with CSS that hides them from visitors.
- Cloaking: The server shows spam to search engine crawlers and normal content to visitors, usually by checking the `User-Agent` or `Referer` header.
- Sneaky redirects: Visitors who come from a search engine, or on mobile, get sent to a spam or scam site.

## How attackers get in

- Outdated CMS core, plugins, or themes. This is the most common way in.
- SQL injection or stored XSS that lets them write content into the database.
- File uploads that can be served as HTML or run as PHP.
- Open redirects on your domain.
- Your own site search results pages getting indexed, so spammers can make "pages" by searching for spam keywords.
- User profiles, comments, and forums that let anyone post links.
- Subdomains pointing to services you no longer use (subdomain takeover).
- A compromised third-party script that adds links or redirects.
- Stolen admin or FTP passwords.

## What to do when writing code

- Sanitize user HTML and add `rel="ugc nofollow"` to every link in user content.
- Add `<meta name="robots" content="noindex">` to internal search results pages and other pages built from query strings.
- Only allow redirects to your own paths or a fixed allow list.
- Store uploads outside the web root, or on a separate domain. Make sure upload folders can never run scripts.
- Build the sitemap from your own data, never from user input or crawled URLs.
- Set a canonical URL on each page.
- Use a Content Security Policy so injected scripts from unknown domains don't load.
- Never check the `User-Agent` to serve different content to search engines. If a crawler needs a different response for a real reason, such as pre-rendering, the content must be the same.
- `robots.txt` doesn't protect anything. Attackers ignore it, and listing private paths there tells them where to look.

## What to do when running the site

- Keep the CMS, plugins, and themes updated, and remove plugins you don't use.
- Give admin accounts strong, unique passwords and two-factor login. Put the admin area behind Cloudflare Access or a VPN if you can.
- Verify the site in Google Search Console and Bing Webmaster Tools so you get warnings about hacks and manual actions.
- Watch for files that changed when they shouldn't have, especially `.htaccess`, `wp-config.php`, `index.php`, and server config.
- Watch the number of indexed pages. A sudden jump usually means spam pages.

## How to check for a hack

1. Search `site:yourdomain.com` and look for pages, languages, or topics you didn't create.
2. Use the URL Inspection tool in Search Console to see what Google's crawler gets, and compare it with what you see in a browser.
3. Fetch a page with a crawler user agent and compare the result: `curl -A "Googlebot" https://yourdomain.com/` against `curl https://yourdomain.com/`.
4. Look through server config and recently changed files for rules that check `User-Agent` or `Referer`.
5. Check the database for posts or options containing links you don't recognize.

## How to recover

1. Take a backup of the current state for investigation.
2. Find how the attacker got in and fix it first. Cleaning without fixing the entry point means the spam comes back.
3. Remove the spam pages, files, links, and redirects. Spam pages should return 404 or 410.
4. Change every password and key: admin, database, FTP or SSH, hosting panel, and API keys.
5. Request a review in Search Console once the site is clean.

## Sources

- [Google: #NoHacked 3.0, fixing common hack cases](https://developers.google.com/search/blog/2017/12/nohacked-30-fixing-common-hack-cases)
- [Google Search spam policies](https://developers.google.com/search/docs/essentials/spam-policies)
- [web.dev: Help, I think I've been hacked](https://developers.google.com/web/fundamentals/security/hacked)
