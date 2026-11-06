# Plan: LG OLED55C9PLA minder "smart", meer onder eigen controle

**Datum:** 2026-11-06
**Toestel:** LG OLED55C9PLA (2019-model, geleverd met webOS 4.5)
**Doel:** zorgen over bepaalde webOS-functies wegnemen

---

## 1. Eerst de verwachting bijstellen (belangrijk)

Je vraag was "een custom software/OS erop zetten". Dat kan in de letterlijke zin **niet**.

- Er bestaat **geen project dat webOS vervangt** door Android, LibreELEC of een andere Linux-distributie op LG-tv's. Ik heb daar bij het uitzoeken niets van gevonden, en de bekende community (webOSbrew) richt zich expliciet op het *modden van* webOS, niet op het vervangen ervan.
- De bootloader van de tv is niet ontgrendelbaar en de firmware is ondertekend. Er is dus geen "flash maar een ander OS"-route zoals bij een telefoon.
- **Wat de mensen op YouTube doen is bijna altijd iets anders:** ze *rooten* webOS en zetten de **Homebrew Channel** erop. De tv blijft webOS draaien, maar jij krijgt root-rechten, SSH, eigen apps, en de mogelijkheid om telemetrie en updates te blokkeren. Dat is het echte uitgangspunt.

> *Niet gevonden / onverifieerd:* een werkende custom-OS-port voor de C9. Als je een specifieke YouTube-video hebt, stuur me de link — dan kijk ik of het inderdaad root + Homebrew is of iets anders.

---

## 2. Wat er wél kan — drie niveaus

### Niveau 0 — Nul risico (begin hier, altijd)
Geen hack nodig, niets kan stuk.

1. **In de tv-instellingen uitzetten:** ACR / "Live Plus", gepersonaliseerde advertenties, en de gebruikersovereenkomsten voor marketing/analytics intrekken (Alle instellingen → Algemeen → Over deze tv → Gebruikersovereenkomsten).
2. **Automatische updates uit** (zie waarschuwing in §4: een update kan de root-mogelijkheid dichtmaken).
3. **DNS-blokkade in je netwerk** via Pi-hole of AdGuard Home. Veelgenoemde LG-domeinen: `lgsmartad.com`, `lgtvsdp.com`, `lgappstv.com`, `ngfts.lge.com`, `lgad.cjpowercast.com`, `alphonso.tv`.
   - Let op twee valkuilen: (a) de tv kan een **hardcoded DNS** gebruiken en je Pi-hole omzeilen — dan moet je op je router uitgaand poort 53 (en 853 voor DNS-over-TLS) blokkeren behalve naar je Pi-hole; (b) te breed blokkeren kan legitieme functies breken.
   - Werkwijze: eerst blokkeren, dan in het Pi-hole/AdGuard-log kijken wat de tv écht aanroept. Dat is meteen je bewijs.
4. **De radicale variant:** haal de tv helemaal van het netwerk (geen wifi, geen LAN) en hang er een extern kastje aan (Apple TV, Nvidia Shield, mini-pc met LibreELEC). De tv wordt dan een "dom" paneel met een uitstekend OLED-beeld. Dit lost privacy, advertenties, trage UI en verdwijnende app-ondersteuning in één keer op — zonder enig risico. Je verliest: ingebouwde apps, AirPlay en firmware-updates.

**Advies:** niveau 0 lost voor veel mensen 80% van de klacht op. Doe dit eerst, voordat je gaat rooten.

### Niveau 1 — Rooten + Homebrew Channel (de "YouTube-route")
Dit is wat je zoekt als je echt controle wil.

**Wat je ervoor terugkrijgt:**
- Root-shell op de tv (SSH / Telnet).
- **Homebrew Channel**: een eigen app-store voor webOS, met o.a. een optie om telemetrie uit te zetten en **"Block system updates"** (firmware-updatechecks helemaal uit).
- Eigen opstart-scripts via `/var/lib/webosbrew/init.d`.
- Een **failsafe-modus**: als de tv bij het opstarten crasht, komt er een noodshell via Telnet beschikbaar.

