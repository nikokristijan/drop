# drop – teaser stranica

Jedna statična stranica: nebo, logo, **start** tipka → XP prozor → upis e-maila.
Nema build koraka, nema ovisnosti. Cijela stranica je `index.html` + `assets/`.

```
index.html          stranica (CSS i JS su unutra)
assets/fonts/       Libre Franklin + DM Mono (self-hosted, OFL licenca)
assets/favicon.svg  monogram iz naljepnica
assets/og.jpg       slika za dijeljenje linka (Instagram bio, WhatsApp...)
```

## 1. Spoji prikupljanje e-mailova (obavezno prije objave)

Dok to ne napraviš, stranica radi u **demo načinu**: adresa se sprema samo u
browser posjetitelja i nigdje se ne šalje.

Otvori `index.html`, nađi na početku `<script>` bloka:

```js
const CONFIG = { endpoint: '' };
```

i upiši URL svog servisa. Stranica šalje `POST` s JSON-om
`{ "email": "...", "source": "drop.hr", "ts": "2026-..." }`.

Najbrže opcije:

- **Formspree** (free): napravi formu, kopiraj `https://formspree.io/f/xxxxxxx`.
  Mailovi stižu u inbox i u tablicu, export u CSV.
- **Buttondown / Mailchimp / Brevo**: koristi njihov API ili form endpoint ako
  želiš odmah slati newsletter s iste liste.
- **Google Apps Script** koji upisuje red u Google Sheet (besplatno, 15 linija koda).

Ako endpoint ne prihvaća JSON (neki Mailchimp URL-ovi), reci i prilagodit ćemo `send()`.

## 2. Objava

Bilo koji statični hosting: Netlify / Vercel / Cloudflare Pages (povuci mapu u
dashboard), GitHub Pages, ili FTP na postojeći hosting. Postavi domenu i
provjeri da `index.html` leži u rootu.

Nakon što znaš domenu, u `<head>` zamijeni `https://drop.hr/assets/og.jpg`
pravim URL-om (scraperi traže apsolutni link).

## 3. Što možeš mijenjati

- **Tekstovi**: u `index.html` traži `Prvi drop stiže uskoro.` (naslov prozora)
  i objekt `copy` u JS-u (naslovi stanja "učitavanje" i "gotovo").
- **Boje**: tokeni na vrhu `<style>` (`--sky`, `--hill`, `--sun`, ...), uzeti iz naljepnica.
- **Oznake u kutovima** (`@drop.hr`, `Nº 001`, `Limited edition`, `2026`): klase `.tag--*`.
- **Privola**: tekst ispod polja ("Koristimo ga samo za obavijest o dropu.") prilagodi
  svojoj politici privatnosti (GDPR), po potrebi dodaj link.

Stranica poštuje `prefers-reduced-motion` (bez animacija, stickeri se odmah slože).
