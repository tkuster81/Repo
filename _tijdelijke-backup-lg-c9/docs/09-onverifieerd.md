# 09 — Wat ik níet heb kunnen vaststellen

Expliciet apart gezet, zodat het niet als feit wordt gelezen.

## Over de tv

| Onderwerp | Status |
|---|---|
| De **exacte firmwareversie** van jouw tv, en dus of hij op dit moment rootbaar is | **Niet bekend.** Alleen vast te stellen via *Over deze tv* + https://cani.rootmy.tv/. Alles in [05](05-route-b-rooten.md) staat of valt hiermee. |
| Of de C9 kwetsbaar is voor de keten uit oktober 2026 | **Niet bekend.** Getest op `32LQ636BPSA` en `27TQ600SW` (webOS 7.5.7-25). De publicatie zegt zelf: *"Whether other models or firmware versions are affected is not known."* |
| Of Luma's **takeover** op een C9 (webOS 4) werkt | **Onverifieerd.** De documentatie noemt alleen webOS 5, 6, 25 en 26. C8 en UM7450 staan op ❌; de C9 heeft geen expliciete markering. |
| Of de **Developer Mode-sessie** periodiek verlengd moet worden bij gebruik zonder root | **Onverifieerd.** Dit is een bekende beperking van LG's Dev Mode, maar niet opnieuw gecontroleerd voor dit model. |

## Over de DNS-lijst

De domeinenlijst in [`dns/lg-blocklist.txt`](../dns/lg-blocklist.txt) komt uit
community-bronnen die **onderling niet consistent zijn** en is **niet geverifieerd tegen
officiële LG-documentatie**. Eén bron meldde bovendien dat een `hosts`-bestand
`info.lgsmartad.com` niet blokkeerde, dus een hosts-bestand alleen is mogelijk onvoldoende.

**Daarom staat stap 4 in [04](04-dns-blokkade.md):** kijk in je eigen DNS-log wat de tv écht
aanroept. Dat is de enige betrouwbare lijst.

## Over de YouTube-video

De aangeleverde video (`https://youtu.be/i0ytu6k8uac`) **kon ik niet inzien**. YouTube-pagina's
leveren alleen navigatie-elementen op bij het ophalen, en het video-ID komt niet in
zoekresultaten voor. De inhoud van die video is dus **niet gevonden** en op geen enkele manier
in dit plan verwerkt.

Wil je hem alsnog laten natrekken: geef de **titel** of de **kanaalnaam**.

## Over "custom OS"

Er is **geen** project gevonden dat webOS vervangt door Android of een andere Linux-distributie
op LG-tv's. Dat is een negatieve bevinding uit zoekwerk, geen bewijs dat het nergens bestaat.
Maar: de bootloader is niet ontgrendelbaar en de firmware is ondertekend, en de hele community
rond LG-tv's werkt *binnen* webOS. Dat is consistent met "het kan niet".
