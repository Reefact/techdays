# Tech Days — Fiches des sujets

## Principes communs

Chaque sujet des Tech Days doit produire **plus que du code** et **plus qu'une analyse**.

Le résultat attendu combine autant que possible :

1. **une cartographie de l'existant** ;
2. **une expérimentation concrète dans le code** ;
3. **des constats factuels** sur la faisabilité, la difficulté et les cas particuliers ;
4. **une mesure du chantier restant** ;
5. **des éléments de décision** lorsqu'un choix technique est nécessaire ;
6. **un backlog exploitable** pour la suite : Tech Stories, ADR/IDR, dépendances, prérequis, équipes concernées, ordre de grandeur.

Le code produit pendant les Tech Days sert donc à deux choses :

- apporter une amélioration immédiate lorsque cela est possible ;
- confronter l'idée au réel pour faire apparaître les difficultés, exceptions et besoins qui devront être ajoutés au backlog.

Un sujet ne doit pas se terminer uniquement par « il faudrait faire X ».

Il doit idéalement permettre de répondre à :

> Où sommes-nous aujourd'hui ? Qu'avons-nous essayé ? Qu'avons-nous appris ? Qu'est-ce qui fonctionne ? Qu'est-ce qui bloque ? Quelle est l'étendue du chantier ? Que faut-il maintenant mettre au backlog ?

---

# 1. Conventional Commits

## Objectif

Adopter une convention commune de messages de commit et mettre en place son enforcement afin de ne pas faire reposer son respect uniquement sur la discipline individuelle.

## Format Tech Days recommandé

**Travail par équipe le mercredi**, puis consolidation commune si plusieurs solutions ou difficultés apparaissent.

## Travail attendu

Chaque équipe :

- vérifie l'état actuel de ses repositories ;
- identifie les éventuelles conventions déjà utilisées ;
- teste une solution de validation des messages de commit ;
- met en place un POC sur au moins un repository représentatif ;
- vérifie le comportement local et dans la CI/CD ;
- identifie les cas particuliers : merge commits, squash, commits automatisés, branches legacy, etc.

## Preuve de faisabilité

Au moins un repository doit disposer d'un mécanisme réellement exécutable permettant de détecter un message de commit non conforme.

## À mesurer / cartographier

- nombre de repositories concernés ;
- repositories déjà conformes ;
- mécanismes de merge utilisés ;
- contraintes particulières de pipeline ;
- effort de généralisation.

## Sorties backlog attendues

- solution technique retenue ou options à arbitrer ;
- règles à appliquer ;
- éventuelles exceptions documentées ;
- Tech Stories de généralisation ;
- travail CI/CD transverse si nécessaire ;
- mise à jour éventuelle de la Definition of Done.

---

# 2. Adoption de Refit

## Objectif

Évaluer et commencer l'adoption de Refit pour les consommateurs HTTP qui utilisent aujourd'hui des implémentations plus manuelles.

## Format Tech Days recommandé

**Cartographie par équipe + migration réelle** le mercredi.

Un groupe spécifique peut poursuivre le jeudi si des difficultés communes ou des cas représentatifs nécessitent une investigation supplémentaire.

## Travail attendu

Chaque équipe :

- recense ses consommateurs HTTP ;
- identifie ceux utilisant déjà Refit et ceux utilisant d'autres approches ;
- choisit un cas représentatif ;
- migre réellement une partie du code ;
- observe la quantité de boilerplate supprimée ;
- relève les problématiques rencontrées : erreurs HTTP, sérialisation, auth, tests, interfaces, configuration, etc.

## Preuve de faisabilité

Au moins un appel HTTP existant doit être migré et fonctionner avec Refit sur un projet réel.

## À mesurer / cartographier

- nombre de clients HTTP ;
- répartition Refit / HttpClient manuel / clients générés / autres ;
- volume restant à migrer ;
- cas simples vs cas particuliers ;
- vitesse de migration observée.

## Sorties backlog attendues

- cartographie globale ;
- exemples de migration ;
- problèmes identifiés ;
- conventions d'usage à définir ;
- Tech Stories de migration ;
- éventuelles décisions complémentaires sur erreurs, auth, observabilité ou génération de clients.

---

# 3. Microsoft.Extensions.Http.Resilience

## Objectif

