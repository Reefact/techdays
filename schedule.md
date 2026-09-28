# Tech Days — Planning

## Objectif

Les Tech Days doivent permettre de passer rapidement de sujets techniques parfois encore généraux à une vision concrète, mesurable et exploitable pour la suite.

L'objectif n'est donc pas uniquement de faire émerger des idées ni de consacrer deux jours à du nettoyage de code. Les Tech Days doivent permettre de :

- faire émerger de nouveaux sujets techniques ;
- faire l'état des lieux des sujets déjà identifiés par la communauté et les Working Groups ;
- cartographier leur impact réel sur le patrimoine applicatif ;
- commencer immédiatement les migrations, expérimentations ou POC lorsque c'est possible ;
- mesurer la difficulté réelle, la vitesse d'avancement et les problèmes rencontrés ;
- partager les apprentissages entre les équipes ;
- réduire l'incertitude avant de chiffrer et planifier les chantiers ;
- transformer les résultats en sujets suffisamment qualifiés pour alimenter le backlog technique et les prochains PI.

Le principe général est simple :

> **Identifier → Cartographier → Expérimenter → Mesurer → Consolider → Prioriser**

Le temps consacré aux échanges doit rester limité au nécessaire. Dès qu'un sujet peut être confronté au code ou au patrimoine existant, l'objectif est de le faire concrètement.

---

# Mercredi — Cartographier et commencer à faire

Le mercredi est principalement organisé **par équipe**.

Chaque équipe travaille sur son propre périmètre applicatif et examine l'ensemble des sujets retenus. La cartographie et le travail concret sont réalisés en parallèle : il n'est pas nécessaire d'attendre d'avoir terminé l'inventaire avant de commencer une migration ou un POC.

## 10h00–11h00 — Lancement, état des lieux et brainstorming

### Objectifs

Cette première heure permet d'aligner la communauté avant de commencer le travail.

Elle comprend :

- un rappel rapide du cadre et des objectifs des Tech Days ;
- un état des lieux des précédents Tech Days ;
- un point sur les sujets déjà en cours dans les Working Groups ou dans la communauté ;
- la présentation des sujets déjà identifiés ;
- un brainstorming court pour faire émerger d'éventuels nouveaux sujets ;
- la clarification des résultats attendus pour la journée.

Les sujets déjà connus servent de point de départ, mais ne constituent pas une liste fermée.

L'objectif du brainstorming n'est pas de résoudre les sujets ni de produire immédiatement des fiches détaillées. Il doit simplement permettre d'obtenir une liste suffisamment claire des sujets que les équipes vont confronter à leur patrimoine.

### Exemples de sujets déjà identifiés

- adoption des Conventional Commits et validation dans la CI/CD ;
- adoption de Refit ;
- migration vers `Microsoft.Extensions.Http.Resilience` ;
- abstraction interne pour le dispatch des use cases et remplacement de MediatR ;
- stratégie commune de résilience HTTP : retry, timeout, circuit breaker ;
- état des lieux des mécanismes d'authentification des API ;
- mise en place de Spectral ;
- état des lieux et stratégie de sortie de FluentAssertions.

D'autres sujets peuvent être ajoutés pendant cette première heure ou apparaître au cours des travaux.

---

## 11h00–17h00 — Travail par équipe sur le périmètre applicatif

Chaque équipe travaille sur son propre patrimoine.

Pour chacun des sujets applicables, elle doit mener **deux activités en parallèle** :

1. **cartographier l'existant** ;
2. **agir concrètement lorsque c'est possible**.

### Cartographie

L'objectif est d'obtenir une vision factuelle du périmètre concerné.

Selon le sujet, l'équipe cherche notamment à identifier :

- les applications, services, projets ou repositories concernés ;
- ce qui est déjà conforme ou déjà migré ;
- ce qui reste à traiter ;
- les différentes implémentations actuellement présentes ;
- les cas particuliers ;
- les dépendances ou contraintes identifiées ;
- les zones représentatives pouvant servir de support à une migration ou à un POC.

