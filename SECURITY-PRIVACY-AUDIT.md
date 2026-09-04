# ENGL C1002 Learning Lab — Security and Privacy Hardening

This package received a security/privacy hardening pass focused on data minimization and reducing the chance that future edits expose user information or create browser-side injection problems.

## Changes made

- Added a site-wide `Referrer-Policy` via `<meta name="referrer" content="no-referrer">` to all HTML pages.
- Added a restrictive Content Security Policy suitable for the site's static, inline-script architecture.
- Added `noreferrer` alongside `noopener` for links that open in a new tab.
- Added `referrerpolicy="no-referrer"` to all Canvas iframe snippets displayed and copied from `teachers.html`.
- Hardened `reflection.html` so unexpected `lab=` URL parameter values cannot resolve inherited JavaScript object properties.
- Removed all uses of `innerHTML`; dynamic content is now created using `textContent`, `replaceChildren()`, and DOM nodes.
- Updated `privacy.html` to distinguish the Learning Lab's own behavior from hosting/email services and to explain the no-referrer protection.
- Added a Security and Privacy maintenance note to `README.md`.

## Verification performed

- HTML pages checked: 41
- Content Security Policy present: 41/41
- Referrer meta policy present: 41/41
- Remaining `innerHTML` occurrences: 0
- Inline JavaScript blocks syntax-checked with Node: 39
- JavaScript syntax errors: 0
- Broken local file references: 0
- New-tab links missing `noopener noreferrer`: 0
- Network API calls (`fetch`, XHR, WebSocket, sendBeacon): 0
- Browser storage (`localStorage`, `sessionStorage`, IndexedDB, cookies): 0
- HTML form tags: 0
- Live iframe embeds in the student site: 0

## Residual considerations

- GitHub Pages, like any web host, may process ordinary request/security logs under its own policies.
- A public contact email remains intentionally visible on the site's Accessibility/License pages. Change it if that address should not be public.
- Existing Canvas pages that already contain an older copied iframe snippet will not automatically gain `referrerpolicy="no-referrer"`; instructors can replace the old embed snippet if they want that additional hardening.
- The CSP currently permits inline scripts/styles (`'unsafe-inline'`) because the site's architecture embeds JavaScript and CSS directly in HTML files. A future refactor to local `.js`/`.css` files could support a stricter CSP.