Adopter `Microsoft.Extensions.Http.Resilience` et mesurer le chantier de migration depuis les mécanismes existants, notamment `Microsoft.Extensions.Http.Polly`.

## Format Tech Days recommandé

**Cartographie + migration par équipe**, avec groupe multi-équipe le jeudi si les stratégies divergent ou si des cas complexes apparaissent.

## Travail attendu

- identifier les projets utilisant Polly, Http.Resilience ou aucun mécanisme explicite ;
- migrer un ou plusieurs cas représentatifs ;
- vérifier l'impact sur la configuration et les tests ;
- identifier les différences de comportement ;
- relever les limitations ou adaptations nécessaires.

## Preuve de faisabilité

Une migration réelle doit être effectuée et vérifiée sur au moins un consommateur HTTP.

## À mesurer / cartographier

- nombre de projets concernés ;
- mécanismes actuels ;
- volume de configuration existante ;
- difficulté de migration ;
- cas particuliers.

## Sorties backlog attendues

- stratégie de migration ;
- conventions communes à définir ;
- Tech Stories par projet / équipe ;
- éventuels sujets complémentaires de résilience.

---

# 4. Stratégie commune de résilience HTTP

## Objectif

Définir une approche cohérente concernant notamment :

- retry ;
- timeout ;
- circuit breaker.

Le sujet porte sur la **stratégie commune**, pas uniquement sur la bibliothèque utilisée.

## Format Tech Days recommandé

**Atelier transverse / multi-équipe** le jeudi.

## Travail attendu

- comparer les stratégies actuellement en place ;
- identifier les cas réellement rencontrés ;
- tester certaines configurations sur des consommateurs représentatifs ;
- observer les impacts et comportements ;
- identifier les situations où une politique unique serait inadaptée.

## Preuve de faisabilité

Une ou plusieurs stratégies candidates doivent être testées sur du code réel.

## À mesurer / cartographier

- politiques actuelles ;
- divergences entre équipes ;
- types de dépendances externes ;
- cas où le retry est ou non pertinent ;
- contraintes particulières.

## Sorties backlog attendues

- décision à formaliser ;
- ADR/IDR éventuel ;
- conventions communes ;
- éventuels profils de résilience selon les usages ;
- Tech Stories de mise en conformité.

---

# 5. Abstraction interne de dispatch des use cases

## Objectif

Évaluer et introduire une abstraction interne pour dispatcher les use cases en remplacement de MediatR.

## Format Tech Days recommandé

**POC ciblé**, idéalement sur un vrai use case.

## Travail attendu

- identifier les usages actuels de MediatR ;
- choisir un cas représentatif ;
- implémenter le dispatch avec l'abstraction candidate ;
- vérifier les impacts sur handlers, pipelines / behaviors, DI, tests et observabilité ;
- identifier les fonctionnalités MediatR réellement utilisées et celles qu'il faudrait reproduire ou abandonner.

## Preuve de faisabilité

Un use case réel doit fonctionner sans MediatR avec l'abstraction proposée.

## À mesurer / cartographier

- projets utilisant MediatR ;
- fonctionnalités utilisées ;
- nombre approximatif de handlers ;
- dépendances implicites à MediatR ;
- difficulté de migration.

## Sorties backlog attendues

- API minimale de l'abstraction ;
- fonctionnalités nécessaires ;
- écarts avec MediatR ;
- Tech Stories de migration ;
- ADR/IDR si la décision est structurante.

---

# 6. Authentification des API

## Objectif

Comprendre les mécanismes d'authentification réellement utilisés afin de préparer une harmonisation.

## Format Tech Days recommandé

**Cartographie par équipe le mercredi**, puis éventuellement atelier transverse le jeudi.

## Travail attendu

- identifier les mécanismes utilisés par les API ;
- identifier les mécanismes utilisés par les consommateurs ;
- relever les variantes, exceptions et dépendances ;
- documenter les flux représentatifs ;
- si pertinent, tester une approche candidate sur un cas limité.

## Preuve de faisabilité

La priorité est d'abord la cartographie. Un POC n'est pertinent que si une hypothèse suffisamment claire ressort de l'état des lieux.

## À mesurer / cartographier

- mécanismes présents ;
- nombre d'API concernées ;
- dépendances techniques ;
- différences entre équipes ;
- cas legacy.

