# dalomin-lab

Dépôt compagnon de la chaîne **DALOMIN**.

## La chaîne

On y décortique les protocoles réseau en partant des **RFC**, pas des
documentations produit. Chaque notion est montée en lab et illustrée par une
capture Wireshark : on lit le texte de la norme, puis on regarde le paquet
correspondant passer sur le câble.

La base du lab est volontairement libre et reproductible — Linux, Containerlab,
Kea, Wireshark. Le matériel propriétaire — commutateurs et routeurs Cisco,
pare-feu Fortinet — n'apparaît qu'en complément, quand il montre ce que
l'émulation ne sait pas rendre : l'option 82 insérée par un vrai commutateur
d'accès, le DHCP snooping, l'empreinte d'une imprimante du commerce.

## Ce dépôt

C'est un **compagnon des vidéos**, pas un produit.

On y dépose les fichiers qu'il serait pénible de retaper depuis un écran :
topologies Containerlab, configurations de serveurs, `Dockerfile`, captures
curées. Chaque série publiée a son dossier et son propre README.

Ce n'est **pas un kit clés en main**, et il n'y a rien à exécuter d'un bloc.
La procédure, c'est la vidéo — les fichiers d'ici servent à suivre, à coller et
à comparer.

Une série n'apparaît que lorsque ses épisodes sont en ligne.

## Organisation

    commun/     ce qui sert à plusieurs séries — image des nœuds, outillage
    series/     un dossier par série, avec son README

## Licence

MIT, voir `LICENSE`. Reprends, modifie, publie. Une mention de la chaîne fait
plaisir sans être exigée.