La cartographie doit autant que possible être basée sur le code et les repositories plutôt que sur la mémoire de l'équipe.

Les développeurs peuvent utiliser tous les moyens utiles : recherche dans les repositories, scripts, analyse des dépendances NuGet, SonarQube, Azure DevOps, outils CLI, etc.

### Migration, expérimentation ou POC

Dès qu'une zone pertinente est identifiée, l'équipe commence à travailler dessus.

Selon le sujet, cela peut prendre différentes formes :

- migration réelle d'une partie du code ;
- mise en conformité ;
- POC ;
- spike technique ;
- modification d'un pipeline ;
- expérimentation d'une librairie ;
- test d'une stratégie de remplacement ;
- automatisation d'une détection ;
- analyse plus poussée d'un cas représentatif.

Le but n'est pas nécessairement de terminer le chantier pendant les Tech Days.

Le travail réalisé doit surtout permettre d'obtenir des informations que la seule cartographie ne fournirait pas :

- vitesse réelle d'avancement ;
- difficulté de migration ;
- quantité de travail manuel ou automatisable ;
- cas particuliers ;
- problèmes inattendus ;
- prérequis ;
- risques ;
- différences entre ce qui semblait simple en théorie et ce qui l'est réellement dans le code.

### Exemple de résultat attendu

Pour un sujet donné, une équipe doit idéalement être capable de produire une synthèse de ce type :

| Élément | Exemple |
| --- | --- |
| Périmètre concerné | 8 projets |
| Déjà conforme | 2 projets |
| À traiter | 6 projets |
| Traité pendant les Tech Days | 2 projets |
| Difficulté observée | faible sur 1, moyenne sur 1 |
| Problèmes rencontrés | configuration spécifique, usage non standard |
| Cas particuliers | 1 projet nécessite une approche différente |
| Première projection | migration majoritairement mécanique, quelques exceptions |

L'objectif n'est pas d'obtenir une précision artificielle, mais de remplacer les suppositions par des observations.

### Attendu à 17h00

À la fin du créneau, chaque équipe doit avoir :

- parcouru les différents sujets sur son périmètre ;
- produit une cartographie aussi complète que possible ;
- commencé les migrations ou POC pertinents ;
- identifié les difficultés et cas particuliers ;
- une première idée de la vitesse d'avancement ;
- identifié les sujets qui peuvent continuer en autonomie ;
- identifié ceux qui nécessitent une aide ou un travail commun avec d'autres équipes ;
- identifié d'éventuels nouveaux sujets apparus pendant l'exploration.

Un champ marqué comme **inconnu** reste une information utile s'il révèle un manque de visibilité qui doit être traité.

---

## 17h00–18h00 — Bilan de la journée et synchronisation inter-équipe

Ce créneau est consacré au partage des résultats du mercredi.

Il ne s'agit pas d'une restitution formelle ni d'une présentation PowerPoint.

Chaque équipe présente rapidement :

- sa cartographie ;
- ce qu'elle a réellement modifié, migré ou expérimenté ;
- son état d'avancement ;
- la vitesse de progression observée lorsque cela a du sens ;
- les difficultés rencontrées ;
- les blocages éventuels ;
- les cas particuliers ;
- les sujets sur lesquels une autre équipe pourrait l'aider.

Les échanges doivent permettre de confronter les expériences.

Une difficulté rencontrée par une équipe peut déjà avoir été résolue par une autre. À l'inverse, un sujet perçu comme simple dans une équipe peut révéler ailleurs des contraintes qui doivent être prises en compte à l'échelle de la communauté.

### Consolidation communautaire

Le bilan doit permettre de commencer à consolider les informations par sujet :

- équipes concernées ;
- volumétrie globale ;
- différentes situations rencontrées ;
- avancement déjà réalisé ;
- problèmes communs ;
- exceptions ;
- solutions déjà testées ;
- questions encore ouvertes.