## Sorties backlog attendues

- cartographie consolidée ;
- problèmes communs ;
- points nécessitant une décision ;
- éventuel atelier / ADR à planifier ;
- Tech Stories si certaines harmonisations sont déjà évidentes.

---

# 7. Spectral

## Objectif

Valider la mise en place de Spectral pour le lint des contrats OpenAPI et mesurer la complexité de généralisation.

## Format Tech Days recommandé

**POC concret sur une API réelle**.

## Travail attendu

- exécuter Spectral sur un artefact OpenAPI ;
- définir ou tester un premier ruleset ;
- intégrer le contrôle localement ;
- intégrer si possible le contrôle dans la CI/CD ;
- observer le volume et la nature des violations ;
- identifier les règles trop bruitées ou inapplicables ;
- mesurer le travail nécessaire pour mettre une API existante en conformité.

## Preuve de faisabilité

Le lint doit fonctionner réellement sur au moins une API, idéalement localement et dans la CI.

## À mesurer / cartographier

- nombre d'API ;
- disponibilité des artefacts OpenAPI ;
- violations détectées ;
- règles applicables ;
- effort de mise en conformité.

## Sorties backlog attendues

- ruleset initial ;
- mode d'intégration proposé ;
- règles à discuter ou valider ;
- Tech Stories de généralisation ;
- éventuelles exceptions / dérogations documentées.

---

# 8. Sortie de FluentAssertions

## Objectif

Obtenir une vision complète de l'usage de FluentAssertions et tester concrètement les stratégies possibles de migration.

## Format Tech Days recommandé

**Cartographie par équipe + migrations expérimentales**.

## Travail attendu

- recenser les projets concernés ;
- identifier les versions utilisées ;
- repérer les usages dominants et les usages avancés ;
- migrer plusieurs exemples représentatifs ;
- distinguer les migrations mécaniques des cas nécessitant une réécriture ;
- mesurer la faisabilité d'une automatisation.

## Preuve de faisabilité

Des tests réels doivent être migrés vers une ou plusieurs alternatives candidates.

## À mesurer / cartographier

- projets concernés ;
- volumétrie approximative ;
- patterns d'assertions ;
- cas avancés ;
- vitesse de migration ;
- part automatisable.

## Sorties backlog attendues

- cartographie complète ;
- options de migration ;
- résultats comparatifs ;
- ADR éventuel sur la cible ;
- Tech Stories de migration ;
- besoins d'outillage éventuels.

---

# 9. Mise à jour de la Definition of Done par squad

## Objectif

Mettre à jour la Definition of Done de chaque squad pour refléter les pratiques techniques réellement attendues.

## Format Tech Days recommandé

**Travail par équipe**.

## Travail attendu

Chaque équipe :

- relit sa DoD actuelle ;
- identifie les pratiques absentes, obsolètes ou non vérifiables ;
- la confronte aux sujets travaillés pendant les Tech Days ;
- distingue les règles pouvant être automatisées des règles nécessitant encore une vérification humaine ;
- propose une DoD mise à jour.

## Preuve de faisabilité

Lorsque la DoD contient une règle automatisable, l'équipe doit essayer de la rattacher à un mécanisme concret : build, test, analyzer, CI, lint, etc.

## À mesurer / cartographier

- DoD existante ou absente ;
- divergences entre squads ;
- règles purement déclaratives ;
- règles déjà automatisées ;
- règles encore non enforceables.

## Sorties backlog attendues

- DoD mise à jour par squad ;
- règles communes candidates à une DoD communautaire ;
- backlog d'automatisation des règles non encore enforceables.

---

# 10. Logging

## Objectif

Améliorer la qualité des logs et converger vers l'usage standard de `ILogger`.

Les axes identifiés sont :

- utiliser `ILogger` au lieu de `Log4Ntf` ;
- utiliser les catégories `ILogger<T>` de manière exploitable ;
- supprimer les logs inutiles ;
- utiliser correctement les niveaux de logs ;
- ajouter des logs pertinents et templatisés ;
- supprimer `Extralogs`.

## Format Tech Days recommandé

**Cartographie + refactoring concret par équipe**.

Un atelier transverse peut être constitué si les équipes rencontrent des problématiques communes ou si des conventions doivent être décidées.

## Travail attendu

