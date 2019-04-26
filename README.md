# adr-rackspace

système de traitement des journaux
problématique: Le flux de données est continu, où stocker toutes les données, comment va t'il être utile de faire ça?


Options envisagées:
1) stockage dans un fichier texte avec une recherche manuelle 
2) Une version MySQL avec une machine se qui induit une inondation de flux de données
3) division des données en table de fusion en fonction du temps ce qui s'implifie la mise à jour

Décision:
les outils doivent être rapides et précis.
les techniciens de l'assistance technique doivent avoir la possibilité d'examiner les journaux de messagerie afin de résoudre les problèmes de nos clients et cela plusieurs fois par jour.
pouvoir gérer plusieurs giga-octets de données générées chaque jour et sur plus de 600 serveurs de messagerie.


Un nouveau système de traitement de journaux utilisant Hadoop à code source ouvert de Google File System et MapReduce a était mis en place.
l'avantage c'est la possiblité de consulter leurs données comme ils veulent, c'est un outil puissant.

conséquences positives:

1) pour pouvoir rechercher les journaux, ils devaient transmettre un ticket à nos ingénieurs.
2) Accélérer le processus de recherche en écrivant un script permettant de rechercher plusieurs serveurs via une seule commande exécutée à partir d'un serveur centralisé.
3) Cela a rendu le nettoyage très rapide. 
4) Les données de journal n'ont été conservées que pendant 3 jours afin de maintenir la base de données MySQL à une taille raisonnable.

conséquences négatives:

1) une fois que nous avons dépassé une douzaine de serveurs, ce processus manuel de connexion à chaque serveur prend trop de temps à nos ingénieurs.
2) si deux ingénieurs effectuaient une recherche en même temps, ce qui ralentissait vraiment les choses.
3) Au fur et à mesure que les tables grandissaient, l'indexation de chaque entrée insérée devenait lente.
