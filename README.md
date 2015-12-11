
# Envoyer un PATCH

`diff`/`apply` vs `format-patch`/`am`

=> Privilégier le `format-patch`/`am` car contient l'auteur et les messages de commit

En savoir plus : https://git-scm.com/book/en/v2/Distributed-Git-Maintaining-a-Project#Applying-Patches-from-Email



# Réécrire une grosse partie de l'historique

Exemples :
- Changer son email sur tous les commits avant de déployer en OSS,
- Supprimer de tout l'historique un fichier contenant les mots de passe de la base de données.

En savoir plus : https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History#The-Nuclear-Option:-filter-branch


# Créer une branche à partir d'un stash

`$ git stash branch testchanges`

Créer une nouvelle branches à partir du stash le plus récent et bascule dessus.


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
`$ git clean -d -n`


# Supprimer un commit

`git reset` (local) vs `git revert` (public)


# Vue d'ensemble par développeur (ex : pour communication sur le contenu d'une version)

`$ git shortlog`

En savoir plus : https://git-scm.com/book/fr/v2/Git-distribu%C3%A9-Maintenance-d%E2%80%99un-projet#Shortlog


# Git Flow vs GitHub Flow

## Références :
- http://nvie.com/posts/a-successful-git-branching-model/
- https://guides.github.com/introduction/flow/

> Git Flow = release peu fréquente, branche longue
> GitHub Flow = release quotidienne, branche courte

=> Git Flow déprécié dans le radar Thoughtworks

## Utile à l'initialisation du projet :

`$ git commit --allow-empty -m "Initial commit"`

(nécessaire d'avoir un commit pour pouvoir tirer les branches)



# Trouver les commits à partir du message

Ex : rechercher le commit qui a corrigé telle évolution
(en considérant que le numéro de l'évolution est présente dans le message de commit)

`$ git log --grep "EV33"`


# Désactiver le pager (less) par défaut sur certaines commandes

Ex : exporter la commande blame d'un gros fichier dans un fichier texte.

`$ git --no-pager blame FILE > FILE-annotated.txt`



# Corriger un rebase foireux

`$ git reflog`
pour retrouver le SHA1 du précédent commit pointé par HEAD

`$ git reset --hard SHA1`
pour restaurer le working directory et l'index


# Merge avancé

Exemples :
- Prendre mes modifs à chaque conflit automatiquement,
- Merger en prenant que mes modifications uniquement (faux merge)

`$ git merge -Xours maBranche   # résoud les conflits en prenant mes modifs`
`$ git merge -Xtheirs maBranche #résoud les conflits en ignorant mes modifs`
`$ git merge -s ours maBranche  # merge en prenant que mes modifs`

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
