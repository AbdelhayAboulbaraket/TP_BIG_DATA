# Découverte et mise en œuvre de Spark

    ## Lecture de données

Après téléchargement des données du lien : https://s3.amazonaws.com/baywheels-data/201802-fordgobike-tripdata.csv.zip, nous avons crée la table "201902_fordgobike_tripdata" depuis le notebook dans databricks.

nous avons changé le schéma de données pour que les colonnes duration_sec soit un entier, start_time et end_time soient du type datetime.

    ## Structure des données

Dans notre dataset, nous avons 183412 fordgobike trips avec 16 colonnes (duration_sec, start_time, end_time, start_station_id, start_station_name, start_station_latitude, start_station_longitude, end_station_id, end_station_name, end_station_latitude ,end_station_longitude, bike_id, user_type, member_birth_year, member_gender, bike_share_for_all_trip). 9 de ces dernières sont numeriques, 2 sont des datetime, 4 de type objet et 1 qui est de type boolien.


    ## Analyse et visualisation des données

Dans cette partie, nous sommes intéressé à comprendre comment la durée du voyage (duration_sec) dépend d'autres spécifications de l'ensemble de données. nous nous attendons à ce que la durée du trajet dépende fortement des stations de départ et des stations d'arrivée, les endroits plus encombrés devraient recevoir plus de trajets, donc certaines stations devraient enregistrer plus de durée. Nous pensons également que user_type, birthyear et gender devraient également affecter la durée du voyage.

    ### A. Exploration Univariante

Nous allons commencer par regarder la distribution de la principale variable d'intérêt : duration_sec.
![Alt text](./images/distribution.png "Title")
Nous observons qu'elle formait un graphique à asymétrie positive, où la majorité des trajets ont une durée comprise entre 5 et 10 minutes.
Affichons maintenant la distribution des fonctionnalités datetime






Lorsque nous regardons la distribution des balades à vélo par heure, nous voyons un pic de déplacement entre 7 et 10 et un autre pic entre 16 et 20;
Quand on regarde la même variable par jour de la semaine, on remarque que du lundi au vendredi nous avons la plupart des trajets avec des pics entre le mardi et le jeudi et un nombre minimal le week-end. 
Notons que ces trajets sont faits principalement dans les heures de déplacement pour partir ou revenir du travail.

Passons à la distribution de la fonctionnalité utilisateur







On voit ici que plus de 87,5% des utilisateurs qui utilisent les services sont des abonnés.

    B. Exploration Bivariante

Commençons par comparer la durée des trajets par les autres fonctionnalités.

Nous voyons que les utilisateurs "Customer" ont tendance à effectuer des trajets plus longs que les utilisateurs "Subscriber".

Nous observons que pendant les week-ends, les gens ont tendance à faire des trajets plus longs.
Faisons maintenant une comparaison de user_type par les autres fonctionnalités

Ici, nous constatons une forte baisse du nombre d'abonnés le week-end, tandis que l’utilisateur client a moins d'impact.

Là encore, on remarque la tendance à l'augmentation des déplacements aux heures de 7 à 10 et de 16 à 20, principalement pour les utilisateurs « Subscriber ».
Les utilisateurs « Customer » suivent une tendance plus discrète avec plus de déplacements dans l'après-midi.
Pour conclure, l’habitude des déplacements varie beaucoup entre "Subscriber" et "Customer". Le “Subscriber” utilise le service de vélos pendant les heures de travail, de sorte que la plupart des déplacements ont eu lieu en semaine (du lundi au vendredi) et surtout aux heures de pointe (lorsqu’on travaille le matin et part l'après-midi), tandis que les “Customer” s'amusent généralement dans l'après-midi ou le week-end.

    C. Exploration Multivariante
Dans cette partie nous comparons la durée moyenne du trajet en minute le user_type par les autres fonctionnalités

Nous avons remarqué que la durée moyenne du trajet horaire, met le “Customer” avec une augmentation du temps pendant les heures de l'après-midi, tandis que le “Subscriber” a peu de variation pendant la journée des heures ouvrables.


Nous avons également observé que le “Customer” passait plus de temps en déplacements durant le week-end, tandis que le “Subscriber” a peu de volatilité pour le week-end.