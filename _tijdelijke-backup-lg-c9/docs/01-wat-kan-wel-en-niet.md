# 01 — Wat kan wel en niet

## De vraag

"Ik wil dat mijn LG OLED55C9PLA op custom software/OS gaat draaien."

## Het eerlijke antwoord

**Een ander besturingssysteem op de tv zetten kan niet.**

- Er bestaat **geen project** dat webOS vervangt door Android, LibreELEC of een andere
  Linux-distributie op LG-tv's. Bij het onderzoek is daar niets van gevonden.
- De bootloader van de tv is niet te ontgrendelen en de firmware is ondertekend. Er is dus geen
  "flash een ander OS"-route zoals bij een telefoon of een Raspberry Pi.
- De community rond LG-tv's (**webOSbrew**) richt zich expliciet op het *modden van* webOS,
  niet op het vervangen ervan. Dat is geen toeval maar een gevolg van bovenstaande.

## Wat de YouTube-video's dan wél tonen

Bijna altijd één van deze twee dingen:

1. **Rooten + Homebrew Channel.** De tv blijft webOS draaien, maar je krijgt root-rechten, een
   SSH-shell, een eigen app-store, en de mogelijkheid telemetrie en firmware-updates te
   blokkeren. Dit is wat mensen bedoelen met "custom firmware" op een LG.
2. **Debloaten / een andere launcher.** Advertenties en LG-apps verbergen, en soms een
   vervangend home screen. Werkt grotendeels alleen op nieuwere webOS-versies — zie
   [06](06-apps-na-root.md).

Als je een specifieke video hebt, kijk naar welke van deze twee het is. Dat bepaalt of de
video op jouw C9 van toepassing is.

## Waarom webOS 4.5 een gunstige uitgangspositie is

De C9 is een 2019-model en kwam met **webOS 4.5**. De aanbevolen exploit (`faultmanager`) werkt
op webOS 4.0 en hoger. De webOSbrew-site meldt:

> "Works on webOS 4.0 and up, including webOS 9." — en: "As of January 2025, no patched
> firmware exists."

En de auteur van de exploit meldt (stand 2025-08-24) dat webOS 5, 6, 7 en 9 inmiddels
grotendeels zijn gepatcht, maar dat hij **nog geen gepatchte webOS 4.5-firmware heeft gezien**.
Oudere toestellen zijn hier dus beter af dan nieuwe.

> ⚠️ Dit is geen garantie voor jouw specifieke firmware. Verifieer hem op
> **https://cani.rootmy.tv/** — zie [05](05-route-b-rooten.md), stap 0.

## Welke exploits bestaan er, en wat werkt nog

| Methode | Werkt op | Status |
|---|---|---|
| **`faultmanager`** | webOS 4.0 en hoger | ✅ aanbevolen; geen gepatchte 4.5-firmware gezien |
| **DejaVuln** | webOS 3.5 en hoger | ⚠️ patches worden uitgerold, nieuwste modellen eerst |
| RootMyTV | webOS 3–6 | ❌ gepatcht in 2022 |
| crashd | webOS 4+ | ❌ gepatcht april 2024 |
| WTA | — | ❌ gepatcht |
| GetMeNow | webOS 1–3 | ❌ werkt niet na Dev Mode-updates van begin 2024 |
| **NVM** (tv openschroeven) | hardware | 🛑 **niet doen** |

Over NVM waarschuwt webOSbrew letterlijk:

> "You may **damage your TV permanently** without proper knowledge."

→ Bronnen in [08](08-bronnen.md).