### Projection sur le jeudi

Le point de 17h00–18h00 sert également à organiser la suite des Tech Days.

À partir des constats de la journée, la communauté identifie :

- les migrations qui peuvent simplement continuer ;
- les sujets nécessitant un POC complémentaire ;
- les problèmes communs à traiter ensemble ;
- les sujets nécessitant un groupe multi-équipe ;
- les sujets nécessitant encore une investigation ;
- les éventuels nouveaux sujets apparus pendant la journée.

À l'issue de ce point, le travail du jeudi doit être suffisamment clair pour constituer rapidement les groupes le lendemain matin.

---

# Jeudi — Approfondir, résoudre et préparer la suite

Contrairement au mercredi, le jeudi n'est pas organisé systématiquement par équipe.

Les groupes sont constitués en fonction de la nature des sujets et de ce qui a été découvert la veille.

Un groupe peut donc être :

- **un groupe d'une même équipe**, travaillant sur un sujet propre à son périmètre ;
- **un groupe POC / spike**, constitué pour valider rapidement une solution ou une hypothèse pour une ou plusieurs équipes ;
- **un groupe multi-équipe**, lorsqu'un sujet touche plusieurs équipes ou nécessite une approche commune ;
- toute autre organisation pertinente permettant d'avancer efficacement sur le sujet.

Le mode d'organisation doit rester au service du problème à résoudre.

---

## 10h00–10h30 — Lancement du jour 2 et constitution des groupes

Le point de départ est la synthèse du mercredi soir.

L'objectif est de :

- rappeler les principaux constats ;
- identifier les sujets à poursuivre ;
- sélectionner les sujets nécessitant un travail spécifique ;
- constituer les groupes adaptés ;
- clarifier ce que chaque groupe cherche à obtenir avant 16h00.

Chaque groupe doit partir avec un objectif suffisamment concret.

Exemples :

- poursuivre une migration commencée mercredi ;
- résoudre un problème rencontré par plusieurs équipes ;
- valider une approche technique avec un POC ;
- comparer deux stratégies ;
- tester la faisabilité d'une migration ;
- approfondir un cas particulier ;
- consolider une volumétrie ;
- préparer une décision technique ;
- obtenir suffisamment d'informations pour découper et chiffrer un chantier.

---

## 10h30–16h00 — Travail par groupe

Ce créneau constitue le cœur de la deuxième journée.

Les groupes gèrent librement leur organisation et leur pause déjeuner.

Selon le sujet, le travail peut inclure :

- poursuite des migrations ;
- résolution de problèmes identifiés la veille ;
- POC ou spike ;
- expérimentation sur un projet représentatif ;
- comparaison d'approches ;
- industrialisation d'une solution ;
- analyse des exceptions ;
- consolidation de la cartographie ;
- mesure de l'effort restant ;
- estimation à partir de la vitesse observée ;
- définition d'une approche commune ;
- préparation d'une décision ou d'un ADR ;
- proposition de découpage en Tech Stories.

L'objectif n'est pas que tous les groupes produisent le même type de résultat.

Un POC réussi, une migration partielle, une cartographie consolidée, une approche invalidée avec des raisons factuelles ou une décision désormais suffisamment instruite constituent tous des résultats utiles.

### Résultat attendu à 16h00

Chaque groupe doit pouvoir expliquer clairement :

- le problème traité ;
- ce qui a été fait ;
- ce qui a été testé ou vérifié ;
- ce qui a été appris ;
- les difficultés rencontrées ;
- ce qui est désormais considéré comme validé ou invalidé ;
- ce qui reste à faire ;
- l'étendue connue du chantier ;
- les éventuelles dépendances ;
- la suite proposée.

Lorsque cela est possible, le groupe doit également être capable de proposer :

- un ordre de grandeur ;
- un découpage ;
- les premières Tech Stories ;
- un ADR si une décision structurante doit être formalisée.

