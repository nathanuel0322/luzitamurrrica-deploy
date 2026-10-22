# Luzitamurrrica

Single-file study app (`citizenship-study.html`) for the 2025 USCIS civics test (128 questions). A personal gift from Nathanuel to his girlfriend, who studies mostly on her phone. Live at https://luzitamurrrica.nateshomelab.top.

## Structure
- Everything lives in `citizenship-study.html`: CSS in `<style>`, markup, then one `<script>` (question data in `RAW`, state in `localStorage`).
- No build step, no dependencies besides Google Fonts (Fraunces, Nunito).
- CSS is layered: base styles, then a "Readability pass" (large fonts), then a "Made-with-love pass" (pink theme). Later blocks override earlier ones; extend the last block rather than editing the base.
- Keep `<!DOCTYPE html>`, `<meta charset>`, and `<meta name="viewport">` at the top of the file. Without them phones render a shrunken desktop layout and emoji break.

## Tone and content rules
- Warm, romantic, hers. Pink light theme, wine/plum dark theme. He loves the current design.
- Footer is signed "— from your tall king 👑". Keep it.
- The header greeting rotates through her nicknames (`PET_NAMES` in the script).
- Write in his voice: "my beautiful girl". Never "mi amor" or "mi vida".
- Settings answers are baked into `DEFAULT_SETTINGS` as permanent NYC defaults (Schumer/Gillibrand, Rep. Gregory W. Meeks, Gov. Hochul, Albany). Blank fields refill from defaults on load.
- Office holders (President, VP, Speaker, Chief Justice) need re-checking against uscis.gov before her interview.
- Civics question data in `RAW` must not change unless USCIS changes the test.

## Deploy
1. Commit and push to `main` of `nathanuel0322/luzitamurrrica-deploy`.
2. In the Proxmox web UI (https://192.168.1.89:8006) open LXC 101 `cloudflare-tunnel` → Console and run:
   `curl -sL https://raw.githubusercontent.com/nathanuel0322/luzitamurrrica-deploy/<COMMIT_SHA>/citizenship-study.html -o /var/www/html/index.html`
3. Verify: `md5sum /var/www/html/index.html` must equal local `md5 -q citizenship-study.html` and `curl -s https://luzitamurrrica.nateshomelab.top/ | md5`.

Use the commit-SHA URL, not `main`: the raw CDN caches `main` for about 5 minutes and serves stale files. Never hand-retype or base64 files into the console. Always go through GitHub then `curl`.
