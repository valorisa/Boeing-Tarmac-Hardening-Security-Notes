# Analyse et comparaison

A mettre en lien ou comparaison avec cet autre article que nous avons traité ensemble : https://www.01net.com/actualites/pirater-un-boeing-737-en-60-secondes-ce-minuscule-boitier-peut-permettre-de-detourner-un-avion.html

Les deux articles se complètent très bien : le premier décrit une **vulnérabilité technique locale**, tandis que l’article sur Airbus décrit la **doctrine de sécurité nécessaire pour gérer ce type de menace à l’échelle d’un groupe aéronautique et de sa supply chain**.

## Le lien central

L’article 01net montre un cas où l’attaquant ne « casse » pas nécessairement le système : il exploite un **accès physique légitime mais insuffisamment protégé**, un port de maintenance accessible depuis le tarmac. Un boîtier d’environ 100 dollars pourrait être installé en moins d’une minute et communiquer avec le réseau avionique interne via le bus ARINC 429.[1]

L’article consacré à Airbus élargit cette logique : l’attaquant moderne utilise un accès déjà disponible — identifiant valide, fournisseur compromis, terminal autorisé, interface technique ou outil d’IA mal configuré — puis agit à l’intérieur du système.

Dans les deux cas, le problème est donc moins l’absence de protection que la **confiance excessive accordée à un accès considéré comme légitime**.

## Comparaison des deux scénarios

| Dimension | Boeing 737 / Bus Driver | Airbus / nouvelle doctrine cyber |
|---|---|---|
| Point d’entrée | Port de maintenance physique accessible depuis le sol | Identifiants, fournisseurs, filiales et outils connectés |
| Type d’accès | Accès direct au réseau avionique | Accès logique à l’écosystème numérique |
| Faiblesse principale | Connecteur exposé et protocole ARINC 429 sans authentification suffisante | Confiance excessive envers identités, terminaux et partenaires |
| Échelle | Un avion donné | Groupe industriel et environ 12 000 sous-traitants |
| Méthode | Implant matériel discret | Compte compromis ou accès fournisseur légitime |
| Détection | Difficile si le boîtier reste caché | Difficile si les actions ressemblent à celles d’un utilisateur normal |
| Impact potentiel | Modification de trajectoire ou de paramètres de préparation du vol | Exfiltration, mouvement latéral, compromission industrielle ou opérationnelle |
| Défense privilégiée | Condamner le port, renforcer les contrôles et sécuriser les communications | Zero trust, surveillance comportementale, segmentation et security by design |

## Le point commun : un accès légitime détourné

Dans le cas du Boeing, le port de maintenance est légitime. Il existe pour permettre aux techniciens de diagnostiquer ou de tester les systèmes. La vulnérabilité vient du fait que l’accès physique paraît implicitement digne de confiance.

Le protocole ARINC 429, largement utilisé depuis les années 1970, permettrait de faire circuler des messages sans mécanisme suffisant pour vérifier cryptographiquement l’identité de l’émetteur. Le dispositif pourrait donc injecter des informations dans les systèmes avioniques, même si la réalisation complète de l’attaque reste complexe.[1]

Chez Airbus, le même raisonnement s’applique aux accès numériques : un compte valide ou un fournisseur autorisé n’est plus considéré comme fiable automatiquement. L’article indique qu’environ 90% des attaques subies par Airbus reposeraient désormais sur des identifiants valides.

La différence est donc la suivante :

- dans un avion, **la prise physique devient une identité technique implicite** ;
- dans l’entreprise, **le compte utilisateur ou fournisseur devient une prise logique implicite**.

## Zero trust appliqué à l’avionique

L’article 01net illustre pourquoi le zero trust ne doit pas être compris uniquement comme une politique d’authentification des utilisateurs. Dans un environnement aéronautique, il doit également s’appliquer à :

- chaque port de maintenance ;
- chaque équipement connecté au bus ;
- chaque message échangé entre calculateurs ;
- chaque logiciel de maintenance ;
- chaque terminal utilisé sur le tarmac ;
- chaque mise à jour et composant matériel ;
- chaque interaction entre les réseaux avioniques et les systèmes au sol.

Un port de maintenance devrait donc être traité comme une interface d’administration hautement privilégiée, avec :

- authentification forte du matériel connecté ;
- autorisation par opération et par durée ;
- journalisation de chaque connexion ;
- détection d’un appareil inconnu ;
- vérification cryptographique des messages ;
- séparation entre diagnostic, lecture et écriture ;
- désactivation physique ou logique lorsque le port n’est pas utilisé.

Cela correspond directement à la philosophie Airbus : **ne faire confiance à aucun utilisateur, terminal, application ou flux par défaut**.

## Une différence importante : IT contre systèmes embarqués

Il faut toutefois éviter de confondre les deux problèmes.