---

## 16h00–16h30 — Consolidation communautaire

Chaque groupe partage brièvement ses résultats.

L'objectif n'est pas de refaire le détail de la journée mais de construire une vision commune.

Chaque restitution doit couvrir au minimum :

- ce qui a été réalisé ;
- ce qui a été appris ;
- les principales difficultés ;
- la conclusion ou décision proposée ;
- le reste à faire ;
- les éventuels points encore ouverts.

Ce point permet également de vérifier que les résultats produits par différents groupes ne sont pas contradictoires et d'identifier les derniers éléments à prendre en compte avant la priorisation.

---

## 16h30–17h30 — Priorisation et préparation du backlog

Le dernier créneau transforme les résultats des deux jours en éléments actionnables.

Pour chaque sujet, la communauté cherche à déterminer :

- si le sujet doit continuer ;
- son niveau de maturité ;
- son périmètre ;
- son importance ;
- son ordre de grandeur ;
- les dépendances connues ;
- l'équipe ou les équipes candidates ;
- le porteur du sujet ;
- le découpage nécessaire ;
- les Tech Stories à créer ;
- les éventuelles décisions ou ADR encore nécessaires.

L'objectif est d'éviter qu'un résultat de Tech Days se termine simplement par :

> « Il faudrait faire X. »

Un sujet retenu doit autant que possible ressortir avec suffisamment d'informations pour pouvoir être compris, priorisé, découpé et intégré au backlog technique.

---

# Résultats attendus à la fin des Tech Days

À la fin du jeudi, la communauté doit disposer de plusieurs niveaux de résultats.

## Vue par équipe

Chaque équipe possède une vision actualisée de son patrimoine sur les sujets étudiés :

- état actuel ;
- éléments déjà conformes ;
- éléments restant à traiter ;
- premières migrations réalisées ;
- cas particuliers ;
- difficultés ;
- ordre de grandeur lorsque celui-ci peut être estimé.

## Vue par sujet

La communauté dispose d'une vision transversale :

- équipes et applications concernées ;
- volumétrie globale ;
- différences d'implémentation ;
- difficultés communes ;
- exceptions ;
- résultats des POC ;
- approche proposée ;
- effort restant.

## Backlog technique

Les sujets suffisamment mûrs sont transformés en éléments actionnables :

- Tech Stories ;
- ADR éventuels ;
- porteurs ;
- équipes candidates ;
- dépendances ;
- ordre de grandeur ;
- priorité proposée.

---

# Synthèse du planning

| Jour | Horaire | Activité |
| --- | --- | --- |
| Mercredi | 10h00–11h00 | Lancement, état des lieux, sujets en cours et brainstorming |
| Mercredi | 11h00–17h00 | Travail par équipe : cartographie + migration / POC en parallèle |
| Mercredi | 17h00–18h00 | Bilan, partage des cartographies, difficultés, entraide et projection |
| Jeudi | 10h00–10h30 | Lancement du jour 2 et constitution des groupes |
| Jeudi | 10h30–16h00 | Travail par groupe : migration, résolution, POC, consolidation, préparation de la suite |
| Jeudi | 16h00–16h30 | Consolidation communautaire |
| Jeudi | 16h30–17h30 | Priorisation et préparation du backlog |

---

# Principe de fonctionnement

Les Tech Days doivent privilégier le concret.

La cartographie permet de comprendre **où** se trouvent les sujets.

La migration et les POC permettent de comprendre **ce qu'ils coûtent réellement**.

Les échanges entre équipes permettent de comprendre **ce qui doit être traité collectivement**.

La consolidation et la priorisation permettent enfin de transformer ces apprentissages en **travail planifiable**.

> **On ne cherche pas seulement à savoir ce qu'il faudrait faire : on profite des Tech Days pour commencer à le faire et apprendre suffisamment pour organiser correctement la suite.**
