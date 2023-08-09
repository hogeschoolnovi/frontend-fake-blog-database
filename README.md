# Fake to-do-applicatie backend

## Beschrijving

Om te oefenen met het versturen en ontvangen van data, kun je deze nepserver gebruiken. De nepserver draait apart van
jouw frontend project, zodat we de "database" via een API kunnen benaderen. Zo kun je todos in de database opvragen en
bewerken, door gebruik te maken van specifieke eindpoints.

## Gebruik

Voor je de server kunt gebruiken zul je de de dependencies moeten installeren met het commando:

`npm install`

Er is een speciaal script aangemaakt om deze server te runnen. Om de server te starten hoef je slechts het volgende commando in jouw terminal in
te voeren:

`npm run json:server`

Deze server draait op [http://localhost:3000](http://localhost:3000), wanneer je dit in de browser opent zul je de
beschikbare endpoints zien verschijnen. Dit mag je echter weer wegklikken, want deze heb je niet nodig.

## Endpoints

Wanneer deze server draait, is hij benaderbaar op [http://localhost:3000](http://localhost:3000). Dis is de **basis url**, welke aan te vullen is met de onderstaande endpoints:

### Alle taken ophalen

`GET /todos`

De backend stuurt bij success een array van taken terug.

**Voorbeeld response**

```json
[
  {
    "id": "fc3afe7e-b043-451d-9b88-7e2a248126b9",
    "title": "Learn CSS",
    "completed": true,
    "description": "Learn CSS and style your web page",
    "priority": 2,
    "created": "2023-08-08T13:28:53.846Z"
  },
  {
    "id": "b8c334a5-8e83-4d6a-a62d-0901fdf7d198",
    "title": "Learn React",
    "completed": false,
    "description": "Learn React and build a todo app",
    "priority": 1,
    "created": "2023-08-08T13:28:53.846Z"
  }
]
```

### Een taak toevoegen

`POST /todos`

Er kan slechts één taak tegelijk worden toegevoegd. Bij het toevoegen van een taak moeten de volgende velden worden
meegestuurd in een object, om consistentie in de database te waarborgen:

* `id` (type _String_)
* `title` (type _String_)
* `completed` (type _Boolean_)
* `description` (type _String_)
* `priority` (type _Number_)
* `created` (type _Date_)

De backend stuurt bij success alle informatie van de zojuist toegevoegde taak terug;

### Een taak ophalen

`GET /todos/:id`

Hierin wordt `:id` vervangen voor de daadwerkelijke id van de taak die verwijderd moet worden. De backend stuurt bij
success een taak-object terug.

**Voorbeeld response**

```json
  {
  "id": "fc3afe7e-b043-451d-9b88-7e2a248126b9",
  "title": "Learn CSS",
  "completed": true,
  "description": "Learn CSS and style your web page",
  "priority": 2,
  "created": "2023-08-08T13:28:53.846Z"
}
```

### Een taak verwijderen

`DELETE /todos/:id`

Hierin wordt `:id` vervangen voor de daadwerkelijke id van de taak die verwijderd moet worden. De backend stuurt bij
success een leeg object terug.

### Een taak wijzigen

`PUT /todos/:id`

Hierin wordt `:id` vervangen voor de daadwerkelijke id van de taak die gewijzigd moet worden. Alle velden, behalve
het `id`-veld, kunnen gewijzigd worden.
Let op: je stuurt het nieuwe taak-object met alle gewenste wijzigingen mee, ook als slechts één van de velden gewijzigd
is:

* `title` (type _String_)
* `completed` (type _Boolean_)
* `description` (type _String_)
* `priority` (type _Number_)
* `created` (type _Date_)

De backend stuurt bij success het gewijzigde taak-object terug.

### Profielinformatie ophalen

`GET /profile`

Bij het ophalen van de profiel-informatie stuurt de backend standaard de volgende response terug:

```json
  {
  "name": "Equals"
}
```

Wanneer je hiermee jouw eigen profiel-informatie zou willen ophalen, kun je de velden desgewenst handmatig toevoegen aan
de database (`db.json`). Let er hierbij wel op dat dit in JSON-format gedaan wordt. 

**Voorbeeld**
```json
{
  "profile": {
    "name": "Marieke",
    "age": 32,
    "city": "Utrecht"
  }
}
```
