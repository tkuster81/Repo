# Checklist

Afvinken terwijl je bezig bent. Begin bovenaan; de bovenste blokken hebben nul risico.

## Blok 1 — Vandaag, 20 minuten, nul risico

- [ ] **Firmwareversie opschrijven** (*Alle instellingen → Ondersteuning → Over deze tv*)
      Model: `______________`  Firmware: `______________`
- [ ] Firmware gecheckt op **https://cani.rootmy.tv/** → uitkomst: `______________`
- [ ] **Automatische software-updates UIT** ⏳ *tijdkritisch — houdt route B open*
- [ ] *Home-instellingen* → **Home Promotion UIT**
- [ ] *Home-instellingen* → **Content Recommendation UIT**
- [ ] *Home-instellingen* → **Power On Screen = `Recent Input`** ⭐ *grootste effect*
- [ ] *Gebruikersovereenkomsten* → marketing / advertenties / analytics **ingetrokken**
- [ ] **Live Plus (ACR) UIT**
- [ ] Ongebruikte LG-apps **verborgen**
- [ ] **HDMI-CEC / SIMPLINK AAN** (zodat je kastje de tv kan schakelen)
- [ ] Getest: tv uit en aan → komt direct op het kastje uit, geen LG-home-screen

→ **Beoordeel hier of je klacht al weg is.** Grote kans van wel.

## Blok 2 — Keuze maken

- [ ] [docs/07 — Risico's en beveiliging](docs/07-risicos-en-beveiliging.md) gelezen,
      met name het **update-dilemma**
- [ ] Heb ik de tv op het netwerk nodig? (bijv. Home Assistant) → ja / nee
- [ ] **Route gekozen:**
      - [ ] **A — tv offline** *(aanbevolen; je hebt al een kastje)*
      - [ ] **B — online + rooten**

## Blok 3a — Route A: tv offline

- [ ] Wifi-verbinding **vergeten/verbroken**, LAN-kabel eruit
- [ ] Getest: alles werkt nog via het kastje
- [ ] *Optioneel:* MAC-adres van de tv **geblokkeerd op de router**
- [ ] ✅ Klaar. Geen tracking, geen advertenties, geen aanvalsoppervlak.

## Blok 3b — Route B: online houden

### DNS-blokkade
- [ ] Pi-hole of AdGuard Home draait
- [ ] Domeinen uit [`dns/lg-blocklist.txt`](dns/lg-blocklist.txt) toegevoegd
- [ ] **Router: uitgaand poort 53 geblokkeerd** behalve naar eigen DNS ⚠️ *anders schijnveiligheid*
- [ ] **Router: uitgaand poort 853 geblokkeerd**
- [ ] **DNS-log gecontroleerd** op het IP van de tv → welke domeinen roept hij écht aan?
- [ ] Ontbrekende domeinen uit het log **toegevoegd aan de lijst**
- [ ] Niets kapot: apps getest

### Rooten
- [ ] CanI.RootMy.TV zegt: **kwetsbaar** (zo niet → stop, ga naar route A)
- [ ] **Quick Start+ UIT**
- [ ] **Datum/tijd van de tv correct**
- [ ] Account op `developer.lge.com`
- [ ] **Developer Mode**-app geïnstalleerd, Dev Mode AAN, **Key Server AAN**, herstart
- [ ] IP-adres van de tv: `______________`
- [ ] SSH gelukt (poort **9922**, gebruiker **`prisoner`**)
- [ ] `autoroot.sh` naar `/tmp`, uitgevoerd, **"Payload complete"** gezien
- [ ] ⚠️ **Developer Mode-app VERWIJDERD vóór herstart**
- [ ] Homebrew Channel is zichtbaar en werkt

### Direct na root — niet uitstellen
- [ ] **SSH-key ingesteld** (standaardwachtwoord is `alpine`) 🔒
- [ ] **Telnet UIT** 🔒
- [ ] Homebrew Channel → **"Block system updates" AAN**
- [ ] Homebrew Channel → **telemetrie UIT**
- [ ] *Aanbevolen:* tv in **apart VLAN / gastnetwerk**

### Daarna de leuke dingen
- [ ] Officiële YouTube-app verwijderd
- [ ] **`youtube-webos`** geïnstalleerd (groene knop = instellingen)
- [ ] *Optioneel:* Piccap / Hyperion voor ambilight
- [ ] *Optioneel:* Luma — maar verwacht geen werkende Home-knop op webOS 4
