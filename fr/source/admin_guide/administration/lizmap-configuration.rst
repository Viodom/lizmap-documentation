===============================================================
Configuration de Lizmap
===============================================================


Introduction
===============================================================

Le menu *Configuration Lizmap* est divisée en 2 parties

* Les **Services** : la configuration générale de Lizmap Web Client - serveur, cache, etc.
* Les **Répertoires** : créer et configurer les répertoires Lizmap


.. image:: ../../MEDIA/administration-lizmap-configuration.png
   :align: center



Les services
===============================================================

Pour configurer les services, cliquer sur le bouton *Modifier* situé sous le récapitulatif

* **URL du serveur WMS** : L'url complète du serveur QGIS, par exemple http://localhost/cgi-bin/qgis_mapserv.fcgi . **Attention** QGIS Server doit être installé sur le même ordinateur que Lizmap Web Client

* **Liste d'URLs WMS de sous-domaine (optionnel)** L'utilisation de plusieurs noms de domaines est une des optimisations classiques lorsqu'une application web utilise OpenLayers (comme Lizmap Web Client). Vous pouvez entrer ici une liste des sous-domaine séparés par virgule.

  + Vous devez utiliser une **liste de sous-domaines** par rapport au domaine avec lequel est utilisé Lizmap Web Client. Par exemple, si votre nom de domaine principal est **cartes.exemple.com**, alors vous pouvez utiliser **a.cartes.exemple.com, b.cartes.exemple.com, c.cartes.exemple.com, d.cartes.exemple.com**.

  + Vous devez bien sûr avoir configuré l'*hôte virtuel* du serveur Apache pour prendre en compte ces sous-domaines, par exemple avec la variable

    .. code:: bash

       ServerAlias \*.cartes.exemple.com

* **Type de stockage pour le cache**

 - *file*: Les tuiles mises en cache sont stockées dans un répertoire du serveur par couche
 - *sqlite*: Les tuiles sont enregistrées dans une base de données sqlite par couche

* **Répertoire racine du cache** : le dossier dans lequel est stocké le cache. Il doit être accessible en écriture par le serveur Apache


* **Durée de vie du cache** : le temps en seconde pendant lequel chaque tuile est conservée. C'est une valeur par défaut pour les couches dont le temps n'a pas été configuré via le plugin

 - Les tuiles du cache plus vieilles que ce temps sont automatiquement raffraîchies.
 - La valeur 0 signigie que les tuiles n'expirent jamais
 - Le temps d'expiration doit être adapté à l'évolution des données

* **Envoi des requêtes à QGIS Server avec** : 2 méthodes. *Php ou Curl* . Utiliser la première si curl n'est pas installé sur le serveur
* *Mode de débogage* : enregistre certaines requêtes dans un fichier de log : *lizmap/var/log/messages.log*

* **Autoriser les visiteurs à demander un compte** : Si cette option est activée, un nouveau lien **Inscription** sera ajouté dans le menu des cartes Lizmap. En cliquant sur ce lien, le visiteur affiche un formulaire qui lui permet de demander un compte à l'administrateur. Il doit remplir certains champs (nom, prénom, adresse e-mail, raison de la demande) puis valide le formulaire pour envoyer sa demande.

* **Couriel de l'administrateur** Si une adresse e-mail valide est donnée, alors les notifications de Lizmap pourront y être envoyées. Par exemple, chaque demande de création de compte via le formulaire d'inscription génrère l'envoi d'un courriel à cette adresse.

.. image:: ../../MEDIA/administration-modify-services.png
   :align: center



Les répertoires
===============================================================

Pour chaque répertoire Lizmap sont listés

* **Les informations principales** : nom (label) et chemin (path)
* **La liste des droits** avec les groupes concernés
* **Des boutons d'action** :

  - *voir* : affiche la page qui liste les cartes de ce répertoire
  - *Modifier*: affiche le formulaire de modification du répertoire
  - *Supprimer* : permet de supprimer le répertoire
  - *Vider le cache* : permet de supprimer tout le cache de toutes les couches des projets de ce répertoire

.. image:: ../../MEDIA/administration-repository-detail.png
   :align: center

On peut créer un nouveau répertoire avec le bouton **Ajouter un répertoire** situé tout en bas de la page

Ajouter un répertoire
---------------------------------------------

Pour créer un répertoire, il faut donner

* **un identifiant**: un mot sans espaces, accents ni caractères spéciaux
* **un label** : le nom qui sera affiché pour ce répertoire, accents et espaces autorisés
* **un chemin (path)** : le chemin complet vers le dossier qui contient les projets QGIS et les données

.. _define_group_rights:

Définir les droits pour chaque groupe
---------------------------------------------

Une fois le répertoire créé, le formulaire de modification du répertoire est automatiquement affiché et permet de définir les droits suivants pour chacun des groupes:

* **Voir les répertoires** :

  - tous les utilisateurs des groupes cochés pourront accéder aux cartes de ce répertoire
  - le groupe *anonymous* représente les utilisateurs non enregistrés et permet de rendre les cartes publiques

* **Utiliser l'outil d'Édition**

  Lorsque cette option est cochée, les utilisateurs du groupe ont accès à l'outil d'édition pour l'ensemble des cartes du répertoire Lizmap pour lesquelles l'édition a été configurée.


* **Afficher toutes les données, mêmes si filtrées par login**

  Cette option est en lien avec la fonctionnalité de filtrage des données des couches par groupe. Voir :ref:`filter_layer_data_by_group`. Cocher la case permet de décider quels groupes pourront voir tout le temps toutes les données, même lorsqu'un filtre est actif sur certaines couches.

* **Autoriser les thèmes du répertoire**

  Cette option permet d'activer la possibilité pour l'éditeur de définir un thème pour le répertoire et des thèmes pour chaque carte. Voir :ref:`lizmap_simples_themes`.

.. image:: ../../MEDIA/administration-modify-repository.png
   :align: center


