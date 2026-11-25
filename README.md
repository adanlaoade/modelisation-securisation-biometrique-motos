# Modélisation de la sécurisation biométrique des motos à double authentification (empreinte digitale et reconnaissance faciale) pour le campus de l'UNSTIM

> Dossier d'analyse et de conception logicielle — travail académique individuel de génie logiciel.
> Version 1.1 — 26 novembre 2026.

**Mots-clés :** sécurisation des motos · authentification biométrique à deux facteurs · empreinte digitale · reconnaissance faciale · système embarqué · application mobile · autorisations temporaires · UML · architecture en couches.

---

## 1. Contexte

En janvier 2025, l'UNSTIM a enregistré quatre cas de vols de motos. La présidente des étudiants a lancé un hackathon pour concevoir un dispositif qui sécurise chaque moto par **deux facteurs biométriques obligatoires** (empreinte digitale et reconnaissance faciale), couplés à une **autorisation d'accès** gérée par le propriétaire depuis une application mobile.

Le démarrage de la moto n'est autorisé que si :

1. l'empreinte digitale est valide ;
2. le visage est valide ;
3. l'utilisateur dispose d'une autorisation valide (permanente ou temporaire) pour cette moto.

## 2. Nature du projet

Ce dépôt couvre les **trois premières phases du cycle de vie logiciel** :

| Phase | Contenu |
|---|---|
| 1 | Analyse et identification des besoins |
| 2 | Étude de faisabilité et planification |
| 3 | Conception (architecture, base de données, interfaces, scénarios, cinq diagrammes UML) |

Le projet est une **simulation** : aucun matériel n'est fabriqué ni acheté, et **aucun code applicatif** n'est écrit à ce stade. Les composants du dispositif embarqué sont modélisés (conçus et décrits).

## 3. Livrables

| Livrable | Emplacement | État |
|---|---|---|
| Rapport complet (version Markdown) | [`rapport/rapport-complet.md`](rapport/rapport-complet.md) | Disponible |
| Rapport final PDF | `rapport/` | À déposer (voir [`rapport/README.md`](rapport/README.md)) |
| Cinq diagrammes UML (Lucidchart) | [`diagrammes/README.md`](diagrammes/README.md) | Réalisés, liens vérifiés |
| Exports PNG des diagrammes | `diagrammes/images/` | À déposer (voir [`diagrammes/images/LISEZ-MOI.md`](diagrammes/images/LISEZ-MOI.md)) |
| Schéma de la base de données | [`docs/04-schema-base-de-donnees.md`](docs/04-schema-base-de-donnees.md) | Disponible |
| Schéma du dispositif embarqué | [`docs/05-schema-dispositif-embarque.md`](docs/05-schema-dispositif-embarque.md) | Disponible |
| Matrice de traçabilité besoins → conception | [`docs/01-matrice-tracabilite.md`](docs/01-matrice-tracabilite.md) | Disponible |
| Décisions de conception | [`docs/02-decisions-de-conception.md`](docs/02-decisions-de-conception.md) | Disponible |
| Points à corriger avant le rendu | [`docs/03-points-a-corriger-avant-rendu.md`](docs/03-points-a-corriger-avant-rendu.md) | Disponible |

## 4. Les cinq diagrammes UML (Lucidchart)

