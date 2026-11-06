# 02 — Route A: de tv van het netwerk af *(aanbevolen)*

## Waarom dit voor jou de beste route is

Normaal is "haal de tv van het netwerk" een zwaar advies, omdat je dan je streaming-apps
kwijt bent. **Maar je hebt al een extern kastje.** Daarmee verlies je vrijwel niets en los je
in één handeling alles op:

| Je klacht | Wordt dit |
|---|---|
| Privacy / tracking | **Volledig weg.** Niet geblokkeerd — technisch onmogelijk. Geen DNS-lek, geen hardcoded resolver die eromheen gaat, niets. |
| Advertenties en home screen | **Weg.** Het menu kan geen advertenties ophalen, en je komt er met `Recent Input` niet eens meer. |
| Traagheid | **Beter.** Een deel van de haperingen in webOS komt doordat de tv wacht op LG-servers die niet antwoorden. |
| *(bonus)* Beveiliging | **Aanvalsoppervlak verdwijnt.** Zie [07](07-risicos-en-beveiliging.md) — webOS heeft een terugkerende stroom van lekken die root geven vanaf het lokale netwerk. |

En: **nul risico, vijf minuten werk, op elk moment terug te draaien.**

## Wat je opgeeft

- **AirPlay naar de tv** en de ingebouwde apps (Netflix, YouTube, Disney+ enz.). Die horen
  vanaf nu bij je kastje.
- **Firmware-updates.** Dat is bij deze route geen nadeel maar een voordeel: zonder netwerk
  is een lek in webOS niet van buiten te bereiken.
- **Smart-home-integratie met de tv zelf.** Draai je Home Assistant en wil je de tv aan/uit
  kunnen zetten of de ingang schakelen? Dan heb je de tv wél op het netwerk nodig.
  → In dat geval: route A vervalt, ga naar [04](04-dns-blokkade.md) + [05](05-route-b-rooten.md).

## Stappen

1. **Eerst de instellingen uit [03](03-niveau-0-instellingen.md).** Doe dit vóór je het netwerk
   eraf haalt, anders kom je er lastiger bij.
   - Belangrijkst: **Power On Screen → `Recent Input`**.
2. **Netwerkverbinding verbreken.**
   - *Alle instellingen → Verbinding → Wifi-verbinding* → verbinding vergeten / verbreken.
   - LAN-kabel eruit, als die erin zat.
3. **HDMI-CEC aanzetten** zodat je kastje de tv kan aan/uitzetten en de ingang kan kiezen.
   - *Alle instellingen → Algemeen → **HDMI-apparaatdetectie / SIMPLINK** → AAN*.
   - Hiermee hoef je nooit meer naar het LG-menu: kastje aan → tv aan → juiste ingang.
4. **Controleren.** Zet de tv uit en weer aan. Je moet nu direct op het beeld van je kastje
   uitkomen, zonder LG-home-screen.
5. *(Optioneel, extra zekerheid)* **Blokkeer het MAC-adres van de tv op je router.** Dan kan
   de tv ook niet per ongeluk terugkeren op het netwerk na een reset of door iemand anders
   in huis. Het MAC-adres staat onder *Alle instellingen → Ondersteuning → Over deze tv*.

## Terugdraaien

Wifi opnieuw verbinden. Klaar. Er is niets aan het systeem gewijzigd.

## Wat je hierna nog zou kunnen willen

- **Advertentieblokkade voor je kastje.** Je privacyprobleem verschuift nu naar het kastje.
  Dat is een eigen traject, maar een Pi-hole of AdGuard Home in je netwerk helpt daar net zo
  goed — zie [04](04-dns-blokkade.md), dezelfde aanpak, andere domeinen.
- **Rooten alsnog**, puur voor de leuke dingen (ambilight via Piccap bijvoorbeeld). Dat kan
  altijd nog, zolang je de firmware niet laat updaten.
