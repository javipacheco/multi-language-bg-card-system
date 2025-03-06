# BGG Catalog: Documentación para Sistema de Cartas de Juegos de Mesa Multi-Idioma

Este repositorio proporciona documentación detallada sobre cómo crear archivos de cartas de juegos de mesa multi-idioma para la aplicación "Catálogo BGG", una aplicación de juegos de mesa disponible en Android e iOS.

## Sobre BGG Catalog

"Catálogo BGG" es una aplicación diseñada para ayudar a los usuarios a gestionar y puntuar sus juegos de mesa. La aplicación está disponible tanto en plataformas Android como iOS.

- Disponible en [Android](https://bit.ly/3oYT9HU)
- Disponible en [iPhone y iPad](https://apple.co/3f9ARRG)

## Por qué este repositorio

Este repositorio muestra cómo crear un archivo de fichas de juegos de mesa en varios idiomas para la aplicación "Catálogo BGG". Los archivos están en formato JSON, no te preocupes si no eres programador, ya que son muy fáciles de crear.

Además este repositorio contiene archivos para juegos que ya están disponibles en "Catálogo BGG", por lo que podrás:

- Crear nuevas traducciones para juegos existentes
- Revisar traducciones de juegos actuales
- Crear un nuevo archivo para otro juego

Los archivos de traducción deben estar en inglés para ser subidos a la aplicación, además de cualquier idioma que quieras añadir

## Cómo contribuir

Sólo tienes que mirar la documentación y enviarme el archivo de traducción a gadestudios@gmail.com, pero antes ponte en contacto conmigo para ver si hay alguien más haciéndolo y no duplicar esfuerzos ;-)

Cuando me envíes el correo:

- Puedes hacerlo en inglés o en español
- El asunto debe empezar por "CARDS -" y añadir el nombre del juego

## Documentación

A continuación se explica de forma detallada los nodos del archivo JSON para la traducción de las cartas

### Estructura General

El archivo tiene la siguiente estructura (esto es un ejemplo de El Banquete de Odín):

```json
{
    "translations": [
        {
            "lang": "en",
            "cards": [
                {
                    "id": "1A",
                    "name": "Peddler",
                    "description": "Each time you use a “Livestock Market” action space, you receive a discount of 1 silver on the total cost of the goods. (For instance, cattle plus milk cost you 2 instead of 3 silver.) You do not receive the discount on goods that are already free of cost.",
                    "data": {
                        "points": 0,
                        "type": "EACH_TIME_CARD"
                    }
                },
                {
                    "id": "2C",
                    "name": "Patron",
                    "description": "On each action space whose actions cost at least 2 silver, you receive a discount of 1 silver, including Emigration from round 2, buying salt meat or cattle plus milk\/sheep, as well as the “Buy 2 Special Tiles” action, if applicable. (When you buy a pair of goods, only its total cost is reduced by 1 silver. For instance, Helmet plus Belt only cost you 2 silver instead of 3. This card does not reduce the cost of ships.)",
                    "data": {
                        "points": 1,
                        "type": "EACH_TIME_CARD"
                    }
                }
            ]
        }
}
```

Un archivo JSON contiene nodos **clave-valor**. La **clave** no se cambia y especifica lo qie significa el dato o **valor**, que si cambia con el dato del idioma concreto. Siempre tendrémos un nodo principal llamado **"translations"** que contendrá todas las traducciones. El nodo **lang** nos dirá el idioma de las cartas, que puede ser: "en", "es", "it", etc. y el nodo **cards** contiene la lista de cartas en ese idioma. Por ejemplo, si tenemos varios idiomas sería algo así:

```json
{
    "translations": [
        {
            "lang": "en",
            "cards": [
                ... lista de cartas ....
            ]
        },
        {
            "lang": "es",
            "cards": [
                ... lista de cartas ....
            ]
        },
        {
            "lang": "it",
            "cards": [
                ... lista de cartas ....
            ]
        }
    ]
}
 ```

### Información de cada carta

Como hemos dicho, el nodo **"cards"** contendrá todas las cartas, por lo cual cada idioma tendrá que tener un nodo por cada una de las cartas del juego como el siguiente:

```json
{
    "id": "1A",
    "name": "Peddler",
    "description": "Each time you use a “Livestock Market” action space, you receive a discount of 1 silver on the total cost of the goods. (For instance, cattle plus milk cost you 2 instead of 3 silver.) You do not receive the discount on goods that are already free of cost.",
    "data": {
        "points": 0,
        "type": "EACH_TIME_CARD"
    }
}
```

Los nodos **"id"**. **"name"** y **"description"** son OBLIGATORIOS, por lo que siempre tienen que estar presentes en la carta. 

- El nodo **id** debe tener un valor único de la carta, normalmente será un número o idenficador único. En el raro caso que no exista, pon un número de forma ascendente en cada identificador
- Los nodos **"name"** y **"description"** contienen la información de la carta

El nodo **data** es un poco especial ya que puede existir o no, y la información es específica para cada juego, pudiendo añadir tu la información que creas interesante para el juego.

#### Ejemplos del nodo data

Por ejemplo en el caso del "El Banquete de Odín" el campo **type** puede ser: EACH_TIME_CARD, IMMEDIATE_CARD, ANYTIME_CARD y AS_SOON_AS_CARD. Esto se usa luego para añadir información a la carta y el color de fondo de la carta de la misma manera que se hace en las cartas físicas del juego.

Otro ejemplo es para el juego "Arcs" en Español

```json
{
    "name": "LUCHA DE GREMIO",
    "description": "**Cuando se asegura:** Puedes robar 1 carta de Gremio de un Rival. Baraja todas las cartas de Gremio de la pila de descarte de la Corte en el mazo de la Corte. Descarta Lucha de Gremio.",
    "id": "30",
    "data": {
        "type": "VOX",
        "references": "Gremio: Guild \n\n\n\n Asegura: Secured"
    }
}
```

Ya que "Arcs" a fecha de hoy no tiene traducción en castellano y el juego sólo se encuentra en inglés, el nodo **"references"** añade algunos significados en el carta física en inglés para un mejor entendimiento de la misma. Los caracteres especiales lo explicamos más adelante en el formato Markdown.

Otro caso es "Gran Austria Hotel" que no necesita información adicional y no tiene nodo **"data"**

```json
{
    "id": "3",
    "name": "Barman",
    "description": "Una volta per round, puoi usare questa carta per ricevere 1 vino"
}
```

### Formato Markdown en la descripción

Puede usar formato Markdown en el caso del nodo **"description"** o tus campos para el nodo **"data"**. Aunque Markdown tiene muchas formas de añadir formato, realmente lo único que tiene sentido dentro de la descripción de la carta es:

- Texto en Negrita: envuelve el texto entre \*\*
- Texto en Cursiva: envuelve el texto entre \*
- Salto de línea: añade \\n\\n\\n\\n

Esto te ayudará a añadir formato a tus descripciones para más claridad del contenido

### Vista final en la aplicación

Aunque el archivo JSON contiene mas nodos para el contenido de la carta, como colores de fondo en el caso de tener cartas de diferentes tipos o mostrar nodos por idiomas, este no es el propósito de este documento. 

Si finalmente te animas a crear un nuevo juego, para buscar cartas de forma sencilla en "Catálogo BGG", yo me encargaré de dar el formato final y lo hablaremos por correo electrónico.
