# Plan comptable général (JSON)

## Informations
Le plan des comptes complet au format **JSON**.

Les données sont répliquées depuis le Plan Comptable Général (PCG) français émis chaque année par l'[Autorité des Normes Comptables](https://www.anc.gouv.fr/sites/anc/accueil.html) (ANC).


## Sources
| Version | Source ANC                                                                                                                                                       | Document                         |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------- |
| 2024    | [Lien](https://www.anc.gouv.fr/files/live/sites/anc/files/contributed/ANC/1_Normes_fran%c3%a7aises/Reglements/Recueils/PCG_Janvier2024/PCG-01-01-2024.pdf)       | [Lien](sources/pcg_20240101.pdf) |
| 2023    | [Lien](https://www.anc.gouv.fr/files/live/sites/anc/files/contributed/ANC/1_Normes_fran%c3%a7aises/Reglements/Recueils/PCG_Janvier2023/PCG_1er-janvier-2023.pdf) | [Lien](sources/pcg_20230101.pdf) |


## Structure
Les différentes versions sont à retrouver dans le dossier *versions*. Chaque fichier **JSON** prend la forme d'une liste d'élements dont la structure est la suivante :
| Clé        | Type                                 | Description                                                                                                                                                                                                                                                                                                                                                                    |
| ---------- | ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `number`   | `int`                                | Le numéro du compte.                                                                                                                                                                                                                                                                                                                                                           |
| `label`    | `string`                             | Le libellé du compte.                                                                                                                                                                                                                                                                                                                                                          |
| `system`   | `"condensed"` `"base"` `"developed"` | Le système minimal dans lequel s'inscrit le compte. <br/> `condensed` si le compte est dans le système abrégé. <br/> `base` si le compte est dans le système de base. <br/> `developed` si le compte est dans le système développé. Notez bien que le système développé contient tous les comptes du système de base qui contient lui-même tous les comptes du système abrégé. |
| `accounts` | `array`                              | La liste des sous-comptes, reprenant la même structure de manière récursive.                                                                                                                                                                                                                                                                                                   |

## Extrait
```js
[
    {
        "number": 1,
        "label": "Capitaux",
        "system": "condensed",
        "accounts": [
            {
                "number": 10,
                "label": "Capital et réserves",
                "system": "base",
                "accounts": [
                    {
                        "number": 101,
                        "label": "Capital",
                        "system": "condensed",
                        "accounts": [
                            {
                                "number": 1011,
                                "label": "Capital souscrit - non appelé",
                                "system": "developed",
                                "accounts": []
                            },
                            ...
                        ]
                    },
                    ...
                ]
            },
            ...
        ]
    },
    ...
]
```
