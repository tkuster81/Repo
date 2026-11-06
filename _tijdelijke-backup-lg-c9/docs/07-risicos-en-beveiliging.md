# 07 — Risico's en beveiliging

## Risicotabel

| Risico | Hoe groot | Hoe beperk je het |
|---|---|---|
| Tv onbruikbaar ("bricken") | Klein bij het volgen van het script; reëel bij eigen gerommel in het systeem | Niet improviseren; er is een failsafe-telnetshell; blijf van de NVM/hardware-methode af |
| Exploit werkt niet (gepatcht) | Onbekend tot je CanI.RootMy.TV hebt gecheckt | Eerst checken, dan beginnen |
| Garantie vervalt | Ja — maar de tv is uit 2019, die is er toch al af | n.v.t. |
| Root verdwijnt na firmware-update | Mogelijk. webOSbrew: *"Theoretically, root can be persistent across updates. But it's not guaranteed."* | Updates blokkeren via Homebrew Channel |
| **Open SSH/Telnet = root-shell in je netwerk** | **Reëel** als je standaardinstellingen laat staan | SSH-key instellen, Telnet uit — zie hieronder |
| Te brede DNS-blokkade breekt functies | Reëel | Stap voor stap, log meekijken ([04](04-dns-blokkade.md)) |
| Onbekende root-scripts van internet | Reëel | Alleen webosbrew / throwaway96 ([06](06-apps-na-root.md)) |

## Het update-dilemma ⚠️

Dit is de belangrijkste afweging in dit hele plan, en hij wordt in video's zelden genoemd.

**Om te kunnen rooten, mag je niet updaten.** Een nieuwe firmware kan de exploit dichtmaken.
Daarom staat in [03](03-niveau-0-instellingen.md): zet automatische updates uit.

**Maar:** webOS heeft een terugkerende stroom van kwetsbaarheden waarmee een aanvaller
**vanaf je lokale netwerk root-rechten** op de tv kan krijgen. Een paar datapunten:

- LG heeft in maart 2024 meerdere root-kwetsbaarheden in webOS gepatcht. Destijds werd gemeld
  dat ruim 90.000 webOS-tv's vanaf internet bereikbaar en kwetsbaar waren.
- In oktober 2026 is een keten van drie kwetsbaarheden gepubliceerd die een aanvaller op
  hetzelfde lokale netwerk root geeft *"without a PIN or any interaction from the owner"*.
  Getest op twee modellen (`32LQ636BPSA` en `27TQ600SW`, webOS 7.5.7-25, firmware 04.54.40).
  Of andere modellen en firmwareversies kwetsbaar zijn, is **niet bekend** — dus ook niet
  bekend of jouw C9 erbij hoort. LG heeft een fix uitgebracht.

**Wat dit betekent:** een C9 op oude, niet-geüpdatete firmware die aan je netwerk hangt, is
een apparaat met bekende en toekomstige lekken dat je bewust niet meer patcht. Dat is te
verdedigen, maar het moet een keuze zijn, niet een ongeluk.

### De drie manieren om hiermee om te gaan

| Keuze | Gevolg |
|---|---|
| **Tv offline** ([route A](02-route-a-tv-offline.md)) | Lekken zijn niet te bereiken. Updaten hoeft niet meer. **Dit lost het dilemma volledig op.** |
| **Tv online + geroot + updates geblokkeerd** | Je accepteert bekende lekken. Zet de tv dan minimaal in een **apart VLAN / gastnetwerk** zonder toegang tot je pc's, NAS en telefoons. |
| **Tv online + updaten** | Veilig, maar je verliest de root-mogelijkheid, mogelijk voorgoed. |

> Gegeven dat je al een extern kastje hebt, is de eerste optie bij jou vrijwel gratis. Dat is
> waarom [route A](02-route-a-tv-offline.md) in dit plan de aanbeveling is — niet omdat rooten
> te moeilijk zou zijn, maar omdat het bij jou een probleem oplost dat je anders zelf
> introduceert.

## Veiligheidsregels als je rooten

1. **SSH-key instellen, direct.** Standaardwachtwoord is `alpine`.
2. **Telnet uit.** De documentatie zelf: *"Telnet - unauthenticated, use sparingly."*
3. **Developer Mode-app verwijderd houden.** *"Do not install the LG Developer Mode app while
   the TV is rooted!"*
4. **Tv in een apart netwerksegment**, als je router dat kan.
5. **Geen onbekende scripts als root uitvoeren.**