- identifier les usages de `Log4Ntf`, `ILogger` et `Extralogs` ;
- identifier les logs inutiles ou mal nivelés ;
- sélectionner un flux représentatif ;
- migrer / nettoyer réellement ce flux ;
- vérifier le rendu et les catégories obtenues ;
- tester le filtrage par catégories et niveaux ;
- identifier les informations réellement utiles à l'exploitation.

## Preuve de faisabilité

Un flux réel doit être migré ou nettoyé, avec un résultat observable dans les logs.

## À mesurer / cartographier

- technologies utilisées ;
- volume d'usages legacy ;
- catégories existantes ;
- niveaux incohérents ;
- usages d'`Extralogs` ;
- principaux patterns de logs non structurés.

## Sorties backlog attendues

- conventions de logging à formaliser ;
- backlog de migration ;
- suppressions à effectuer ;
- règles de niveau / catégories ;
- éventuels analyzers ou contrôles automatisés à étudier.

---

# 11. Value Objects

## Objectif

Identifier des concepts qui gagneraient réellement à être modélisés sous forme de Value Objects et valider leurs bénéfices sur du code existant.

Le but n'est pas de créer des Value Objects artificiellement.

## Format Tech Days recommandé

**Atelier dédié**, potentiellement multi-équipe.

## Travail attendu

- analyser plusieurs zones métier ;
- identifier des primitives ou structures portant une vraie sémantique métier ;
- sélectionner quelques candidats ;
- expliciter les invariants associés ;
- implémenter un ou deux Value Objects ;
- adapter un flux réel pour les utiliser ;
- observer les impacts sur validation, lisibilité, erreurs et tests.

## Preuve de faisabilité

Au moins un Value Object doit être utilisé réellement dans un flux métier représentatif.

## À mesurer / cartographier

- concepts candidats ;
- invariants actuellement dispersés ;
- duplications de validation ;
- impacts sur contrats, persistence et sérialisation ;
- bénéfices et coûts observés.

## Sorties backlog attendues

- liste priorisée de Value Objects candidats ;
- critères permettant de reconnaître un bon candidat ;
- Tech Stories d'introduction progressive ;
- éventuels besoins d'outillage ou conventions.

---

# 12. Documentation dans le code

## Objectif

Faire de la documentation technique un élément versionné avec le code et proche du système qu'elle décrit.

## Format Tech Days recommandé

**Travail par équipe**.

## Travail attendu

Chaque équipe :

- ajoute un projet / espace de documentation à son repository ;
- définit une structure minimale ;
- y place au moins un contenu utile et réel ;
- identifie les documents existants qui pourraient être rapprochés du code ;
- teste la facilité de consultation et de maintenance.

## Preuve de faisabilité

Le repository doit contenir une première documentation réelle, versionnée et reliée au code.

## À mesurer / cartographier

- repositories disposant déjà de documentation ;
- emplacement actuel des documents ;
- documentation obsolète ou dispersée ;
- besoins communs de structure.

## Sorties backlog attendues

- structure minimale commune ;
- conventions de documentation ;
- documents à migrer ;
- backlog de documentation manquante ;
- éventuels futurs sujets de living documentation.

---

# 13. IDR — Important Decision Records

## Objectif

Identifier les décisions techniques importantes prises récemment ou à venir et commencer à les formaliser au plus près du code.

## Format Tech Days recommandé

**Travail par équipe**, directement dans le projet de documentation.

## Travail attendu

Chaque équipe :

- identifie les décisions significatives récentes ;
- identifie les décisions importantes à venir ;
- sélectionne au moins une décision suffisamment structurante ;
- la formalise sous forme d'IDR ;
- documente le contexte, les options, la décision et ses conséquences.

Exemples possibles : HATEOAS, stratégie de résilience, remplacement d'une bibliothèque structurante, choix d'architecture, stratégie d'authentification.

## Preuve de faisabilité

Au moins un IDR réel doit être créé par une équipe ayant une décision pertinente à documenter.

## À mesurer / cartographier

- décisions importantes non documentées ;
- décisions à venir ;
- sujets nécessitant encore une expérimentation ;
- liens avec les autres chantiers Tech Days.

## Sorties backlog attendues

- IDR créés ;
- décisions à instruire ;
- POC ou analyses nécessaires avant décision ;
- Tech Stories issues des décisions prises.

