# 08 — Bronnen

Alles in dit plan is hierop gebaseerd. Peildatum onderzoek: **2026-11-06**.

## Primaire bronnen (projecten met reputatie)

| Bron | Waarvoor gebruikt |
|---|---|
| https://github.com/throwaway96/faultmanager-autoroot | aanbevolen exploit; webOS 4.0–10.0; patchstatus; stappen; waarschuwingen |
| https://www.webosbrew.org/rooting | overzicht welke exploit bij welke webOS-versie; wat gepatcht is; NVM-waarschuwing |
| https://github.com/webosbrew/webos-homebrew-channel | wat Homebrew Channel biedt; failsafe-modus; `alpine`-wachtwoord; Telnet-waarschuwing |
| https://cani.rootmy.tv/ | firmware-checker (zelf invullen met je eigen versie) |
| https://github.com/webosbrew/youtube-webos | advertentievrije YouTube; features; installatie |
| https://github.com/ecklf/lg-luma | launcher; compatibiliteitslijst; takeover alleen webOS 5/6/25/26 |
| https://github.com/throwaway96/dejavuln-autoroot | alternatieve exploit, webOS 3.5+ |
| https://github.com/RootMyTV/RootMyTV.github.io | historisch; gepatcht in 2022 |

## Achtergrond en context

| Bron | Waarvoor gebruikt |
|---|---|
| https://velmo.one/guides/debloat-lg-tv/ | wat webOS wel/niet toestaat bij debloaten |
| https://debloattv.com/lg-samsung-tv-debloat/ | home-screen-instellingen; apps verbergen vs. verwijderen |
| https://forum.level1techs.com/t/lg-tv-block-mini-how-to/255178 | DNS-domeinen; `dnsmasq`-syntax; poort 53/853-omzeiling |
| https://thehackernews.com/2026/10/lg-smart-tvs-vulnerable-to-pre-auth.html | keten van 3 kwetsbaarheden, oktober 2026; getest op 32LQ636BPSA / 27TQ600SW |
| https://cybernews.com/security/lg-smart-tv-webos-complete-takeover-exploit/ | root-kwetsbaarheden webOS, gepatcht maart 2024 |
| https://securityaffairs.com/posts/lg-smart-tvs-vulnerable | ~91.000 blootgestelde webOS-tv's |

## Niet gebruikt, met opzet

Diverse GitHub-repo's met "LG debloat toolkit" in de naam, van accounts zonder staat van
dienst. Die vragen root-toegang tot je tv. Zie de waarschuwing in [06](06-apps-na-root.md).
