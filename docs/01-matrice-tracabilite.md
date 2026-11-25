# Matrice de traçabilité : besoins → modules → diagrammes

Objectif : montrer que chaque besoin fonctionnel (BF) est pris en charge par au moins un module et représenté dans la conception.
À vérifier avec les diagrammes Lucidchart avant le rendu final.

| Besoin | Intitulé | Module(s) ou composant(s) responsable(s) | Diagrammes principalement concernés |
|---|---|---|---|
| BF1 | Créer et gérer un compte | Gestion des comptes | Cas d'utilisation, classes, composants |
| BF2 | Enregistrer une moto et l'associer à son dispositif | Gestion des motos | Cas d'utilisation, classes, composants |
| BF3 | Enrôler empreintes et visages avec des capteurs compatibles | Authentification biométrique ; dispositif embarqué | Cas d'utilisation, classes, composants |
| BF4 | Ajouter plusieurs utilisateurs autorisés | Gestion des autorisations | Cas d'utilisation, classes |
| BF5 | Autorisation permanente ou temporaire (dates et heures) | Gestion des autorisations | Cas d'utilisation (extension « Définir la période de validité »), classes (`estValide(instant)`) |
| BF6 | Révoquer une autorisation | Gestion des autorisations ; synchronisation | Cas d'utilisation, classes, composants |
| BF7 | Vérifier empreinte, visage et autorisation avant démarrage | Dispositif embarqué ; authentification biométrique | Cas d'utilisation (inclusions), activités, séquences |
| BF8 | Autoriser le démarrage seulement si les trois contrôles réussissent | Dispositif embarqué (commande de démarrage) | Activités, séquences |
| BF9 | Journaliser chaque tentative d'accès | Historique et journalisation ; dispositif embarqué | Activités, séquences, classes (Tentative d'accès) |
| BF10 | Consulter l'historique | Historique et journalisation ; application mobile | Cas d'utilisation, composants |
| BF11 | Synchroniser autorisations et dispositifs | Synchronisation des dispositifs ; module de communication | Composants, séquences (envoi optionnel de la tentative) |
| BF12 | Superviser la plateforme | Interface d'administration | Cas d'utilisation, composants |
| BF13 | Autoriser un même utilisateur sur plusieurs motos | Gestion des autorisations (table `AUTORISATION`) | Classes, base de données |

## Exigences non fonctionnelles clés

| Exigence | Où elle est traitée |
|---|---|
| Sécurité (TLS, chiffrement des gabarits, limitation des essais) | Rapport 2.5 ; règles de conception 4.12 ; diagramme de composants (liaison TLS) |
| Confidentialité (gabarits, pas d'images brutes) | Rapport 4.6 et 4.12 |
| Disponibilité hors connexion | Rapport 4.9 (scénario 5) et 4.12 ; diagramme de séquences (note, fragment `opt`) |
| Sûreté (jamais de coupure moteur en circulation) | Rapport 3.5 et 4.12 ; schéma du dispositif |
| Traçabilité (journaux horodatés) | Table `TENTATIVE_ACCES` ; module Historique |
