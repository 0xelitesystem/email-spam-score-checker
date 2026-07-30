# email-spam-score-checker

A browser tool that scores your email content against 40 SpamAssassin-style rules locally. No upload, no API, no tracking.

**Live demo:** https://0xelitesystem.github.io/email-spam-score-checker/

Single HTML file. All checks run in the browser. Paste subject, from-address, and body. See a 0-to-20+ score broken down by which rules fired.

## What it does

Paste:
- Subject line
- From address (or display name)
- Body (plain text or HTML)

The tool runs 40 content checks and shows:
- Total score with verdict (deliver / risky / spam)
- Every rule that fired, with point weight and short explanation
- A preview of how the email looks in an inbox row
- The full list of all 40 rules so you can audit the logic

## Rules included

40 checks across 4 categories:

| Category | Examples |
|---|---|
| Subject heuristics (9) | All caps, multiple exclamations, dollar signs, spam trigger words, fake Re:/Fwd:, too short, too long, emoji-heavy, number-heavy |
| Body heuristics (14) | All-caps lines, repeated spam triggers, excessive punctuation, multiple dollar amounts, URL shorteners, money-back guarantees, urgency phrasing, all-caps blocks |
| Structure (10) | Image-only body, link-to-text ratio, hidden text, font-size abuse, color-on-color, table-based layout, missing plain-text alternative |
| Reputation proxies (7) | Generic from-address, no-reply pattern, domain mismatch in display name, free-mail sender claiming business, bracket spam in display name |

Point weights match SpamAssassin defaults where they exist. Custom rules use weights calibrated against a small public corpus of confirmed spam.

## Scoring

| Score | Verdict | Meaning |
|---|---|---|
| 0 to 4 | Deliver | Likely lands in the inbox on most filters |
| 5 to 9 | Risky | Some filters will route to promotions or spam; review |
| 10 or more | Spam | High probability of being filtered |

## What this is not

This is a content-side check. It does not test:
- DKIM, SPF, DMARC authentication (those require sending a real message)
- Sender reputation (built up over months by recipient engagement)
- Recipient-specific filters (Gmail, Outlook, and corporate filters all learn from individual behavior)
- Bayesian content models (those need access to the recipient's spam folder history)

A 0 score does not guarantee inbox placement. A high score does not guarantee filtering. The tool catches content-side problems before you hit send, which is the cheapest thing to fix.

## Why not just use mail-tester.com

That service requires you to actually send the email to a test address, then it scores the full envelope including auth headers. Useful, but slow and requires real delivery. This tool runs offline in 50ms and catches the 80% of issues that are content-related.

Use both. This one first, mail-tester for the final send.

## Privacy

Nothing transmitted. No analytics, no fonts, no external scripts. The HTML file is self-contained. View source to verify.

## Build

No build. Open `index.html` directly or deploy via GitHub Pages.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT.

## Related

- [legal-pages-starter](https://github.com/0xelitesystem/legal-pages-starter) - terms and privacy templates that often go in transactional emails
- [solo-saas-launch-checklist](https://github.com/0xelitesystem/solo-saas-launch-checklist) - includes email deliverability items
- [ai-product-disclaimers](https://github.com/0xelitesystem/ai-product-disclaimers) - disclaimers for AI-product transactional email
- [api-security-audit-checklist](https://github.com/0xelitesystem/api-security-audit-checklist) - covers API-driven email send paths
- [webhook-inspector](https://github.com/0xelitesystem/webhook-inspector) - for debugging email-service webhooks
