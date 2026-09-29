# Industrial Robotic Cell — AutoSpé 5

> Cellule pédagogique intégrant convoyage, vision industrielle, automate Siemens et robot Stäubli pour détecter, localiser puis manipuler des Kaplas.  
> **English version below.**

## Contexte

Projet académique réalisé en binôme (**Samy Hammadi / Richard Alexis**) afin d'intégrer automatisme, communication industrielle, vision, robotique et IHM.

## Fonctionnement

`Kapla → convoyeur → détection → caméra SensoPart → X / Y / angle → automate Siemens → robot Stäubli → prise → construction d'une tour`

1. L'automate commande le tapis.
2. Un capteur détecte le Kapla et le tapis positionne la pièce sous la caméra.
3. La caméra SensoPart est déclenchée et transmet X, Y, l'angle et le numéro d'image via **PROFINET**.
4. L'automate convertit les données puis les transmet au robot.
5. Le programme robot met à jour un point de référence, saisit la pièce puis la dépose dans la tour.
6. Des acquittements automate ↔ robot synchronisent les étapes.

## Calibration vision / robot

Une grille de calibration 15×13 de 200 mm a été utilisée pour faire correspondre le repère caméra au repère world du robot. Des points ont été comparés entre la caméra et le robot pour vérifier la cohérence des coordonnées. Un offset Z de 5 mm a ensuite été réglé pour le plan observé.

## Éléments fournis / préconfigurés

Le projet n'a pas été construit à partir d'une cellule vide. Le rapport indique explicitement que l'environnement **TIA Portal était préconfiguré**, avec la **communication et la safety déjà en place**.

La cellule et ses équipements industriels existaient également comme support pédagogique.

## Travail réalisé pendant le projet

Le rapport documente notamment :
- configuration du programme de vision SensoPart et du modèle de Kapla ;
- réglages d'exposition/gain ;
- calibration caméra ↔ robot ;
- définition de la trame PROFINET caméra → automate ;
- récupération et conversion des coordonnées ;
- variables d'échange automate ↔ robot ;
- programmes **Ladder** pour les échanges et conditions du GRAFCET ;
- programme robot **VAL3** : lecture des positions, prise, déplacement et dépôt ;
- GRAFCET de coordination du cycle ;
- mécanisme d'acquittements `start_rob`, `start_roback`, `pieceprise`, `piecepriseack` ;
- IHM tapis/caméra ;
- essais et corrections de synchronisation/calibration.

## Technologies

**Siemens · TIA Portal · PROFINET · SensoPart · vision industrielle · Stäubli · VAL3 · Ladder · GRAFCET · IHM · variateur · convoyeur**

## Résultats

Le rapport final indique qu'un cycle complet transporte le Kapla, détermine sa pose, transmet les données au robot puis permet la prise et le dépôt pour construire la tour.

Une optimisation testée consiste à préparer le Kapla suivant pendant que le robot termine le dépôt du précédent, tout en utilisant les acquittements pour conserver la synchronisation.

## Limites

La synchronisation robot/automate et la calibration restaient des axes d'amélioration. Le rapport mentionne notamment des incohérences d'échange rencontrées pendant l'intégration.

Les captures contenant des adresses réseau ou des détails de configuration ne sont volontairement pas publiées telles quelles.

---

# English version

Academic two-person industrial robotics project combining a conveyor, **SensoPart machine vision**, a **Siemens PLC over PROFINET** and a **Stäubli robot**.

The conveyor positions a Kapla under the camera. The camera returns X/Y coordinates, rotation angle and an image number to the PLC. The PLC converts and forwards the relevant data to the robot. A VAL3 program updates the robot reference point, picks the part and places it as part of a tower-building cycle.

### Scope clarification

The TIA Portal environment, communication layer and safety configuration were already provided/preconfigured. Our work focused on system integration: camera setup and calibration, data exchange, Ladder logic, robot variables/programming, GRAFCET sequencing, HMI and synchronization tests.

**Stack:** Siemens · TIA Portal · PROFINET · SensoPart · Stäubli · VAL3 · Ladder · GRAFCET · HMI
