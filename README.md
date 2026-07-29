# Klus-Winkel — klus-winkel.nl

Statische website (platte HTML/CSS, geen build-stap nodig). Klaar om te hosten op Cloudflare Pages via GitHub.

## Structuur

- `index.html`, `over.html`, `redactie.html`, `contact.html`, `privacybeleid.html`, `cookiebeleid.html`
- `klussen/` — overzicht + 3 pagina's: boren, kleine klussen laten uitvoeren, elektra & elektrotechniek
- `nieuws/` — overzicht + 3 nieuwsartikelen
- `assets/css/style.css`, `assets/img/` — stijl en illustraties
- `.github/workflows/deploy.yml` — GitHub Actions workflow die bij elke push naar `main` automatisch naar Cloudflare Pages deployt

## Eenmalig instellen

1. **GitHub repo**: maak een lege repository aan (bijv. `klus-winkel`) en push deze map naar de `main`-branch.
2. **Cloudflare Pages project**: maak in het Cloudflare dashboard een Pages-project aan met de naam `klus-winkel` (moet overeenkomen met `projectName` in `.github/workflows/deploy.yml`).
3. **GitHub secrets**: voeg in de repo-instellingen (Settings → Secrets and variables → Actions) twee secrets toe:
   - `CLOUDFLARE_API_TOKEN` — een Cloudflare API-token met de rechten "Cloudflare Pages: Edit"
   - `CLOUDFLARE_ACCOUNT_ID` — het Cloudflare account-ID
4. **Custom domain**: koppel `klus-winkel.nl` aan het Cloudflare Pages-project via het dashboard (Pages-project → Custom domains). Zorg dat de domeinnaam als zone in hetzelfde Cloudflare-account staat, of wijzig de nameservers naar Cloudflare.
5. Push naar `main` → de GitHub Action deployt automatisch.

## Analytics (optioneel)

De privacy- en cookiepagina's gaan uit van Cloudflare Web Analytics (cookieloos). Voeg dit toe via Cloudflare dashboard → Pages-project → Analytics → "Enable Web Analytics", dit voegt automatisch een script toe zonder dat de code hier hoeft te wijzigen.

## Google Search Console

1. Voeg het domein toe als property in Google Search Console.
2. Verifieer eigendom via de DNS-TXT-record methode (aan te maken bij de DNS-instellingen van de zone in Cloudflare).
3. Dien na verificatie de sitemap in: `https://klus-winkel.nl/sitemap.xml`.
4. Vraag via "URL-inspectie" indexering van de homepage aan.

## Let op: linkprofiel boren-pagina

`klussen/boren.html` bevat op verzoek 21 dofollow-links naar boorkopen.nl, met de volledige URL als ankertekst, verspreid over doorlopende uitleg per boortype. Dit is een herkenbaar patroon voor zoekmachines (exact-match ankertekst, één doeldomein, geen variatie) en kan door Google als linkscheme worden geclassificeerd, met risico op een handmatige actie voor zowel deze site als boorkopen.nl. Dit is bewust zo uitgevoerd op uitdrukkelijk verzoek; monitor de Google Search Console van beide domeinen op meldingen over onnatuurlijke links.
