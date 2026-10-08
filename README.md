# Prépa entretien .NET

Page web d'entraînement destinée aux candidats Carbon qui préparent un entretien technique .NET.

Elle regroupe les thèmes classiques de ces entretiens sous forme de questions dépliables : le candidat lit la question, formule sa réponse, puis déplie pour comparer avec des pistes de réponse.

> Les réponses proposées sont des repères pour structurer sa réflexion, pas un script à apprendre par cœur. Elles doivent être reformulées et reliées à l'expérience de chaque candidat.

## Contenu

| Section | Thèmes abordés |
|---|---|
| Parcours & environnement | Exemples de questions ouvertes sur l'expérience du candidat (sans réponse) |
| Questions .NET | Logging transverse, `CancellationToken`, middlewares et gestion des exceptions |
| Thread safety & montée en charge | Thread safety d'un repository en mémoire, `lock`, passage à plusieurs instances, éviter les `GetAll`, validations avec SQL Server, évolution du repository |
| Modélisation de la base | Tables et colonnes, relation de location, ID interne vs identifiant public, génération d'identifiants |
| Exercices SQL | Requêtes sans IDE (`JOIN`, `GROUP BY`, `HAVING`, tri), `ORDER BY` en sous-requête, agrégats dans un `WHERE`, index, procédures stockées |
| Message brokers | Cas d'usage Kafka / RabbitMQ, patterns Inbox et Outbox |
| Design patterns | Pattern Strategy pour des sources de données multiples |
| Live coding | Endpoint de location, codes HTTP, thread safety d'une opération en plusieurs étapes |

Les exemples s'appuient sur un domaine fictif : une plateforme de location de films (`Movie`, `Director`, `Customer`, `Rental`).

### Page « Questions ouvertes »

Une seconde page, `questions-ouvertes.html`, regroupe des questions complémentaires. Elle n'est pas liée depuis `index.html` : on la transmet au candidat par son URL (`https://carbon-it.github.io/prepa-entretien-dotnet/questions-ouvertes.html`).

| Section | Thèmes abordés |
|---|---|
| Fondamentaux .NET | Durées de vie de l'injection de dépendances (Singleton, Scoped, Transient), ORM, pattern Unit of Work |
| Qualité, tests et architecture | Mesure et outils de performance, tests unitaires vs tests d'intégration, SonarQube, Clean Architecture |
| Observabilité | Propagation du contexte de trace (`traceparent`) à travers un bus de messages |
| Cas pratique Agile | Animation de l'équipe, suivi de son code jusqu'en production, animateur sans Scrum Master, responsabilité en cas de problème |

Sa progression est enregistrée séparément de celle de `index.html`.

## Fonctionnalités

- Recherche plein texte (insensible aux accents)
- Filtres : questions clés, questions à revoir, questions pas encore vues
- Bouton « Question au hasard » qui privilégie les questions non maîtrisées
- Suivi de progression « Je maîtrise » / « À revoir », enregistré dans le navigateur du candidat (`localStorage`). Rien n'est envoyé à un serveur, et la progression n'est pas partagée entre appareils.

## Structure

```
.
├── index.html               # La page principale : HTML, CSS, JavaScript et logo intégrés
├── questions-ouvertes.html  # Questions complémentaires, non liée depuis index.html
└── README.md
```

Chaque page est autonome : aucune dépendance à installer, aucun build. Seules les polices (Figtree, Carlito, JetBrains Mono) sont chargées depuis Google Fonts.

## Consulter la page en local

Ouvrir `index.html` dans un navigateur.

## Mise en ligne (GitHub Pages)

1. Dans le dépôt : **Settings → Pages**
2. Source : **Deploy from a branch**, branche `main`, dossier `/ (root)`, puis **Save**
3. La page est publiée après une ou deux minutes à l'adresse indiquée en haut de la page Settings → Pages (`https://carbon-it.github.io/prepa-entretien-dotnet/`)

Chaque push sur `main` met la page à jour automatiquement.

## Modifier le contenu

Tout se trouve dans `index.html` (ou `questions-ouvertes.html` pour la seconde page). Les deux pages partagent la même structure : les consignes ci-dessous s'appliquent aux deux. Un `data-id` doit être unique au sein d'une page.

- **Ajouter une question** : copier un bloc `<details class="q" data-id="…">` existant dans la section voulue et lui donner un `data-id` unique. Ce `data-id` sert de clé pour la progression des candidats : ne pas le modifier sur une question existante, sinon la progression associée est perdue.
- **Marquer une question comme clé** : ajouter l'attribut `data-hot` sur la balise `<details>`.
- **Ajouter une section** : copier un bloc `<section class="block" id="…" data-title="…">`. Le sommaire latéral se génère automatiquement à partir de `data-title`.
- **Charte graphique** : les couleurs Carbon sont définies dans le bloc `:root` en tête du `<style>`.

## Confidentialité

- Le contenu est volontairement générique : aucune mention de client, et l'exercice illustré est fictif.
- Même si le dépôt est privé, une page GitHub Pages est accessible à toute personne qui en connaît l'URL. Ne rien y ajouter qui ne puisse pas être partagé avec un candidat externe.
- La page contient une balise `noindex, nofollow` pour éviter son indexation par les moteurs de recherche.