**Welke exploit voor jouw tv:**
- **`faultmanager-autoroot`** (door throwaway96) is de aanbevolen methode voor webOS 4.0 en hoger. De webOSbrew-site: *"Works on webOS 4.0 and up, including webOS 9"* en *"As of January 2025, no patched firmware exists."*
- Specifiek relevant voor jou: de README meldt (stand 2025-08-24) dat webOS 5, 6, 7 en 9 inmiddels grotendeels gepatcht zijn, maar dat de auteur **nog geen gepatchte webOS 4.5-firmware heeft gezien**. Jouw C9 valt in die categorie, dus de kans is groot dat hij rootbaar is.
- Alternatief: **DejaVuln** (werkt op webOS 3.5 en hoger, via USB) — handig als faultmanager niet lukt.
- Verouderd / werkt niet meer: **RootMyTV** (gepatcht in 2022), **crashd** (gepatcht april 2024), **WTA**, **GetMeNow**.
- Niet doen: de **NVM**-methode, waarbij je de tv openschroeft. De site waarschuwt letterlijk: *"You may **damage your TV permanently** without proper knowledge."*

**Globale stappen (details in §3):** firmware-versie checken → verifiëren op CanI.RootMy.TV → Developer Mode aanzetten → via SSH `autoroot.sh` uitvoeren → Developer Mode-app verwijderen → Homebrew Channel staat erop.

### Niveau 2 — De interface echt vervangen
Pas doen als niveau 1 werkt en stabiel is.

- **`youtube-webos`** — YouTube zonder advertenties, met SponsorBlock, Shorts weg, afgedwongen hoogste kwaliteit, audio-only-modus. **Root is hier niet eens voor nodig** (kan via Developer Mode), maar met Homebrew Channel is het permanent. De officiële YouTube-app moet je eerst verwijderen.
- **`Luma`** — een alternatieve launcher/home-screen in Apple TV-stijl voor geroote tv's. De C9 staat in de compatibiliteitslijst onder webOS 4 en Luma *"should start on any TV running webOS 4 or newer"*.
  - **Maar let op:** de "takeover"-functie, waarmee Luma de LG-home-knop echt overneemt, wordt volgens de documentatie alleen ondersteund op webOS 5, 6, 25 en 26. Op webOS 4 (jouw C9) kun je dus naar verwachting alleen de autostart-variant gebruiken, die de Home-knop **niet** herkent. *(Onverifieerd voor exact de C9 — de lijst markeert takeover per model, en C8/UM7450 staan expliciet op ❌.)*
- Overige homebrew die vaak genoemd wordt: Piccap/Hyperion (ambilight), Device Manager, Input Hook.

---

## 3. Concreet stappenplan niveau 1 (voor een beginner)

### Stap 0 — Informatie verzamelen (doe dit eerst, voordat je iets installeert)
1. Op de tv: **Alle instellingen → Ondersteuning → Over deze tv**. Schrijf op:
   - exacte modelnaam (`OLED55C9PLA...`)
   - **softwareversie / firmware** (bv. `05.30.xx`)
   - webOS-versie als die genoemd wordt
2. Vul die gegevens in op **https://cani.rootmy.tv/** — dat is de officiële checker. Die vertelt je of jouw firmware kwetsbaar is en welke exploit je moet gebruiken.
3. **Zet automatische updates uit, nu.** Als LG een gepatchte firmware voor de C9 uitbrengt en jouw tv die binnenhaalt, is de root-route mogelijk voorgoed weg.

> ⛔ **Stop hier als CanI.RootMy.TV zegt dat je firmware niet kwetsbaar is.** Firmware downgraden is een aparte, risicovollere route. Dan is niveau 0 (extern kastje + DNS-blokkade) je beste optie.

### Stap 1 — Voorbereiden
- Laptop op hetzelfde netwerk als de tv.
- Een SSH-client. Op Windows: PowerShell heeft `ssh` ingebouwd, of gebruik PuTTY. Op Mac/Linux: Terminal.
- Zet **Quick Start+** uit op de tv (staat in de troubleshooting van de exploit).
- Controleer dat de **datum/tijd van de tv correct** staat — een foute datum geeft een `errorCode -5`.

### Stap 2 — Developer Mode
- Maak een gratis account op `developer.lge.com`.
- Installeer de **Developer Mode**-app uit de LG Content Store, log in, zet Dev Mode aan, zet **Key Server** aan, en herstart de tv.
- Noteer het IP-adres van de tv.

