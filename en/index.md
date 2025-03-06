# BGG Catalog Multi-Language Board Game Card System Documentation

This repository provides detailed documentation on how to create multi-language board game card files for the "BGG Catalog" application, a board game app available on Android and iOS.

## About BGG Catalog

"BGG Catalog" is an application designed to help users manage and score their board games. The app is available on both Android and iOS platforms.

- Available on [Android](https://bit.ly/3oYT9HU)
- Available on [iPhone and iPad](https://apple.co/3f9ARRG)

## Why this repository

This repository shows how to create a multi-language board game card file for the "BGG Catalog" application. The files are in JSON format, don't worry if you are not a programmer, as they are very easy to work with.

Also this repository contains files for games that are already available in "BGG Catalog", so you will be able to:

- Create new translations for existing games
- Review translations of current games
- Create a new file for another game

Translation files must be in English to be uploaded to the application, plus any language you want to add.

## How to contribute

Just look at the documentation and send me the translation file to gadestudios@gmail.com, but first contact me to see if there is someone else doing it and not to duplicate efforts ;-)

When you send me the mail:

- You can do it in English or Spanish
- The subject should start with "CARDS - " and add the game name

## Documentation

Below is a detailed explanation of the JSON file nodes for translating the cards.

### General Structure

The file has the following structure (this is an example from A Feast for Odin):

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

A JSON file contains **key-value** nodes. The **key** does not change and specifies what the **value** means, which does change with the specific language data. We will always have a main node called **"translations"** that contains all translations. The **lang** node tells us the language of the cards, which can be: "en", "es", "it", etc. The **cards** node contains the list of cards in that language. For example, if we have multiple languages, it would look like this:

```json
{
    "translations": [
        {
            "lang": "en",
            "cards": [
                ... list of cards ....
            ]
        },
        {
            "lang": "es",
            "cards": [
                ... list of cards ....
            ]
        },
        {
            "lang": "it",
            "cards": [
                ... list of cards ....
            ]
        }
    ]
}
```

### Information on Each Card

As mentioned, the **"cards"** node will contain all the cards, so each language must have a node for each card in the game, like the following:

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

The **"id"**, **"name"**, and **"description"** nodes are MANDATORY, so they must always be present in the card.

- The **id** node must have a unique value for the card; usually, it will be a number or a unique identifier. In the rare case that one does not exist, assign an ascending number to each identifier.
- The **"name"** and **"description"** nodes contain the card's information.

The **data** node is a bit special as it may or may not exist, and the information is specific to each game, allowing you to add the details you find relevant for the game.

#### Examples of the data node

For example, in "A Feast for Odin," the **type** field can be: EACH_TIME_CARD, IMMEDIATE_CARD, ANYTIME_CARD, and AS_SOON_AS_CARD. This is later used to add information to the card and determine the background color, similar to how it is done in the physical cards of the game.

Another example is for the game "Arcs" in Spanish:

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

Since "Arcs" does not currently have a Spanish translation and the game is only available in English, the **"references"** node adds some meanings from the physical card in English for better understanding. Special characters will be explained later in the Markdown format section.

Another case is "Grand Austria Hotel," which does not require additional information and lacks a **"data"** node:

```json
{
    "id": "3",
    "name": "Barman",
    "description": "Una volta per round, puoi usare questa carta per ricevere 1 vino"
}
```

### Markdown Format in Descriptions

You can use Markdown formatting in the **"description"** node or your fields for the **"data"** node. Although Markdown offers many formatting options, only the following make sense within the card description:

- Bold Text: wrap the text with **
- Italic Text: wrap the text with *
- Line Break: add \n\n\n\n

This will help format your descriptions for better content clarity.

### Final View in the Application

Although the JSON file contains more nodes for the card content, such as background colors for different card types or displaying nodes by language, that is not the purpose of this document.

If you decide to create a new game, to easily search for cards in the "BGG Catalog," I will handle the final formatting, and we can discuss it via email.