L’article Airbus concerne principalement la transformation de la cybersécurité d’un groupe industriel : identités, SOC, fournisseurs, cloud, IA, souveraineté et développement logiciel.

L’article 01net concerne une attaque contre un système embarqué soumis à des contraintes particulières :

- certification aéronautique ;
- longue durée de vie des équipements ;
- protocoles hérités ;
- exigences de sûreté de fonctionnement ;
- disponibilité en vol ;
- séparation des réseaux ;
- maintenance physique ;
- impossibilité de modifier rapidement toute une flotte.

Dans l’IT classique, on peut souvent remplacer un composant, appliquer un correctif ou révoquer un compte rapidement. Dans l’avionique, une modification peut exiger des essais, une certification et un déploiement contrôlé sur de nombreux appareils. C’est pourquoi le *security by design* est particulièrement important : corriger une faiblesse après certification peut être extrêmement coûteux.

## Le rôle du security by design

Les deux articles convergent fortement sur ce point.

Le scénario du Boeing révèle une décision de conception ancienne : un connecteur de maintenance accessible, relié à un bus interne et insuffisamment authentifié. Les chercheurs recommandent notamment de condamner ou retirer le connecteur vulnérable et d’ajouter des mécanismes de chiffrement.[1]

Airbus veut éviter que ce type de choix soit traité uniquement après coup. Sa doctrine vise à intégrer la sécurité dès la conception :

- architecture réseau ;
- choix des protocoles ;
- gestion des accès de maintenance ;
- composants électroniques ;
- langages de programmation ;
- chaînes de compilation ;
- systèmes de supervision ;
- dépendances cloud et fournisseurs.

L’utilisation de Rust évoquée par Airbus s’inscrit dans cette démarche, mais elle ne constitue qu’une partie de la solution. Rust peut réduire certaines erreurs de mémoire ; il ne garantit pas l’authentification des messages, la séparation des privilèges ou la sécurité physique d’un connecteur.

## Le cas de l’IA

L’IA ajoute une nouvelle couche à ce rapprochement.

Dans l’article Airbus, une IA mal configurée chez un sous-traitant peut devenir un vecteur de menace lorsqu’elle dispose d’un accès à plusieurs systèmes ou à de grands volumes d’informations internes.

Dans un avion ou son environnement de maintenance, un agent logiciel doté de privilèges excessifs pourrait théoriquement devenir une nouvelle interface d’administration. Il faudrait alors lui appliquer les mêmes règles qu’à un équipement ou à un technicien :

- identité propre ;
- droits minimaux ;
- accès limité dans le temps ;
- outils explicitement autorisés ;
- séparation lecture/écriture ;
- validation humaine pour les commandes critiques ;
- journaux non falsifiables ;
- impossibilité de modifier directement des paramètres de vol sans contrôles indépendants.

Autrement dit, un agent IA ne doit jamais être traité comme une source fiable simplement parce qu’il s’exécute dans un environnement autorisé.

## Ce que Boeing apporte à la doctrine Airbus

Le cas du Boeing permet de rendre concrète la phrase du CSO d’Airbus : « Nous ne faisons plus confiance à rien. »

Cette phrase ne signifie pas qu’il faut supprimer tous les accès nécessaires à la maintenance. Elle signifie qu’un accès utile doit être :

1. identifié ;
2. authentifié ;
3. autorisé pour une action précise ;
4. limité dans le temps ;
5. surveillé ;
6. vérifié indépendamment ;
7. révoqué dès que l’opération est terminée.

Le port de maintenance, le compte d’un sous-traitant, le terminal d’un technicien et l’agent IA d’un fournisseur doivent donc être considérés comme des **points d’entrée privilégiés**, et non comme des éléments automatiquement fiables.

## Conclusion

L’article sur le Boeing montre une faiblesse au niveau de la **surface technique de l’avion** : une interface physique oubliée, un bus ancien et une confiance implicite dans les équipements connectés.

L’article sur Airbus montre la réponse organisationnelle et stratégique à ce type de problème : **zero trust, défense de la supply chain, contrôle des identités, automatisation de la détection, souveraineté et sécurité intégrée dès la conception**.

La leçon commune est claire : dans l’aéronautique moderne, la sécurité ne peut plus reposer uniquement sur le fait qu’un système est « interne », qu’un appareil est « autorisé » ou qu’un port est réservé à la maintenance. Tout accès doit être considéré comme potentiellement compromis jusqu’à ce que son identité, son contexte, son action et son résultat aient été vérifiés.

Citations :
[1] Pirater un Boeing 737 en 60 secondes : ce minuscule boîtier peut permettre de détourner un avion https://www.01net.com/actualites/pirater-un-boeing-737-en-60-secondes-ce-minuscule-boitier-peut-permettre-de-detourner-un-avion.html
