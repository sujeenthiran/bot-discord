# Bot Discord – structures de données en Python

Bot Discord de modération et d'assistance, réalisé en 1re année à Ynov. L'objectif du projet était d'**implémenter soi-même les structures de données classiques** (liste chaînée, file, arbre, table de hachage) et de les utiliser dans un vrai programme.

![Python](https://img.shields.io/badge/Python-3.9+-3776AB?logo=python&logoColor=white)
![discord.py](https://img.shields.io/badge/discord.py-2.x-5865F2?logo=discord&logoColor=white)

## Structures de données utilisées

| Fichier | Structure | Rôle dans le bot |
|---|---|---|
| `module1.py` | Liste doublement chaînée | Historique des commandes (`$history`, `$last`, `$clear`) |
| `module2.py` | File (FIFO) | File d'attente des commandes exécutées automatiquement |
| `module3.py` | Arbre | Conversation guidée avec le bot (`$tree`, `$reset`) |
| `module4.py` | Table de hachage | Historique par utilisateur (identifiants hachés) |

## Fonctionnalités

- **Modération** : `$ban`, `$deco` (déconnecter un membre du vocal), `$purge`, `$signaler` (envoie un signalement dans un salon dédié)
- **Rôles** : `$role`, `$addrole`, choix de rôles par réaction à l'arrivée d'un membre
- **Salons vocaux** : `$cree`, `$invite`, `$voc_size`
- **Divers** : `$joke` (API JokeAPI), `$myhelp`

## Installation

```bash
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env        # puis remplir DISCORD_TOKEN et SIGNALEMENT_CHANNEL_ID
set -a && source .env && set +a
python bot.py
```

## Sécurité

- Le jeton du bot n'est **jamais écrit dans le code** : il est lu dans la variable d'environnement `DISCORD_TOKEN` (`.env` est ignoré par Git).
- Les commandes de modération (`$ban`, `$purge`, `$role`, `$addrole`, `$deco`) vérifient les permissions Discord de l'utilisateur (ajouté après relecture : avant, n'importe quel membre pouvait s'attribuer un rôle).
- Les identifiants Discord sont hachés avant d'être stockés dans l'historique.

## Ce que j'ai appris

- Implémenter et choisir une structure de données selon le besoin (accès au dernier élément, ordre d'arrivée, arborescence, recherche rapide).
- Programmation asynchrone avec `asyncio` et l'API Discord.
- Gérer un secret (jeton d'API) correctement : variable d'environnement, `.gitignore`, révocation en cas de fuite.