| N° | Diagramme | Lien modifiable |
|---|---|---|
| 1 | Cas d'utilisation | [Ouvrir](https://lucid.app/lucidchart/9a4ebf0b-6770-41ef-99bb-a27063f30b32/edit) |
| 2 | Classes | [Ouvrir](https://lucid.app/lucidchart/b0ba8773-c643-4c7e-8382-7cc05d71aa14/edit) |
| 3 | Activités | [Ouvrir](https://lucid.app/lucidchart/3e1a5c8b-5b49-432b-8678-06f10d6c99b4/edit) |
| 4 | Composants en couches | [Ouvrir](https://lucid.app/lucidchart/9bd4dd57-efcf-47e6-9494-79717662b0c6/edit) |
| 5 | Séquences | [Ouvrir](https://lucid.app/lucidchart/e92d5f79-ded3-4f4c-b0ed-070367f0af91/edit) |

Les documents appartiennent au compte Lucidchart de l'auteure : pour qu'un tiers (enseignant) les consulte, un lien de partage doit être créé (voir [`diagrammes/README.md`](diagrammes/README.md)).

## 5. Décisions de conception essentielles

- **Deux facteurs biométriques obligatoires** : empreinte **et** visage.
- **Un utilisateur peut être autorisé sur plusieurs motos** (la table `AUTORISATION` relie utilisateurs et motos).
- **Autorisation temporaire** : le dispositif compare l'heure courante aux dates de début et de fin.
- **Révocation** : effective dès que le dispositif a reçu la mise à jour ; limite assumée en mode hors connexion, atténuée par une durée de validité courte de la copie locale.
- **Mode hors connexion** : les autorisations déjà synchronisées sont vérifiées localement, avec leur expiration.
- **Sûreté** : le système ne coupe jamais le moteur d'une moto en circulation (la commande n'agit que sur l'autorisation de démarrage).
- **Protection biométrique** : gabarits chiffrés uniquement, pas d'images brutes conservées.
- **Enrôlement** : réalisé avec les capteurs du dispositif ; les données biométriques internes d'un téléphone ne sont pas exportables.

## 6. Architecture retenue

Trois couches, plus un sous-système embarqué distinct :

- **Présentation** : application mobile du propriétaire, interface d'administration.
- **Traitement** : API REST sécurisée et six modules (comptes, motos, autorisations, authentification biométrique, historique, synchronisation des dispositifs).
- **Données** : base relationnelle et stockage sécurisé des références biométriques.
- **Dispositif embarqué** (un par moto) : capteur d'empreinte, caméra, unité de traitement, mémoire sécurisée locale, module de communication, commande de démarrage, alimentation.

## 7. Organisation du dépôt

```
.
├── README.md                      ← ce fichier
├── CHANGELOG.md                   ← historique des versions
├── rapport/
│   ├── README.md                  ← consignes pour déposer le PDF final
│   └── rapport-complet.md         ← rapport complet (version Markdown)
├── diagrammes/
│   ├── README.md                  ← liens Lucidchart + explication de chaque diagramme
│   └── images/                    ← exports PNG (à déposer)
├── docs/
│   ├── 01-matrice-tracabilite.md
│   ├── 02-decisions-de-conception.md
│   ├── 03-points-a-corriger-avant-rendu.md
│   ├── 04-schema-base-de-donnees.md
│   └── 05-schema-dispositif-embarque.md
└── sources/
    └── enonce-et-exigences.md     ← énoncé du travail et exigences
```

## 8. Démarche

1. Analyse des besoins (acteurs, besoins fonctionnels et non fonctionnels, contraintes, périmètre).
2. Étude de faisabilité (technique, économique, opérationnelle), ressources, risques, planification.
3. Conception en ordre logique : architecture générale → composants physiques → utilisateurs → couches → modules → base de données → interfaces → interactions → scénarios → cinq diagrammes UML → schéma du dispositif embarqué.

## 9. Périmètre

**Inclus :** analyse, faisabilité, planification, conception.
**Exclus :** fabrication ou achat de matériel, programmation de l'application, paiement, géolocalisation, déploiement en production.
**Étape suivante possible :** simulateur du dispositif embarqué, de l'API et de l'application.

## 10. Références

- Cours de génie logiciel et de modélisation UML de l'enseignant (référence principale).
- OMG, *Unified Modeling Language (UML) Specification*.
- Documentation de Lucidchart (Lucid Software).
- ISO/IEC 19794 (formats d'échange de données biométriques) et ISO/IEC 30107 (détection d'attaques de présentation).

## 11. Dépôt

https://github.com/adanlaoade/modelisation-securisation-biometrique-motos
