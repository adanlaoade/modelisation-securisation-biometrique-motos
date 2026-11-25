# Décisions de conception

Chaque décision compare brièvement les options et justifie le choix retenu, dans le contexte d'un projet académique de simulation.

## 1. Architecture logicielle
| Option | Avantages | Inconvénients |
|---|---|---|
| **3 couches (retenue)** | Simple à expliquer et à défendre, conforme à l'architecture de référence, modules clairs | Moins souple qu'une architecture distribuée |
| Microservices | Évolutivité | Complexité excessive pour le périmètre |

**Choix :** 3 couches (Présentation, Traitement, Données) + dispositif embarqué comme sous-système distinct. Seul ajustement : le module de **synchronisation des dispositifs** est isolé dans la couche Traitement car il porte les règles de révocation et d'expiration.

## 2. Base de données
| Option | Avantages | Inconvénients |
|---|---|---|
| **Relationnelle (retenue)** | Données structurées ; relations naturelles propriétaire–moto, moto–autorisation, utilisateur–autorisation ; intégrité par clés | — |
| Documentaire (NoSQL) | Souplesse du schéma | Relations et contraintes d'intégrité moins naturelles ici |

## 3. Où décider du démarrage ?
| Option | Avantages | Inconvénients |
|---|---|---|
| **Décision locale sur le dispositif (retenue)** | Fonctionne sans réseau ; décision en quelques secondes ; données biométriques comparées localement | Révocation non connue d'un dispositif hors connexion |
| Décision côté serveur | Révocation immédiate | Inutilisable sans réseau ; réseau mobile parfois instable |

## 4. Révocation en mode hors connexion
Un dispositif qui n'a pas reçu la mise à jour ne peut pas connaître la révocation. Limite **assumée et documentée**. Atténuation : durée de validité courte de la copie locale d'une autorisation, renouvelée à chaque synchronisation. La durée exacte est un paramètre du simulateur.

## 5. Stockage biométrique
Gabarits (références) **chiffrés** uniquement, jamais d'images brutes conservées. Comparaison locale. L'administrateur n'accède pas aux données biométriques brutes.

## 6. Enrôlement
Réalisé avec les capteurs du dispositif (ou compatibles). Les données biométriques internes d'un téléphone ne sont pas exportables vers les capteurs de la moto.

## 7. Sûreté
La commande de démarrage n'agit que sur l'autorisation d'allumage ; elle ne coupe jamais un moteur déjà en marche.

## Précisions de conception proposées (à valider avant intégration au rapport)
Ces points renforcent la cohérence sans changer l'architecture :

1. **Unicité biométrique** : contrainte d'unicité sur (`id_utilisateur`, `type`) dans `REFERENCE_BIOMETRIQUE`, pour garantir au plus une empreinte et un visage par utilisateur.
2. **Distribution minimale des gabarits** : un dispositif ne reçoit les gabarits chiffrés que des utilisateurs autorisés sur sa moto.
3. **Horloge fiable** : les autorisations temporaires supposent une horloge fiable sur le dispositif (horloge simulée dans le projet) ; une dérive doit conduire au refus ou à une resynchronisation.
4. **Limitation des essais** : nombre d'essais échoués limité avec temporisation, journalisé.
5. **Procédure de secours du propriétaire** : prévue en besoin de fiabilité ; à détailler comme scénario si l'enseignant le demande.
