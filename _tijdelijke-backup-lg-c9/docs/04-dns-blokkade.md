# 04 — DNS-blokkade met Pi-hole of AdGuard Home

Nodig als je de tv **wel** op het netwerk wil houden (bijvoorbeeld voor Home Assistant), maar
niet wil dat hij naar huis belt.

## Het idee

Je zet een DNS-server in je eigen netwerk die bepaalde domeinnamen weigert te vertalen. De tv
vraagt "waar vind ik `lgsmartad.com`?" en krijgt geen antwoord. Het verzoek komt dus nooit aan.

**Bonus:** dit maakt de interface vaak merkbaar vlotter. Een deel van de haperingen in webOS
komt doordat de tv zit te wáchten op advertentie- en telemetrieservers. Een weigering is
direct; een timeout duurt seconden.

## Stap 1 — Pi-hole of AdGuard Home installeren

Draai je al Home Assistant? Dan is **AdGuard Home** als add-on de makkelijkste weg. Anders is
een Pi-hole op een Raspberry Pi de klassieker. Beide doen hetzelfde.

## Stap 2 — De LG-domeinen blokkeren

Lijst staat in [`dns/lg-blocklist.txt`](../dns/lg-blocklist.txt).

Voor Pi-hole kun je ze als *Local DNS record* of in `dnsmasq` zetten:

```
address=/lgsmartad.com/0.0.0.0
```

In AdGuard Home: *Filters → DNS blocklists → Custom filtering rules*.

## Stap 3 — De valkuil die iedereen vergeet ⚠️

**Een slimme tv kan je DNS-server omzeilen.** Veel apparaten hebben een *hardcoded* DNS-server
ingebakken (vaak die van Google) en gebruiken die als jouw server iets blokkeert. Dan heb je
een Pi-hole die netjes logt dat hij niets doet.

Oplossing, op je **router**:
- Blokkeer uitgaand **poort 53** (DNS) voor alle apparaten, **behalve** naar je Pi-hole/AdGuard.
  Of beter: *redirect* alle poort-53-verkeer naar je eigen server.
- Blokkeer ook uitgaand **poort 853** (DNS-over-TLS), anders gaat het daarlangs.

Zonder deze stap is je blokkade mogelijk schijn. Dit is geen detail.

> Volledige dekking krijg je met DNS nooit: een apparaat dat DNS-over-HTTPS (poort 443) gebruikt
> is met deze methode niet te stoppen, want dat verkeer is niet te onderscheiden van gewoon
> web-verkeer. Daarom is [route A](02-route-a-tv-offline.md) technisch sterker.

## Stap 4 — Meten of het werkt

Dit is de belangrijkste stap en wordt bijna altijd overgeslagen.

1. Kijk in het **log** van je Pi-hole/AdGuard, gefilterd op het IP-adres van je tv.
2. Zet de tv aan, loop door het menu, start een app.
3. Je ziet nu letterlijk welke domeinen je tv aanroept — en welke geblokkeerd zijn.

Dat log is je bewijs. Het vertelt je ook of er domeinen bij zitten die niet in de lijst staan;
voeg die dan toe.

## Stap 5 — Wat je kunt breken

Te breed blokkeren heeft gevolgen:
- Blokkeer je alle update-domeinen, dan kun je geen firmware-updates meer binnenhalen.
  (Bij dit plan vaak gewenst — maar weet dat je het doet.)
- Sommige apps kunnen haperen als een CDN-domein meegeblokkeerd wordt.

**Werkwijze:** blokkeer in kleine stappen, test na elke stap, en houd het log erbij.
