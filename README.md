# Fake blog backend

## Beschrijving

Om te oefenen met het versturen en ontvangen van data, kun je deze nepserver gebruiken. De nepserver draait apart van
jouw frontend project, zodat we de "database" via een API kunnen benaderen. Zo kun je blogposts in de database opvragen
en
bewerken, door gebruik te maken van specifieke eindpoints.

## Gebruik

Voor je de server kunt gebruiken zul je de de dependencies moeten installeren met het commando:

```shell
npm install
```

Er is een speciaal script aangemaakt om deze server te runnen. Om de server te starten hoef je slechts het volgende
commando in jouw terminal in
te voeren:

```shell
npm run json:server
```

Deze server draait op [http://localhost:3000](http://localhost:3000), wanneer je dit in de browser opent zul je de
beschikbare endpoints zien verschijnen. Dit mag je echter weer wegklikken, want deze heb je niet nodig.

## Endpoints

Wanneer deze server draait, is hij benaderbaar op [http://localhost:3000](http://localhost:3000). Dis is de **basis url
**, welke aan te vullen is met de onderstaande endpoints:

### Alle posts ophalen

`GET /posts`

De backend stuurt bij success een array van blogposts terug.

**Voorbeeld response**

```json
[
  {
    "id": 1,
    "title": "De Smaken van Italië",
    "subtitle": "Een culinaire reis door Bella Italia",
    "content": "Italië, het land van heerlijke pasta, pizza en gelato, is een culinair paradijs dat elke fijnproever moet ervaren. In deze blog nemen we je mee op een smakelijke reis door Bella Italia. Ontdek de geheimen achter de perfecte risotto, leer hoe je zelfgemaakte pasta maakt en proef de verrukkelijke regionale gerechten van Noord tot Zuid. Bereid je voor om je smaakpapillen te verwennen in de keuken van de laarsvormige natie.",
    "created": "2023-09-21T09:30:00Z",
    "author": "Anna de Kok",
    "readTime": 5,
    "comments": 12,
    "shares": 8
  },
  {
    "id": 2,
    "title": "De Pracht van Thailand",
    "subtitle": "Een avontuurlijke reis door het land van de glimlach",
    "content": "Thailand is een betoverend land met een rijke cultuur, adembenemende natuurlijke schoonheid en een verrukkelijke keuken. In deze blog nemen we je mee op een avontuurlijke reis door het 'Land van de Glimlach'. Verken de bruisende straten van Bangkok, ontspan op de witte zandstranden van Phuket en proef de heerlijke streetfoodgerechten die je op elke hoek van de straat vindt. Laat je inspireren om Thailand te verkennen en haar unieke schoonheid en smaken te ontdekken.",
    "created": "2023-09-20T11:45:00Z",
    "author": "Erik van der Reis",
    "readTime": 7,
    "comments": 18,
    "shares": 10
  }
]
```

### Een post toevoegen

`POST /posts`

Er kan slechts één post tegelijk worden toegevoegd. Bij het toevoegen van een post moeten de volgende velden worden
meegestuurd in een object, om consistentie in de database te waarborgen:

* `title` (type _String_)
* `subtitle` (type _String_)
* `content` (type _String_)
* `created` (type _String_)
* `author` (type _String_)
* `readTime` (type _Number_)
* `comments` (type _Number_)
* `shares` (type _Number_)

Je stuurt dus geen `id` mee, deze wordt door de backend zelf aangemaakt. De backend stuurt bij success alle informatie
van de zojuist toegevoegde blogpost terug.

### Een post ophalen

`GET /posts/:id`

Hierin wordt `:id` vervangen voor de daadwerkelijke id van de blog die opgehaald moet worden. De backend stuurt bij
success een compleet taak-object terug.

**Voorbeeld response**

```json
{
  "id": 1,
  "title": "De Smaken van Italië",
  "subtitle": "Een culinaire reis door Bella Italia",
  "content": "Italië, het land van heerlijke pasta, pizza en gelato, is een culinair paradijs dat elke fijnproever moet ervaren. In deze blog nemen we je mee op een smakelijke reis door Bella Italia. Ontdek de geheimen achter de perfecte risotto, leer hoe je zelfgemaakte pasta maakt en proef de verrukkelijke regionale gerechten van Noord tot Zuid. Bereid je voor om je smaakpapillen te verwennen in de keuken van de laarsvormige natie.",
  "created": "2023-09-21T09:30:00Z",
  "author": "Anna de Kok",
  "readTime": 5,
  "comments": 12,
  "shares": 8
}
```

### Een post verwijderen

`DELETE /posts/:id`

Hierin wordt `:id` vervangen voor de daadwerkelijke id van de post die verwijderd moet worden. De backend stuurt bij
success een leeg object (`{}`) terug.

### Een post wijzigen

`PUT /posts/:id`

Hierin wordt `:id` vervangen voor de daadwerkelijke id van de blog die gewijzigd moet worden. Alle velden, behalve
het `id`-veld, kunnen gewijzigd worden. _Let op:_ je stuurt het **gehele blogpost-object** inclusief alle gewenste
wijzigingen mee, ook als slechts één van de velden gewijzigd is. De oude blogpost wordt namelijk in z'n geheel vervangen
met de taak die je in dit request meestuurt (behalve de `id`-key).

* `title` (type _String_)
* `subtitle` (type _String_)
* `content` (type _String_)
* `created` (type _String_)
* `author` (type _String_)
* `readTime` (type _Number_)
* `comments` (type _Number_)
* `shares` (type _Number_)

De backend stuurt bij success het gewijzigde blogpost-object terug.
