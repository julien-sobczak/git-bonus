# 01_Introduction

## 1-3 Les méthodes de base

* Rsync = remote synchronization (Tous OS)
* Time Machine : Utilitaire Mac pour garder un historique sur un disque dur externe

## 1-4 Les avantages

* Les inconvénients :
** Aucun message de commit : je sais ce qui a changé mais pas pourquoi
** Difficile de voir facilement l'historique d'un fichier donné (parcours dans l'arborescence)

## 1-8 CVCS - Les solutions

- FSF = Free Software Foundation
- ASF = Apache Software Foundation

* Inconvénients CVS :
** Renommage/suppression fichier sans perte de l'historique
** commit non atomic (chaque fichier est commité séparément)
** Mauvais support fichier binaire
** Performance (tout le fichier transite sur le réseau et non pas que les modifications)

## 1-10 Distributed Version Control System

Avantages :
- Architecture peer-to-peer
- Travail en local (rapidité)
- Encourage versioning en local avant même de pousser les modifications

# 1-11 DVCS - Les solutions

Bazaar : Canonical, société derrière Ubuntu
=> Ubuntu, MySQL, GNU, Inkspace, Bugzilla, ...

Mercurial : pas mal utilisé en interne par Google
=> Mozilla, NetBeans, openJDK, Python

Git : Tous les projets sur GitHub !
=> Git, noyau Linux, Docker, Spring, ...


# 1-13 Type de workflow possible

Voir les Distributed Workflows (à ne pas confondre avec les Branching Workflows)
https://git-scm.com/book/en/v2/Distributed-Git-Distributed-Workflows


# 2-3 Le problème à résoudre

Montrer un git add suivi d'une modification du working directory




# Forgotten

Advantages and inconvenients of Centralized Version Control System (CVCS) :
+ everyone knows to a certain degree what everyone else on the project is doing.
+ Administrators have fine-grained control over who can do what
- single point of failure that the centralized server represents

Advantages of DVCS :
+ fully mirror the repository : Every checkout is really a full backup of all the data.
+ you can collaborate with different groups of people in different ways simultaneously within the same project. This allows you to set up several types of workflows that aren’t possible in centralized systems, such as hierarchical models.

Some of the original goals of Git :
• Speed
• Simple design
• Strong support for non-linear development (thousands of parallel branches)
• Fully distributed
• Able to handle large projects like the Linux kernel efficiently (speed and data size)


# Envoyer un PATCH

diff/apply vs format-patch/am
=> Privilégier le format-patch/am car contient l'auteur et les messages de commit

En savoir plus : https://git-scm.com/book/en/v2/Distributed-Git-Maintaining-a-Project#Applying-Patches-from-Email



# Réécrire une grosse partie de l'historique

Ex : changer son email sur tous les commits avant de déployer en OSS,
supprimer de tout l'historique un fichier contenant les mots de passe de la base de données.

En savoir plus : https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#The-Nuclear-Option:-filter-branch


# Créer une branche à partir d'un stash

git stash branch testchanges
> créé une nouvelle branches à partir du stash le plus récent et bascule dessus.


# Fonctionnalité avancée de recherche

grep dans tous les arbres :
https://git-scm.com/book/en/v2/Git-Tools-Searching#Git-Grep
Trouver le commit qui a introduit une nouvelle constante :
https://git-scm.com/book/en/v2/Git-Tools-Searching#Git-Log-Searching  


# Trouver l'origine d'un Bug

git bissect :
https://git-scm.com/book/tr/v1/Git-Tools-Debugging-with-Git#Binary-Search


# Cleaner son working repository

Permet de voir ce que les autres développeurs vont vraiment récupérer.
(Utile pour faire un clean install avant commit)

Supprime les fichiers "untracked" du working directory :
https://git-scm.com/docs/git-clean

Mode Dry-Run
$ git clean -d -n


# Supprimer un commit

git reset (local) vs git revert (public)


# Vue d'ensemble par développeur (ex : pour communication sur le contenu d'une version)

git shortlog
https://git-scm.com/book/mk/v1/%D0%94%D0%B8%D1%81%D1%82%D1%80%D0%B8%D0%B1%D1%83%D0%B8%D1%80%D0%B0%D0%BD-Git-Maintaining-a-Project#The-Shortlog


# Git Flow vs GitHub Flow

Références :
- http://nvie.com/posts/a-successful-git-branching-model/
- https://guides.github.com/introduction/flow/

Git Flow = release peu fréquente, branche longue
GitHub Flow = release quotidienne, branche courte

=> Git Flow déprécié dans le radar Thoughtworks

Utile à l'initialisation du projet :
$ git commit --allow-empty -m "Initial commit"
(nécessaire d'avoir un commit pour pouvoir tirer les branches)



# Trouver les commits à partir du message

Ex : rechercher le commit qui a corrigé telle évolution
(en considérant que le numéro de l'évolution est présente dans le message de commit)

$ git log --grep "EV33"


# Désactiver le pager (less) par défaut sur certaines commandes

Ex : exporter la commande blame d'un gros fichier dans un fichier texte.
$ git --no-pager blame FILE > FILE-annotated.txt



# Corriger un rebase foireux

$ git reflog
pour retrouver le SHA1 du précédent commit pointé par HEAD

$ git reset --hard SHA1
pour restaurer le working directory et l'index


# Merge avancé

Ex :
- Prendre mes modifs à chaque conflit automatiquement,
- Merger en prenant que mes modifications uniquement (faux merge)

$ git merge -Xours maBranche   # résoud les conflits en prenant mes modifs
$ git merge -Xtheirs maBranche #résoud les conflits en ignorant mes modifs
$ git merge -s ours maBranche  # merge en prenant que mes modifs

En savoir plus : https://git-scm.com/book/tr/v2/Git-Tools-Advanced-Merging#Other-Types-of-Merges



# Créer un livrable avec Git

$ git archive master --prefix='project/' | gzip &gt; `git describe master`.tar.gz
$ ls \*.tar.gz
v1.6.2-rc1-20-g8c5b85c.tar.gz

En savoir plus : https://git-scm.com/book/en/v2/Distributed-Git-Maintaining-a-Project#Preparing-a-Release


# Ne pas saisir ses credentials GitHub à chaque appel

- Possibilité de conserver en mémoire ses crédentials pendant une durée fixe (15 minutes par défaut).
- Possibilité de conserver sur disque (dépendant de l'OS).

En savoir plus : https://git-scm.com/docs/git-credential-cache


# Rejouer avec les différentes commandes classiques

Faire le TP en ligne : http://gitimmersion.com/


# Git status moins verbeux

$ git status -s
 M README
MM Rakefile
A  lib/git.rb
M  lib/simplegit.rb
?? LICENSE.txt

En savoir plus : https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository#Short-Status