---

# 14. Enforcement du style de code

## Objectif

Définir des règles de style communes et valider un mécanisme d'enforcement automatisé.

Le point de départ est le guide :

`Reefact/guidelines/guide-formattage-donet.md`.

Le principe proposé dans ce guide est de centraliser les règles dans `.editorconfig`, de privilégier les règles automatiquement corrigeables par `dotnet format`, puis d'utiliser l'éditeur, un hook local, le build et la CI comme niveaux successifs d'application.

## Format Tech Days recommandé

**Atelier transverse**, avec un repository pilote.

## Travail attendu

- relire et challenger les règles proposées ;
- sélectionner un sous-ensemble de règles candidates ;
- vérifier qu'elles sont automatiquement corrigeables ;
- créer ou adapter un `.editorconfig` ;
- exécuter `dotnet format` ;
- tester le build avec enforcement ;
- tester le contrôle dans la CI ;
- mesurer le diff produit sur un projet existant ;
- identifier les règles problématiques ou trop coûteuses.

## Preuve de faisabilité

Un repository pilote doit pouvoir être automatiquement formaté puis vérifié par un mécanisme reproductible.

## À mesurer / cartographier

- configurations existantes ;
- divergences entre repositories ;
- IDE utilisés ;
- volume de reformatage initial ;
- règles non automatiquement corrigeables ;
- impacts sur les branches en cours.

## Sorties backlog attendues

- règles retenues / rejetées ;
- `.editorconfig` de référence ;
- stratégie de migration ;
- mécanisme d'enforcement proposé ;
- Tech Stories de généralisation ;
- backlog de gouvernance / distribution multi-repos.

---

# 15. Validation de la Rich Domain Architecture sur une API

## Objectif

Valider sur une API réelle la faisabilité et la pertinence de la **Rich Domain Architecture** décrite dans :

`Reefact/guidelines/rich-domain-architecture.md`.

La spécification décrit notamment :

- une Clean Architecture dont la structure révèle les capacités métier ;
- des use cases explicites ;
- un Domain riche portant comportements et invariants ;
- des frontières API / Application / Domain / Infrastructure ;
- un CQRS léger ;
- des écritures passant par le Domain ;
- des lectures pouvant contourner le Domain lorsqu'aucun comportement métier n'est nécessaire ;
- des adapters minces ;
- des erreurs représentées explicitement ;
- des règles architecturales vérifiables lorsque cela est possible.

## Format Tech Days recommandé

**Atelier POC sur une API réelle**, avec un groupe restreint.

Il est préférable de choisir une API présentant suffisamment de logique métier pour que l'exercice soit significatif. Une API purement CRUD ou essentiellement technique serait un mauvais support de validation.

## Travail attendu

Le groupe doit sélectionner un ou plusieurs use cases représentatifs et essayer réellement de les structurer selon les principes de la Rich Domain Architecture.

Le POC doit notamment permettre de vérifier :

### Structure

- séparation API / Application / Domain / Infrastructure ;
- organisation par capacités métier et use cases ;
- lisibilité du système à partir de l'arborescence ;
- cohérence d'une même capacité à travers les différentes zones.

### API

- endpoint centré sur une opération ;
- adaptation du protocole vers l'Application ;
- mapping aux frontières ;
- absence de logique métier dans l'endpoint.

### Application

- use case explicite ;
- orchestration sans duplication des règles métier ;
- dépendances exprimées via des abstractions internes.

### Domain

- comportement métier réellement porté par le modèle ;
- invariants protégés ;
- Value Objects / Entities / Aggregates uniquement lorsqu'ils ont une vraie justification métier.

### Read / Write

- écriture traversant le Domain ;
- lecture utilisant un chemin simplifié si le Domain n'apporte aucune valeur sur ce scénario.

### Infrastructure

- détails techniques confinés ;
- implémentation des ports attendus par les couches internes ;
- absence de contamination du Domain par les technologies externes.

### Erreurs

- erreurs métier, applicatives et techniques distinguées ;
- traduction explicite aux frontières ;
- absence d'utilisation systématique des exceptions pour les branches métier attendues.

### Tests et vérification

- tests du Domain centrés sur comportements et invariants ;
- tests du use case sur l'orchestration ;
- au moins quelques règles architecturales candidates à une vérification automatique.

