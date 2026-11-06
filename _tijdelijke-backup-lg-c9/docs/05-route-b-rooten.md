# 05 — Route B: rooten + Homebrew Channel

Alleen nodig als je de tv **online** wil houden en toch controle wil. Heb je een extern kastje
en kan de tv offline? Dan is [route A](02-route-a-tv-offline.md) eenvoudiger én sterker.

## Wat je ervoor terugkrijgt

- **Root-shell** op de tv via SSH (of Telnet).
- **Homebrew Channel**: een eigen app-store voor webOS, met opties om telemetrie uit te zetten
  en **"Block system updates"** (firmware-updatechecks volledig uit).
- Eigen opstart-scripts via `/var/lib/webosbrew/init.d`.
- Een **failsafe-modus**. De documentatie: *"In case a device crashes on boot only an emergency
  shell will be exposed via telnet."* Er is dus een vangnet als het misgaat bij het opstarten.

## De methode voor een C9

**`faultmanager-autoroot`** van throwaway96. Werkt op webOS 4.0 en hoger; er is nog geen
gepatchte webOS 4.5-firmware gezien. Zie [01](01-wat-kan-wel-en-niet.md) voor de alternatieven
en wat er niet meer werkt.

---

## Stap 0 — Informatie verzamelen ⛔ *niet overslaan*

1. Op de tv: *Alle instellingen → Ondersteuning → **Over deze tv***. Noteer:
   - exacte modelnaam (bijv. `OLED55C9PLA.AEU`)
   - **softwareversie / firmware** (bijv. `05.30.xx`)
   - webOS-versie, als die vermeld staat
2. Vul die in op **https://cani.rootmy.tv/** — de officiële checker van de community. Die
   vertelt je of jouw firmware kwetsbaar is en welke exploit je nodig hebt.
3. **Zet automatische updates uit** (zie [03](03-niveau-0-instellingen.md), onderdeel C).

> **Stop hier als CanI.RootMy.TV zegt dat je firmware niet kwetsbaar is.** Firmware downgraden
> is een aparte en risicovollere route die niet in dit plan staat. Kies dan
> [route A](02-route-a-tv-offline.md).

## Stap 1 — Voorbereiden

- Laptop op hetzelfde netwerk als de tv.
- Een SSH-client. Windows: `ssh` zit in PowerShell, of gebruik PuTTY. Mac/Linux: Terminal.
- **Quick Start+ uitzetten** op de tv. Staat in de troubleshooting van de exploit; met Quick
  Start+ aan herstart de tv niet echt volledig.
- **Controleer datum en tijd** van de tv. Een foute datum geeft een `errorCode -5`.

## Stap 2 — Developer Mode

1. Maak een gratis account op `developer.lge.com`.
2. Installeer de **Developer Mode**-app uit de LG Content Store.
3. Log in, zet **Dev Mode** aan, zet **Key Server** aan, herstart de tv.
4. Noteer het IP-adres van de tv.

## Stap 3 — Rooten

1. Verbind via SSH met de tv: poort **9922**, gebruiker **`prisoner`**.
2. Download `autoroot.sh` naar een schrijfbare map op de tv, bijvoorbeeld `/tmp`.
3. Uitvoeren:
   ```sh
   sh /tmp/autoroot.sh
   ```
4. Wacht op het bericht **"Payload complete"**.

**Wat normaal is en je niet moet laten schrikken:**
- De exploit veroorzaakt **bewust een segmentation fault**. Dat hoort erbij.
- Staat Homebrew Channel er na "succes" niet op? Herstarten, en controleer dat Quick Start+ uit
  staat.

## Stap 4 — Afronden ⚠️ *dit is de stap die mensen fout doen*

1. **Verwijder de LG Developer Mode-app vóórdat je herstart.** De documentatie is expliciet:
   *"Do not install the LG Developer Mode app while the TV is rooted!"*
2. Open **Homebrew Channel** en zet aan:
   - **"Block system updates"**
   - de telemetrie-opties **uit**
3. **Zet onmiddellijk een SSH-key.** Homebrew Channel gebruikt standaard het wachtwoord
   **`alpine`** totdat je eigen keys hebt ingesteld, en **Telnet is volledig zonder
   authenticatie** (de documentatie zelf zegt: *"Telnet - unauthenticated, use sparingly"*).
   Laat Telnet dus uit staan.

> Dit is geen formaliteit. Een geroote tv met wachtwoord `alpine` of open Telnet is een
> root-shell die openstaat voor iedereen in je netwerk. Zie [07](07-risicos-en-beveiliging.md).

## Stap 5 — Pas daarna de leuke dingen

→ [06 — Apps na root](06-apps-na-root.md)

## Blijft root bestaan na een update?

webOSbrew: *"Theoretically, root can be persistent across updates. But it's not guaranteed."*
Vertrouw er niet op. Blokkeer updates via Homebrew Channel.
