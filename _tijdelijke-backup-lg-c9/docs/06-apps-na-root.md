# 06 — Apps na root: wat werkt wel en niet op een C9

## `youtube-webos` — advertentievrije YouTube ✅

Het meest waardevolle resultaat van dit hele traject, en **root is er niet eens voor nodig**
(kan ook via Developer Mode; met Homebrew Channel is het wel permanent en gemakkelijker).

Features volgens de documentatie:
- **advertenties blokkeren**
- **SponsorBlock**-integratie (sponsorsegmenten automatisch overslaan)
- Shorts verwijderen, hoogste videokwaliteit afdwingen, audio-only-modus (blauwe knop),
  klok op het scherm, YouTube-logo weg, eindscreens weg, accountkiezer overslaan
- Autostart

**Let op:** je moet de **officiële YouTube-app eerst verwijderen**.
**Configuratie:** de **groene knop** op je remote opent het instellingenscherm.

Installeren: via Homebrew Channel (staat in de officiële repository), via Device Manager met
een `.ipk` van de Releases-pagina, of via de webOS CLI.

## `Luma` — alternatieve launcher ⚠️ beperkt op een C9

Een home screen in Apple TV-stijl voor geroote tv's. De C9 staat in de compatibiliteitslijst
onder webOS 4, en Luma *"should start on any TV running webOS 4 or newer"*.

**Maar de "takeover"-functie — waarmee Luma de Home-knop echt overneemt — wordt volgens de
documentatie alleen ondersteund op webOS 5, 6, 25 en 26.** Op webOS 4 blijft dus naar
verwachting alleen de autostart-variant over, en die herkent de Home-knop **niet**.

> *Onverifieerd voor exact de C9.* De compatibiliteitslijst markeert takeover per model; C8 en
> UM7450 staan expliciet op ❌. Zie [09](09-onverifieerd.md).

Waarschuwingen uit de documentatie, als je het toch probeert:
- Zet Home-knop-mapping in LG Input Hook uit vóór je takeover aanzet.
- Zet autostart uit vóór je takeover aanzet of Luma verwijdert.
- Verwijder je Luma zonder eerst takeover uit te zetten, dan blijft er een boot-hook achter
  die een fout logt omdat Luma er niet meer is.

## Debloat-tooling ⚠️ grotendeels niet voor webOS 4

Het gros van de populaire "debloat"- en vervangende-home-screen-projecten richt zich op
**webOS 5 en nieuwer**. Meerdere stoppen expliciet op webOS 4, omdat daar geen systemd op zit
en een oude Node.js-versie. Eén project meldt dat zijn vervangende home screen alleen op
webOS 7, 9 en 10 werkt.

**Conclusie voor de C9:** reken er niet op dat je het home screen echt kunt vervangen. De
praktische oplossing blijft `Power On Screen = Recent Input` uit [03](03-niveau-0-instellingen.md).

## 🛑 Draai geen willekeurige scripts als root op je tv

Bij het onderzoek kwamen diverse GitHub-repo's langs met "LG debloat toolkit" in de naam, van
accounts zonder enige staat van dienst. Die krijgen **root-toegang tot je tv** als je ze
uitvoert.

Blijf bij de projecten met reputatie in deze community:
- **webosbrew** (Homebrew Channel, youtube-webos)
- **throwaway96** (faultmanager-autoroot, dejavuln-autoroot)

Dit is geen paranoia maar hetzelfde principe als geen onbekende `.exe` met
administratorrechten draaien. Op een tv is het erger, want je merkt niet wat er gebeurt.

## Overige homebrew die vaak genoemd wordt

- **Piccap / Hyperion** — ambilight op basis van het tv-beeld. Vaak de echte reden waarom
  mensen rooten.
- **Device Manager** — apps installeren en beheren.
- **LG Input Hook** — remote-knoppen herkennen. Documentatie: *"Test op een spare button first."*