### Stap 3 — Rooten
- Verbind via SSH met de tv (poort 9922, gebruiker `prisoner`).
- Download `autoroot.sh` naar `/tmp` op de tv en voer uit: `sh /tmp/autoroot.sh`
- Wacht op het bericht **"Payload complete"**.
- De exploit veroorzaakt *bewust* een segmentation fault — dat is normaal, niet kapot.
- Als Homebrew Channel er na succes niet lijkt te staan: herstarten, en Quick Start+ uit.

### Stap 4 — Afronden (niet overslaan)
- **Verwijder de LG Developer Mode-app vóórdat je herstart.** De README is expliciet: *"Do not install the LG Developer Mode app while the TV is rooted!"*
- Open Homebrew Channel → zet **"Block system updates"** aan.
- Zet de telemetrie-opties in Homebrew Channel uit.
- **Zet direct een SSH-key.** Homebrew Channel gebruikt standaard het wachtwoord `alpine` tot je eigen keys hebt ingesteld, en Telnet is zelfs volledig zonder authenticatie — dus niet aan laten staan.

### Stap 5 — Pas daarna leuke dingen
`youtube-webos` installeren, eventueel Luma, Piccap, etc.

---

## 4. Risico's, eerlijk op een rij

| Risico | Hoe groot | Hoe beperk je het |
|---|---|---|
| Tv onbruikbaar ("bricken") | Klein bij het volgen van het script, reëel bij eigen gerommel in het systeem | Niet improviseren; failsafe-telnetshell bestaat; blijf van NVM/hardware af |
| Exploit werkt niet (gepatcht) | Onbekend tot je CanI.RootMy.TV hebt gecheckt | Eerst checken, dan beginnen |
| Garantie vervalt | Ja, maar de tv is uit 2019 — garantie is er toch al af | n.v.t. |
| Root verdwijnt na firmware-update | Mogelijk; webOSbrew: *"Theoretically, root can be persistent across updates. But it's not guaranteed."* | Updates blokkeren via Homebrew Channel |
| Open SSH/Telnet = tv aanvalbaar in je eigen netwerk | Reëel als je het standaardwachtwoord laat staan | SSH-keys instellen, Telnet uit |
| Te brede DNS-blokkade breekt functies | Reëel | Stap voor stap, log meekijken |

---

## 5. Mijn aanbeveling

1. **Deze week:** niveau 0 volledig doen (instellingen + DNS-blokkade met log-controle). Meet wat er daarna nog overblijft van je klacht.
2. **Zelfde week:** firmware-versie opzoeken en op CanI.RootMy.TV checken, en automatische updates uitzetten. Dit is tijdkritisch — de mogelijkheid kan verdwijnen met een update.
3. **Daarna, als de klacht nog niet weg is:** niveau 1 (rooten + Homebrew Channel), en daarbovenop `youtube-webos`.
4. **Als rooten niet kan:** extern kastje + tv offline. Dat is geen nederlaag; het is de meest robuuste oplossing en vele malen minder werk.

---

## 6. Bronnen

- faultmanager-autoroot (aanbevolen exploit, webOS 4.0+): https://github.com/throwaway96/faultmanager-autoroot
- webOSbrew rooting-overzicht (welke exploit voor welke versie): https://www.webosbrew.org/rooting
- webOS Homebrew Channel: https://github.com/webosbrew/webos-homebrew-channel
- Firmware-checker: https://cani.rootmy.tv/
- youtube-webos (YouTube zonder ads): https://github.com/webosbrew/youtube-webos
- Luma launcher: https://github.com/ecklf/lg-luma
- DejaVuln autoroot (alternatief, webOS 3.5+): https://github.com/throwaway96/dejavuln-autoroot
- RootMyTV (historisch, gepatcht in 2022): https://github.com/RootMyTV/RootMyTV.github.io

## 7. Wat ik níet kon verifiëren

- De exacte firmwareversie van **jouw** tv, en dus of hij op dit moment rootbaar is. Dat moet via Over deze tv + CanI.RootMy.TV.
- Of Luma's "takeover" op een C9 (webOS 4) werkt. De documentatie noemt alleen webOS 5, 6, 25 en 26.
- Of de Developer Mode-sessie op de C9 periodiek verlengd moet worden bij gebruik zonder root (bekend als beperking van LG's Dev Mode, maar niet opnieuw gecontroleerd voor dit model).
