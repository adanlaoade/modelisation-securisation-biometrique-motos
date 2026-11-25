# Énoncé et exigences du travail

**Rôle demandé :** ingénieur logiciel (analyse des besoins, architecture, conception, UML). Travail académique **individuel**, à présenter et défendre devant un enseignant de génie logiciel.

**Règle fondamentale :** les enseignements et exigences du professeur sont la référence principale.

## Contexte
En janvier 2025, l'UNSTIM a enregistré quatre vols de motos. Un hackathon vise à concevoir un système de sécurisation biométrique : deux facteurs obligatoires (empreinte digitale + reconnaissance faciale) et une autorisation d'accès valide. Chaque moto a son dispositif embarqué (capteurs, unité de traitement, module de communication, commande de démarrage). Le propriétaire utilise une application mobile (compte, moto, utilisateurs autorisés, autorisations permanentes ou temporaires avec dates et heures, révocation, historique). L'administrateur supervise la plateforme.

## Titre
Doit commencer par « Modélisation de ... ». Mots-clés à identifier.

## Phases demandées
1. **Analyse et identification des besoins** : contexte, problématique, objectifs, acteurs, besoins fonctionnels et non fonctionnels, contraintes, périmètre.
2. **Faisabilité et planification** : technique, économique, opérationnelle, ressources, risques et solutions, planification.
3. **Conception** : architecture générale ; composants physiques ; utilisateurs ; architecture en couches ; modules ; base de données ; interfaces ; interactions ; scénarios ; cinq diagrammes UML ; schéma complémentaire du dispositif embarqué.

## Architecture de référence
Trois couches (Présentation, Traitement, Données) ; dispositif embarqué = sous-système distinct relié à la plateforme.

## Cinq diagrammes UML obligatoires
Cas d'utilisation · classes · activités · composants en couches · séquences. Le schéma du dispositif embarqué n'est pas un sixième diagramme UML.

## Exigences sur les diagrammes
Notation UML respectée, alignements et espacements réguliers, pas de croisements inutiles, textes lisibles, palette sobre. Réalisés **dans Lucidchart**, modifiables, avec liens réels.

## Rapport final (PDF)
Document central et autonome : page de garde, table des matières, introduction, parties hiérarchisées, tableaux, diagrammes lisibles non déformés, conclusion, références, lien du dépôt GitHub.

## Dépôt GitHub
Rapport PDF, documents de travail, analyse et conception, liens et exports des diagrammes, README complet, dossiers propres, versions importantes conservées. Ne jamais affirmer qu'un fichier ou diagramme est publié s'il ne l'est pas.

## Précautions techniques
Deux facteurs obligatoires ; un utilisateur sur plusieurs motos ; autorisations temporaires respectées ; révocation effective après prise en compte ; fonctionnement hors connexion étudié (limite de la révocation) ; jamais de coupure moteur en circulation ; gabarits biométriques protégés (pas d'images brutes non protégées) ; enrôlement avec capteurs compatibles (pas d'export des données biométriques d'un téléphone).

## Hors périmètre
Programmation de l'application.
