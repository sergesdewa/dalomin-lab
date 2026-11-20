# Boîte à outils

L'image unique dont sortent **tous** les nœuds des topologies Containerlab.

Ce qui distingue un serveur d'un client n'est pas l'image, c'est le processus
qu'on y lance : `kea-dhcp4` dans l'un en fait un serveur, `dhclient` dans
l'autre en fait un client. D'où une image qui contient les deux.

## Construire

    docker build -t dalomin/boite-a-outils:1.0 .

Trois à cinq minutes, cinq à sept cents mégaoctets. Les topologies y renvoient
par une **version explicite** — jamais `:latest` — pour qu'un ancien épisode
continue de tirer l'image qu'il avait à l'écran.

## Vérifier

    docker run --rm dalomin/boite-a-outils:1.0 sh -c '
    for t in dhclient dhcpcd kea-dhcp4 dnsmasq dhcrelay tcpdump tshark \
             mergecap arping nft dig jq; do
      printf "%-12s %s\n" "$t" "$(command -v $t || echo MANQUANT)"
    done'

## Prérequis sur l'hôte

Docker et Containerlab. Containerlab a besoin d'un moteur de conteneurs pour
fournir les machines ; le réseau lui-même — espaces de noms et paires veth —
ne relève que du noyau Linux.
