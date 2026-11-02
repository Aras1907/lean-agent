# Privacy checklist

Personal data is anything that can identify a person: names, emails, phone numbers, IP addresses, device IDs, location, and anything linked to them. Laws like GDPR in the EU and CCPA in California set rules for it. This checklist is not legal advice. When a project handles health, payment, or children's data, tell the user to get a proper legal review.

## Collect less

- Only collect data the feature needs right now. If you can't say what a field is used for, don't add it.
- Prefer less detail: a birth year instead of a full birth date, a city instead of an exact location.
- Don't keep raw IP addresses longer than needed. Shorten or hash them for analytics.

## Keep it short

- Set how long each kind of data is kept, and add a job that deletes or anonymizes it after that.
- Remember that backups, logs, caches, and search indexes hold copies too.
- Build a real delete path. When a user deletes their account, their data should be removed or anonymized everywhere.
- Let users download their data if the product is likely to fall under GDPR.

## Protect what you keep

- Use HTTPS everywhere.
- Encrypt sensitive fields in the database, and use the database or cloud provider's encryption for everything else.
- Limit who and what can read personal data. Admin tools should log who looked at what.
- Never put personal data in URLs. URLs end up in logs, browser history, and `Referer` headers sent to other sites.
- Don't use production data in development or tests. Use fake or anonymized data.

## Logs and errors

- Don't log personal data. If you must, mask it, for example `j***@example.com`.
- Remove personal data from error reports before sending them to services like Sentry.

## Third parties

- Every analytics tool, ad script, chat widget, and font or CDN request sends visitor data to someone else. Add them only when the user asks, and list them so the user knows.
- In regions that require it, load tracking scripts only after the visitor consents. Make declining as easy as accepting.
- Prefer privacy-friendly analytics that don't use cookies or track people across sites.
- Don't send user data to AI APIs or other outside services without the user knowing, and check that the provider's terms allow it.

## Cookies

- Set only the cookies the site needs.
- Session cookies get `HttpOnly`, `Secure`, and `SameSite`.
- Don't put personal data in cookies or `localStorage` unless it's needed, and never put secrets in `localStorage`.

## Tell the user

When you finish, say what personal data the code collects, where it is stored, who it is shared with, and how long it is kept. If the project has no privacy policy and collects personal data, point that out.