## Preuve de faisabilité

Le résultat attendu n'est pas un diagramme théorique.

Au moins un use case réel doit fonctionner dans une structure conforme aux principes testés.

Le groupe doit également montrer :

- le code avant / après ou l'écart avec l'architecture existante ;
- les bénéfices observés ;
- les points qui deviennent plus complexes ;
- les règles de la spécification qui semblent faciles ou difficiles à appliquer ;
- les éventuelles ambiguïtés de la spécification révélées par le POC.

## À mesurer / cartographier

- structure actuelle de l'API ;
- responsabilités aujourd'hui mélangées ;
- logique métier présente dans API / Application / Infrastructure ;
- use cases candidats ;
- dépendances entre projets ;
- effort de migration ;
- possibilités d'adoption progressive.

## Sorties backlog attendues

Le résultat doit alimenter **à la fois le backlog de l'application et le backlog de la guideline**.

### Backlog application

- refactorings nécessaires ;
- use cases à migrer ;
- frontières à corriger ;
- Value Objects ou modèles métier à introduire ;
- tests manquants ;
- règles architecturales à automatiser ;
- Tech Stories de migration progressive.

### Backlog guideline / communauté

- principes confirmés ;
- points ambigus ;
- règles trop rigides ;
- exemples manquants ;
- décisions d'implémentation restant ouvertes ;
- fitness functions candidates ;
- adaptations de la guideline révélées par le terrain.

## Critère de réussite

Le POC est réussi même s'il montre qu'une partie de la proposition doit être modifiée.

L'objectif des Tech Days est précisément de confronter la guideline au réel afin de savoir :

> ce qui fonctionne, ce qui ne fonctionne pas, ce qui doit être précisé, et ce qu'il faudrait réellement faire pour adopter progressivement cette architecture.

---

# Vue synthétique

| Sujet | Format principal | Code attendu | Cartographie | Sortie principale |
| --- | --- | --- | --- | --- |
| Conventional Commits | Équipe / CI | Oui | Repositories | Règles + généralisation |
| Refit | Équipe + migration | Oui | Clients HTTP | Migration + backlog |
| Http.Resilience | Équipe + migration | Oui | Projets / policies | Migration + conventions |
| Stratégie résilience | Multi-équipe | Oui, POC | Policies existantes | Décision / ADR |
| Dispatch use cases | POC | Oui | MediatR / handlers | API interne + migration |
| Authentification API | Équipe puis transverse | Optionnel | Mécanismes auth | Cartographie + décision |
| Spectral | POC API | Oui | APIs / contrats | Ruleset + CI + backlog |
| FluentAssertions | Équipe + essais | Oui | Projets de tests | Stratégie de migration |
| Definition of Done | Équipe | Partiellement | DoD / contrôles | DoD + backlog enforcement |
| Logging | Équipe + refactoring | Oui | Logs / frameworks | Conventions + migration |
| Value Objects | Atelier | Oui | Concepts métier | Candidats + patterns |
| Documentation | Équipe | Oui, structure repo | Repositories | Documentation versionnée |
| IDR | Équipe | Non obligatoire | Décisions | IDR + sujets à instruire |
| Style de code | Transverse + pilote | Oui | Configurations | Règles + enforcement |
| Rich Domain Architecture | POC API | Oui | Architecture / use cases | Validation + backlog app + guideline |

---

# Résultat global attendu

À l'issue des Tech Days, chaque sujet travaillé doit se retrouver dans l'un des états suivants :

- **adoptable** : la faisabilité est démontrée et la généralisation peut être planifiée ;
- **à décider** : les informations nécessaires sont disponibles pour prendre une décision ;
- **à approfondir** : le POC a révélé des questions précises qui doivent être traitées ;
- **à abandonner ou revoir** : l'expérimentation montre que l'approche n'est pas adaptée dans sa forme actuelle.

Dans tous les cas, le résultat doit être matérialisé par des éléments concrets :

- code / POC ;
- cartographie ;
- constats ;
- problèmes identifiés ;
- décisions ou questions ouvertes ;
- Tech Stories / ADR / IDR / backlog.

Les Tech Days ne cherchent donc pas seulement à produire du code.

Ils utilisent le code comme un moyen de transformer des intentions techniques en **faits, décisions et travail planifiable**.
