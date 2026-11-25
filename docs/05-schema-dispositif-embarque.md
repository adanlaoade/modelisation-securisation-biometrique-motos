# Schéma complémentaire : fonctionnement du dispositif embarqué

Ce schéma n'est **pas** un sixième diagramme UML : il résume la chaîne de décision du dispositif.

```mermaid
flowchart TD
    A["Doigt posé"] --> B["Capteur d'empreinte"]
    V["Visage présenté"] --> C["Caméra faciale"]
    B --> U["Unité de traitement"]
    C --> U
    M[("Mémoire sécurisée locale : gabarits chiffrés, autorisations, journaux")] <--> U
    U --> D{"3 contrôles valides ?<br/>empreinte, visage, autorisation locale"}
    D -- oui --> S["Commande de démarrage : démarrage autorisé"]
    D -- non --> R["Refus signalé"]
    S --> J["Journal local"]
    R --> J
    J --> K["Module de communication"]
    K -. "TLS, dès que le réseau est disponible" .-> P["Plateforme : API et base de données"]
    P -. "synchronisation : autorisations et révocations" .-> K
```

## Règles de sûreté
- La commande de démarrage n'intervient **qu'à l'allumage**.
- Elle ne coupe **jamais** un moteur en marche.

## Fonctionnement hors connexion
Sans réseau, le dispositif vérifie localement les gabarits et l'autorisation synchronisée (avec son expiration), conserve les journaux, puis les envoie au retour du réseau.

## Composants physiques (modélisés, simulés)
Capteur d'empreinte · caméra faciale · unité de traitement · mémoire sécurisée locale · module de communication · commande de démarrage (relais) · alimentation protégée sur la batterie de la moto.
