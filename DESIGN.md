# DESIGN.md — Konoba Porat (v5)

> **Color handoff: MOZAK (hospitality-web-builder) → OKO (Impeccable). Brand mode.**
> Impeccable izvodi KAKO (OKLCH, kontrast, ritam, motion-zanat), ali NE smije pregaziti karakter palete, keyless mapu, "nikad prazno", SEO/schema.

## Klijent
- **Naziv:** Konoba Porat · **Mjesto:** Vodice (Šibensko-kninska) · **Kategorija:** Restorani i konobe
- **Tel:** +385 22 442 290 · **Web:** nema (🔴 Nema weba) · TripAdvisor/Google: nepoznato → TODO[klijent]
- **Status izrade:** Gotovo (NEPROMIJENJEN — ovo je test) · **Radi terminal:** T2 (NETAKNUT)
- **Arhetip:** **PRESET 1 — Fine Dining / Konoba** (intimno, tipografski elegantno, hrana i atmosfera junaci)

## Anti-clone (postojeće verzije u Notionu — v5 MORA biti drukčiji)
- v1 = Fine dining (tamno) · v2 = Heritage · v3 = Mediteran svjetlo · v4 = Editorial minimal
- **v5 lane = "Porat na plavi sat"** — radna lučica na plavom satu. Niti tamni fine-dining (v1), niti svijetli mediteran (v3): **vapnenasti kamen kao baza + duboko lučko petrol-tirkizno more kao STRUKTURNI tamni ton + mjed lučke lampe kao akcent.** Hero-tip i paleta oba pomaknuti vs v1–v4.

## Odluka o KARAKTERU palete (i zašto — iz imena "Porat" + Vodice)
**"Porat"** (dalmatinski/venecijanski = mala luka, mol, lučica) = radno srce ribarskog mjesta: vezovi, konopi, kamena riva, fenjer nad stolom kad barke utihnu. → **vapnenac rive + duboko lučko more (petrol-tirkiz) + mjed fenjera.** Mirno, maritimno, toplo-hladni kontrast. Namjerno NIJE zemljano (≠ Tovar terakota, ≠ Maslina maslinasto), NIJE olujno-hladno (≠ Reful), NIJE blijeda krema (anti-AI-default): baza je pigmentiran topli vapnenac, dubina je more, toplina dolazi iz mjedi i fotografije svjetla — ne iz bež podloge.

| Token | Hex | Odakle |
|---|---|---|
| `--bg` | `#EDE6D8` | vapnenac vodičke rive na suncu (pigmentiran topli kamen, NE blijeda krema) |
| `--bg-alt` | `#E3DAC8` | suhi kamen / pijesak mula, sekundarne sekcije |
| `--bg-deep` | `#102B2C` | duboko lučko more na plavi sat (petrol-tirkiz near-black — dark sekcije) |
| `--ink` | `#16201F` | mokri kamen u sjeni, maritimni topli near-black (body ≥ 9:1 na `--bg`) |
| `--mid` | `#5C6A64` | osušena alga / vjetrom glodan kamen (čitljiv mid ≥ 4.5:1) |
| `--accent` | `#B0833F` | **mjed lučkog fenjera / okov barke** — primarni brand ton, toplina |
| `--accent-2` | `#8C6529` | tamnija mjed/bronca za hover/aktivno |
| `--sea` | `#2C6063` | lučko tirkizno more po danu — sekundarni akcent (štedljivo, linije/ikone) |

- **Display font:** **Bitter** (slab serif, 400/500/600 + italic) — topao, čvrst, "obojena lučka signalizacija / stari emajl natpis". Karakter radne-ali-ponosne lučice. Svjesno NIJE delikatni didone/garamond (anti-clone vs Maslina/Cormorant, Tovar/EB Garamond, Reful/Bodoni). **Impeccable nota:** Fraunces/Newsreader/Cormorant/DM Sans su na njegovoj reflex-reject listi — zato BITER (off-list) umjesto njih; PRESET 1 default fontovi su namjerno nadjačani po tie-breakeru (OKO pobjeđuje na tipografskom zanatu).
- **Body font:** **Hanken Grotesk** (400/500) — humanistički grotesk, off reflex-reject liste, izvrsna čitljivost. Par je na osi kontrasta (slab serif + grotesk), ne dva slična sansa.
- **Hero-tip:** **Split hero** (visoka fotografija mula/barki na plavi sat ∥ tagline na vapnencu). Anti-clone: drukčiji od fullbleed-dark (v1) i fullbleed-svjetlo (v3). Mobile: slika gore, tagline ispod.

## Set potpisnih interakcija (PRESET 1 — suzdržano, unutar perf budžeta)
1. **Word reveal** (vanilla SplitText) na H2 — stagger 0.08, ne na bodyju.
2. **Hero breathing zoom** (scale 1.05→1.0 na scroll, scrub) — jedan scrub.
3. **Scroll fade-reveal** (fade + 20px Y, ne-scrub onEnter) na sekcijama.
4. **Galerija — "plavi sat" grade** (NE topli sepia kao Tovar): blago hladnije večernje `sepia(0.10) contrast(1.06) saturate(0.92)` + hover lift.
5. **Reservation slide-in panel** (desna ploča, GSAP xPercent).
- NE: WebGL, magnetic, scramble, horizontal scroll, kinetička tipografija, **custom cursor s efektima** (restraint za P1 konobu).

## Dekorativni potpis (individualiziran — NE generički Impeccable default, NE ponavljanje)
- **SVG "mooring line / konop" divider** — tanka ručno-vođena užad-linija s malim čvorom/alkom između sekcija (motiv veza za mol). Jedinstveno za Porat; NE isti divider kao drugi buildovi.
- **Logo-lockup mikro-ornament:** mala mjedena alka/halka (mooring ring) uz naziv.
- **BEZ custom cursora** (svjesno — restraint P1; ujedno garantira da se ne dijeli generički cursor-potpis s drugim stranicama).

## Tvrda pravila (Impeccable NE smije pregaziti)
- **Keyless mapa:** Vodice lokacija ISKLJUČIVO kao keyless `<iframe ...output=embed>`. Nikad Maps JS API / `key=`.
- **Bez tajni:** nijedan ključ/token/secret u HTML/JS/CSS/atributima/komentarima. S1-CHECK grep prije commita.
- **Nikad prazno:** sav copy konkretan, na-brend (Vodice, lučica, riba s kanala). Nepoznato (godina, chef, obitelj) → uvjerljiv tekst + `TODO[klijent]`, nikad lorem/prazna sekcija.
- **SEO/schema:** jedan H1, semantička hijerarhija, lokacija u naslovima/kontaktu, alt tekstovi, `Restaurant` JSON-LD, OG tagovi, canonical.
- **Fotografije:** privremene (stock), provjereno da nisu sadržajno/geografski krive; klijent mijenja stvarnima → `TODO[klijent]`.
