# 03 — Instellingen op de tv (geen hack, nul risico)

Dit is de goedkoopste winst van het hele plan. Doe dit altijd, bij elke route.

## A. Home screen en opstartgedrag

*Algemeen → Systeem → Aanvullende instellingen → **Home-instellingen***

| Instelling | Zet op | Effect |
|---|---|---|
| Home Promotion | **UIT** | haalt de promotiebanners bovenaan het menu weg |
| Content Recommendation | **UIT** | haalt de aanbevolen-content-rijen weg |
| **Power On Screen** | **`Recent Input`** | tv start op je laatste HDMI-ingang in plaats van op het LG-home-screen |

> `Power On Screen = Recent Input` is de belangrijkste instelling in dit hele document.
> Het LG-home-screen is de plek waar de advertenties staan én waar de traagheid zit. Als je
> daar nooit meer komt, is het probleem in de praktijk weg — zonder dat je iets gehackt hebt.

## B. Tracking en toestemmingen

*Alle instellingen → Ondersteuning → Over deze tv → **Gebruikersovereenkomsten***

- Trek alles in wat gaat over **marketing**, **gepersonaliseerde advertenties**, **analytics**
  en **spraakherkenning**. Wat overblijft is de basisovereenkomst die je niet kunt weigeren.
- Zet **Live Plus** uit. Dat is LG's naam voor **ACR** (Automatic Content Recognition): de
  functie die vaststelt wát je kijkt — ook op HDMI, dus ook wat er van je kastje af komt.

> ACR is doorgaans de echte reden waarom mensen zich zorgen maken over een smart-tv. Het
> herkent je beeld en koppelt dat aan een profiel. Dit uitzetten is dus geen detail.

## C. Updates

*Alle instellingen → Ondersteuning → Software-update*

- **Automatisch bijwerken → UIT.**
- Zet ook "Updates toestaan" / NSU-modus uit als die er staat; dat voorkomt prerelease-firmware.

**Waarom:** een nieuwe firmware kan de root-mogelijkheid dichtmaken. Zolang je niet update,
houd je route B open.
**Maar lees ook [07](07-risicos-en-beveiliging.md)** — niet updateren heeft een keerzijde die
je bewust moet afwegen.

## D. Apps opruimen

- Ongebruikte LG-apps kun je **verbergen** in de app-lijst (lang indrukken op de app → verbergen).
- Op retail-firmware kun je ingebouwde apps **niet verwijderen**, alleen verbergen. Dat is wel
  omkeerbaar. Verwijderen vereist root, en zelfs dan is het af te raden omdat je het systeem
  kunt breken.

## E. Controleren of het werkt

Zet de tv uit en weer aan. Je zou nu:
- direct op je HDMI-ingang moeten uitkomen,
- geen promotiebanners meer moeten zien als je wél naar het menu gaat.

## Wat dit níet oplost

- De tv praat nog steeds met LG-servers. Toestemmingen intrekken is een belofte, geen
  technische blokkade. Wil je dat echt dichtzetten, dan heb je [04](04-dns-blokkade.md)
  (DNS-blokkade) of [02](02-route-a-tv-offline.md) (netwerk eraf) nodig.
