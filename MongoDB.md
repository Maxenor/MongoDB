# Semaine Mongo DB

## Introduction

Document stocké dans un conteneur JSON sans schéma défini. Information stocké sous champs (objets)
BDD orienté document.

> https://www.mongodb.com/docs/

Possibilité d'imbriquer dans des tableaux. Trsè gros désavantage = informations dupliquées.

## Commandes

use pour creer une nouvelle base de données qui n'existe pas. L'insertion du premier document va creer la base.
"db" est un mot réservé.
la combinaison de db et collection représente un namespace

# Exercices

### Exo 1
Affichez l’identifiant et le nom des salles qui sont des SMAC.
db.salles.find( { smac: true}, { nom: 1, _id:0})

Requête qui sélectionne que les champs avec smac = true.

### Exo 2
db.salles.find( { capacite : { $gt: 1000}}, { nom: 1, _id:0})
Requête qui montre les salles dont la capacité est supérieure a 1000
### Exo 3
db.salles.find({"adresse.numero": {$exists: false}}, {"nom":1})

Permet de trouver les adresses qui ont un champ numéro vide.

### Exo 4
db.salles.find({"avis": {$size: 1}}, {"nom":1})
Permet de trouver les salles qui ont exactement un avis.

### Exo 5
db.salles.fi	nd({"styles.": {$eq: "blues"}}, {"styles":1})
Permet de trouver les salles qui programment du blues.

### Exo 6
db.salles.find({"styles.0": {$eq: "blues"}}, {"styles":1})
Permet de trouver les salles qui ont en 1ere position dans le tableau styles "blues"

### Exo 7 
db.salles.find( { "codePostal": { "\$regex": "^84" }, "capacite": { "\$lt": 500 } }, { "ville": 1 } )

Permet de voir les villes qui ont un code postal commençant par 84 et avec une capacité inférieure a 500

### Exo 8

db.salles.find({ \$or : [ {"avis": {\$exists: false}}, {"_id": {$mod: [2, 0]}}]}, {"nom": 1})
Permet de chercher les salles qui ont un id pair et pas d'avis

### Exo 9
db.salles.find({"avis.note": {\$gte :8}, "avis.note": {\$lte: 10}}, {"_id": 1})
Permet de trouver les salles dont les avis sont compris entre 8 et 1 inclus

### Exo 10
db.salles.find({"avis.date": {$gt: ISODate("2019-11-15")}}, {"nom": 1})

Permet de trouver les salles qui ont un avis datant d'avant le 15 11 2019.

### Exo 11
db.salles.find({\$expr: {\$gt: [{\$multiply: ["\$_id", 100]}, "$capacite"]}}, {nom: 1, capacite: 1})
Permet d'avoir les salles dont l'id multiplié par 100 est supérieur a la capacité

### Exo 12
db.salles.find({"type": "smac", "$where": "this.styles?.length > 2"}, {"_id": 0, "nom": 1})

### Exo 13
db.salles.find({}, {"_id": 0, "adresse.codePostal": 1})
Permet d'afficher tout les codes postaux

### Exo 14
db.salles.updateMany({}, {$inc: {"capacite": 100}})
Permet d'ajouter 100 a la capacité des salles.

### Exo 15
db.salles.updateMany({"styles": {\$ne: "jazz"}}, {\$push: {"styles": "jazz"}}) 
Permet d'ajouter le style "jazz" a toutes les salles

### Exo 16
db.salles.updateMany({"_id": {\$nin: [2, 3]}, "styles": "funk"}, {\$pull: {"styles": "funk"}})
Permet de retirer le style funk aux salles dont l'id n'est ni 2 ni 3

### Exo 17
db.salles.updateOne({"_id": 3}, {$addToSet: { "styles": { $each: ["techno", "reggae"] } }})
Permet d'ajouter à la salle avec id 3 les styles techno et reggae.

###



# Lexique

Document : ensemble de données clé => valeur, très proche du js.

Schéma : il est dynamique

Collection : permet de stocker des documents de manière logique comme une table. schéma adaptable.






> **Note:** The **Publish now** button is disabled if your file has not been published yet.
> **ProTip:** You can disable any **Markdown extension** in the **File properties** dialog.


## SmartyPants

SmartyPants converts ASCII punctuation characters into "smart" typographic punctuation HTML entities. For example:

|                |ASCII                          |HTML                         |
|----------------|-------------------------------|-----------------------------|
|Single backticks|`'Isn't this fun?'`            |'Isn't this fun?'            |
|Quotes          |`"Isn't this fun?"`            |"Isn't this fun?"            |
|Dashes          |`-- is en-dash, --- is em-dash`|-- is en-dash, --- is em-dash|

## UML diagrams

You can render UML diagrams using [Mermaid](https://mermaidjs.github.io/). For example, this will produce a sequence diagram:

```mermaid
sequenceDiagram
Alice ->> Bob: Hello Bob, how are you?
Bob-->>John: How about you John?
Bob--x Alice: I am good thanks!
Bob-x John: I am good thanks!
Note right of John: Bob thinks a long<br/>long time, so long<br/>that the text does<br/>not fit on a row.

Bob-->Alice: Checking with John...
Alice->John: Yes... John, how are you?
```

And this will produce a flow chart:

```mermaid
graph LR
A[Square Rect] -- Link text --> B((Circle))
A --> C(Round Rect)
B --> D{Rhombus}
C --> D
```
