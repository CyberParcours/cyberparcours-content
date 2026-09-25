# CyberParcours — Contenu pédagogique

Ce dépôt contient le catalogue pédagogique en français utilisé par l’application mobile **CyberParcours**.

CyberParcours s’adresse aux personnes qui découvrent la cybersécurité. Son objectif est de proposer un parcours clair, progressif et accessible : comprendre les notions essentielles, acquérir de bons réflexes, découvrir les réseaux et se préparer progressivement à un premier challenge pratique de type CTF.

> Ce dépôt contient uniquement le contenu des leçons. Le code source de l’application mobile est conservé séparément.

## Structure du dépôt

```text
cyberparcours-content/
├── lessons_fr.json   # Catalogue français des modules, leçons et quiz
└── README.md
```

Le catalogue public est disponible à cette adresse :

```text
https://raw.githubusercontent.com/CyberParcours/cyberparcours-content/main/lessons_fr.json
```

## Fonctionnement des mises à jour

L’application contient une copie intégrée du catalogue afin de rester utilisable hors connexion.

Lorsqu’une recherche de mises à jour est lancée, l’application :

1. télécharge `lessons_fr.json` depuis ce dépôt ;
2. vérifie la structure et la version du catalogue ;
3. enregistre localement la nouvelle version si elle est valide et plus récente ;
4. conserve la dernière version valide en cas d’erreur réseau ou de fichier incorrect.

Ce système permet d’ajouter ou d’améliorer des leçons sans publier immédiatement une nouvelle version de l’application sur Google Play. Une mise à jour de l’application reste nécessaire si la structure technique du catalogue ou les fonctionnalités de l’application changent.

## Format général du catalogue

```json
{
  "schemaVersion": 1,
  "contentVersion": 1,
  "language": "fr",
  "modules": []
}
```

| Champ | Rôle |
|---|---|
| `schemaVersion` | Version de la structure JSON prise en charge par l’application. |
| `contentVersion` | Version du contenu publié. Elle doit être augmentée à chaque mise à jour. |
| `language` | Langue du catalogue. La valeur actuelle est `fr`. |
| `modules` | Liste ordonnée des modules et de leurs leçons. |
| `id` | Identifiant unique et permanent d’un module, d’une leçon ou d’une question. |
| `content` | Contenu pédagogique complet d’une leçon disponible. |

## Règles de modification

Avant de publier une nouvelle version du catalogue :

- ne jamais modifier les identifiants `id` déjà publiés, car ils servent à conserver la progression des utilisateurs ;
- maintenir un ordre d’apprentissage logique et progressif ;
- expliquer chaque notion avec un vocabulaire adapté aux débutants ;
- éviter les détails qui n’aident pas directement à comprendre la leçon ;
- vérifier que chaque quiz correspond au contenu enseigné ;
- vérifier que chaque `correctIndex` désigne une réponse existante ;
- augmenter `contentVersion` d’une unité ;
- ne modifier `schemaVersion` que si l’application prend en charge la nouvelle structure.

Une leçon planifiée peut apparaître dans le parcours sans champ `content`. Elle ne devient accessible que lorsque son contenu complet et son quiz ont été ajoutés.

## Validation du fichier JSON

Depuis la racine du dépôt :

```bash
python3 -m json.tool lessons_fr.json > /dev/null
```

Si la commande ne retourne aucune erreur, la syntaxe JSON est valide. Il faut ensuite tester le catalogue dans l’application avant sa publication.

## Publication d’une mise à jour

```bash
git add lessons_fr.json
git commit -m "Mise à jour du catalogue CyberParcours"
git push
```

Après le `push`, le fichier brut de GitHub devient la source de mise à jour consultée par l’application.

## Principes pédagogiques

Le parcours CyberParcours doit :

- partir de zéro, sans supposer de connaissances techniques ;
- relier les leçons entre elles pour éviter les sauts de difficulté ;
- présenter la cybersécurité comme un domaine complet, et pas uniquement comme la recherche d’un flag ;
- encourager la curiosité, la pratique responsable et la compréhension ;
- réserver les exercices aux systèmes personnels, laboratoires et environnements explicitement autorisés.

## État du projet

Le premier catalogue comprend **3 modules et 10 leçons planifiées**. Les premières leçons sont progressivement enrichies avant l’ouverture du parcours complet et du premier mini-CTF guidé.

---

Développé avec soin pour rendre la cybersécurité plus accessible aux débutants.
