# LG OLED55C9PLA — webOS onder eigen controle

Documentatie en werkplan om een **LG OLED55C9PLA** (2019, webOS 4.5) minder "smart" te maken:
geen tracking, geen advertenties, een snellere interface.

> **Status:** plan + onderzoek afgerond. Nog niets uitgevoerd op de tv.
> **Eigenaar:** Tom Kuster · **Laatst bijgewerkt:** 2026-11-06

---

## De korte versie

**Wat niet kan:** webOS vervangen door Android of Linux. Er bestaat geen enkel project dat dat
doet op een LG-tv. De bootloader is niet te ontgrendelen en de firmware is ondertekend.

**Wat de YouTube-video's wél laten zien:** webOS *rooten* en de **Homebrew Channel** installeren.
De tv blijft webOS draaien, maar je krijgt root, SSH, eigen apps, telemetrie uit en de
mogelijkheid firmware-updates permanent te blokkeren.

**Wat voor jou het beste werkt:** je hebt al een extern kastje. Daarmee wordt de simpelste route
ook de beste route — zie hieronder.

---

## Twee routes

### Route A — tv van het netwerk af *(aanbevolen)*
De tv wordt een dom OLED-paneel. Je kastje doet al het slimme werk.

- ✅ Tracking volledig weg. Niet geblokkeerd, maar onmogelijk.
- ✅ Advertenties in het menu weg.
- ✅ Interface sneller (geen wachten op LG-servers).
- ✅ Geen aanvalsoppervlak meer in je netwerk — zie [docs/07](docs/07-risicos-en-beveiliging.md), dit is een serieus punt.
- ✅ Nul risico, in vijf minuten gedaan, altijd omkeerbaar.
- ❌ Geen AirPlay naar de tv, geen ingebouwde apps, geen firmware-updates.

→ **[docs/02-route-a-tv-offline.md](docs/02-route-a-tv-offline.md)**

### Route B — rooten + Homebrew Channel
Alleen nodig als je de tv per se online wil houden.

- ✅ Telemetrie uit, updates blokkeren, eigen apps, advertentievrije YouTube.
- ❌ Klein maar reëel risico, meer werk, en je zit vast aan oude firmware met bekende lekken.

→ **[docs/05-route-b-rooten.md](docs/05-route-b-rooten.md)**

---

## Doe dit in elk geval, bij beide routes

Drie instellingen op de tv, geen hack nodig, grootste effect van alles:

| Instelling | Waarde | Waarom |
|---|---|---|
| Home Promotion | **UIT** | haalt de promotiebanners uit het menu |
| Content Recommendation | **UIT** | haalt aanbevolen content weg |
| **Power On Screen** | **`Recent Input`** | tv start direct op je kastje, slaat het LG-home-screen helemaal over |

→ **[docs/03-niveau-0-instellingen.md](docs/03-niveau-0-instellingen.md)**

---

## Inhoud

| Document | Waarover |
|---|---|
| [01 — Wat kan wel en niet](docs/01-wat-kan-wel-en-niet.md) | de reality check, met bronnen |
| [02 — Route A: tv offline](docs/02-route-a-tv-offline.md) | aanbevolen route, stap voor stap |
| [03 — Instellingen op de tv](docs/03-niveau-0-instellingen.md) | zonder hack, nul risico |
| [04 — DNS-blokkade](docs/04-dns-blokkade.md) | Pi-hole / AdGuard Home, inclusief de router-valkuil |
| [05 — Route B: rooten](docs/05-route-b-rooten.md) | faultmanager + Homebrew Channel |
| [06 — Apps na root](docs/06-apps-na-root.md) | youtube-webos, Luma, wat wel/niet werkt op webOS 4 |
| [07 — Risico's en beveiliging](docs/07-risicos-en-beveiliging.md) | inclusief het update-dilemma |
| [08 — Bronnen](docs/08-bronnen.md) | alles waarop dit plan is gebaseerd |
| [09 — Onverifieerd](docs/09-onverifieerd.md) | wat ik níet heb kunnen vaststellen |
| [CHECKLIST.md](CHECKLIST.md) | afvinklijst om mee aan de slag te gaan |
| [dns/lg-blocklist.txt](dns/lg-blocklist.txt) | kant-en-klare domeinenlijst |

---

## Eén ding is tijdkritisch

**Zet automatische software-updates nu uit op de tv.** Als LG een gepatchte firmware voor de C9
uitbrengt en je tv haalt die binnen, verdwijnt de root-mogelijkheid mogelijk voorgoed. Dit kost
je niets en houdt route B open, ook als je uiteindelijk voor route A kiest.

*(Lees eerst [docs/07](docs/07-risicos-en-beveiliging.md) — er zit een keerzijde aan.)*
