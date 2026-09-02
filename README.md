# Goûts 100

**Goûts 100** est un test interactif de préférences composé de 100 questions. Il vise à produire une cartographie descriptive des goûts d'une personne à travers plusieurs domaines de la vie quotidienne, puis à synthétiser les réponses selon différentes dimensions transversales.

L'application est contenue dans un unique fichier `index.html` et peut être utilisée directement dans un navigateur ou publiée avec GitHub Pages.

## Principe général

Le test comprend 100 affirmations évaluées sur une échelle de 1 à 5, de « Pas du tout » à « Énormément ».

Les questions couvrent dix domaines :

- Alimentation
- Musique
- Cinéma et séries
- Lecture et culture
- Jeux et divertissement
- Voyage et environnement
- Esthétique et design
- Vie sociale et rythme
- Technologie et usages
- Curiosité et expériences

Les réponses sont ensuite synthétisées sur onze axes transversaux :

- Nouveauté
- Intensité
- Structure
- Sociabilité
- Environnement
- Esthétique
- Technologie
- Rythme
- Culture
- Sensorialité
- Créativité

Le résultat final comprend notamment un profil synthétique, un radar des dimensions principales, des scores par domaine, ainsi que les préférences les plus fortement appréciées ou rejetées.

## Utilisation multi-participants

L'application permet de gérer plusieurs personnes indépendamment.

Avant de commencer, chaque utilisateur peut sélectionner son nom dans la liste disponible ou ajouter un nouveau nom. Une progression distincte est ensuite enregistrée pour chaque participant.

Sur un même ordinateur et dans un même navigateur, plusieurs personnes peuvent donc utiliser successivement le test sans écraser les réponses des autres.

La page **Données** permet également d'ajouter plusieurs noms en une seule fois afin de préparer un répertoire de participants sur un poste partagé.

## Préparer la liste des collègues

Deux méthodes sont disponibles.

### Depuis l'interface

Dans la page **Données**, utiliser **Ajouter plusieurs noms**, saisir un nom par ligne, puis cliquer sur **Copier le lien équipe**. Le lien généré contient la liste des participants ainsi que leurs identifiants internes. Il peut être envoyé aux collègues : lors de l'ouverture du lien, la même liste apparaît dans leur navigateur et chacun peut sélectionner son propre nom.

Le maintien du même identifiant entre les appareils permet d'éviter les doublons lors de l'import ultérieur des fichiers. Si plusieurs versions d'une même session sont présentes, le corpus conserve automatiquement celle qui contient le plus de réponses, puis la plus récente en cas d'égalité.

### Directement dans `index.html`

Une liste peut également être inscrite directement dans le fichier source en modifiant la constante suivante :

```js
const PRESET_PARTICIPANTS = ["Alice", "Bob", "Camille"];
```

Par défaut, elle est vide. Cette méthode est pratique lorsque la liste doit apparaître immédiatement chez toutes les personnes utilisant exactement la même version du site.

## Sauvegarde des réponses

Les données sont enregistrées automatiquement dans le stockage local du navigateur.

Pour chaque participant, l'application conserve notamment :

- un identifiant unique
- le nom ou pseudonyme
- la date de création de la session
- la date de dernière modification
- la date de première réponse
- la date de complétion lorsque les 100 questions sont terminées
- la progression
- les 100 réponses
- les scores des axes transversaux
- les scores des domaines
- le profil synthétique

Une session interrompue peut être reprise ultérieurement depuis le même navigateur.

## Récupération des données des collègues

GitHub Pages étant un hébergement statique, les réponses enregistrées sur l'ordinateur d'un collègue ne peuvent pas être transférées automatiquement vers le navigateur d'une autre personne sans ajouter un serveur ou un service de base de données.

Goûts 100 utilise donc un système d'export et d'import local :

1. Préparer la liste des collègues dans la page **Données** et, idéalement, leur transmettre le **lien équipe**.
2. Chaque collègue ouvre le lien et sélectionne son propre nom.
3. Il complète le test.
4. Il utilise **Exporter mes résultats JSON** depuis la page de résultats.
5. Il transmet le fichier `.json` généré.
6. Les fichiers reçus sont importés simultanément dans la page **Données**.
7. Le corpus complet est ensuite exportable en CSV large, CSV long ou JSON.

Les fichiers importés sont conservés localement dans le navigateur qui réalise l'agrégation.

## Formats d'export du corpus

### CSV large

Le fichier `gouts100_corpus_large.csv` contient une ligne par participant.

Il comprend :

- les métadonnées de session
- le profil synthétique
- les onze scores d'axes
- les dix scores de domaines
- les réponses `Q001` à `Q100`

Ce format est adapté à une lecture directe dans Excel, Jamovi, R, Python ou un logiciel statistique comparable.

### CSV long

Le fichier `gouts100_corpus_long.csv` contient une ligne par participant et par question.

Les principales colonnes sont :

- `participant_id`
- `nom`
- `question_id`
- `domaine`
- `question`
- `reponse`

Ce format est particulièrement utile pour les analyses par item, les transformations de données et les pipelines statistiques.

### JSON

Le corpus peut également être exporté sous forme de fichier `gouts100_corpus.json`, qui conserve la structure complète des sessions et peut être réimporté ultérieurement dans l'application.

## Confidentialité

Aucune donnée n'est envoyée automatiquement vers un serveur externe.

Les réponses restent dans le navigateur tant qu'un export n'est pas volontairement déclenché par l'utilisateur. Aucun compte, cookie publicitaire ou service de suivi externe n'est nécessaire au fonctionnement du test.

Si des noms réels sont utilisés, les fichiers exportés contiennent ces noms. Il est donc possible d'utiliser des pseudonymes si une identification directe n'est pas nécessaire.

## Interprétation

Goûts 100 est un outil ludique et descriptif. Il ne constitue pas un instrument psychométrique validé, un test diagnostique, une mesure clinique ou une mesure scientifique standardisée de la personnalité.

Les résultats décrivent uniquement les réponses fournies au moment de la passation. Ils ne doivent pas être interprétés comme des traits psychologiques stables ou comme une classification définitive d'une personne.

## Installation sur GitHub Pages

Le dépôt peut rester minimal :

```text
/
├── index.html
├── README.md
└── .gitignore
```

Pour publier l'application avec GitHub Pages, il suffit de déposer ces fichiers dans le dépôt puis d'activer GitHub Pages sur la branche utilisée pour le site.

Aucune compilation, installation de dépendance ou configuration de serveur n'est nécessaire.

## `.gitignore`

Le dépôt inclut un `.gitignore` qui exclut les fichiers système, les réglages d'éditeur, les fichiers temporaires et les exports locaux `gouts100_*.json` / `gouts100_*.csv`. Cela évite de publier accidentellement les résultats individuels des participants sur GitHub.

## Compatibilité

L'application fonctionne directement dans les navigateurs web modernes sur ordinateur et mobile. La mise en page est responsive et inclut plusieurs options de personnalisation et d'accessibilité, notamment l'ajustement de la taille du texte, le contraste renforcé et la réduction des animations.

## Licence

Aucune licence n'est imposée par ce README. Une licence peut être ajoutée au dépôt selon les conditions de diffusion souhaitées.
