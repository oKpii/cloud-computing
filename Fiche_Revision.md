# Fiche de révision Cloud Computing

## Vue d'ensemble du projet pédagogique
- Pipeline complet autour des données DPE : ingestion via Flask, streaming Kafka, persistance PostgreSQL, traitements Spark/Iceberg/MinIO, exposition SQL Trino et dashboards Superset, avec Airflow en option pour l'orchestration.【F:README.md†L29-L142】
- Objectifs clés : comprendre le rôle de chaque brique d'architecture cloud, manipuler les flux de données en streaming et batch, pratiquer la containerisation Docker et le fonctionnement d'un cluster distribué.【F:README.md†L29-L142】

## Progression des TP
1. **API Python** : consommation de l'API ADEME, manipulation JSON et préparation des données.【F:README.md†L149-L157】
2. **Docker** : conteneurisation du script, gestion d'images et de volumes, lancement multi-services avec docker-compose.【F:README.md†L158-L168】
3. **Kafka + PostgreSQL** : publication de flux, consumption vers base relationnelle, notions de topic/partition/offset/consumer group.【F:README.md†L170-L179】
4. **Spark / Iceberg / MinIO** : transformations distribuées depuis PostgreSQL, stockage analytique colonnaire sur MinIO, compréhension driver/workers et batch/micro-batch.【F:README.md†L181-L191】
5. **Trino / Superset** : requêtes SQL distribuées sur Iceberg/PostgreSQL et création de tableaux de bord interactifs.【F:README.md†L193-L202】
6. **Airflow (bonus)** : DAG orchestrant toute la chaîne, planification et dépendances de tâches.【F:README.md†L205-L214】

## Docker : fondamentaux et pratiques
- Conteneurisation légère et reproductible pour packager application et dépendances, avec isolation et déploiement rapide (exemples data : bases PostgreSQL/MySQL, jobs Python, outils Kafka/Spark/MinIO).【F:Docker.md†L131-L154】
- Prérequis et tests : compte Docker Hub, usage de Play With Docker, vérification avec `docker version`/`docker info` et exécution `hello-world`.【F:Docker.md†L156-L194】
- Volumes : persistance via volumes nommés ou bind mounts, commandes `docker volume create/ls/inspect/rm`, démonstration de génération/lecture de CSV dans un volume pour garantir la durabilité des fichiers au-delà du conteneur.【F:Docker.md†L46-L67】【F:Docker.md†L52-L65】
- Docker Compose : définition multi-services (app, requirements, Dockerfile, compose) pour lancer et nettoyer une stack complète en une commande.【F:Docker.md†L73-L83】
- Docker Swarm : notions de cluster (manager/workers), services distribués, scaling, load balancing et tolérance aux pannes pour exposer une application web.【F:Docker.md†L84-L109】
- Mini-projets : formulaire Streamlit + MySQL sur réseau overlay PWD et extraction DPE par département via conteneurs paramétrés écrivant des Parquet persistés localement.【F:Docker.md†L110-L129】

## Kafka : streaming et exercices
- Rôle : broker haute performance pour ingestion massive, traitement temps réel, découplage producteur/consommateur et persistance tolérante aux pannes.【F:Kafka.md†L51-L89】
- Stack pédagogique : broker `obsidiandynamics/kafka` et interface Kafdrop pour explorer topics/messages et consumer groups.【F:Kafka.md†L91-L124】
- Parcours d'exercices progressifs :
  - Producer Python envoyant des messages à intervalle régulier et visualisation Kafdrop.【F:Kafka.md†L145-L154】
  - Envoi de données d'API vers Kafka, puis pipeline complet Producer/Consumer.【F:Kafka.md†L22-L30】【F:Kafka.md†L26-L33】
  - Intégration PostgreSQL, gestion de partitions et scaling de consumers, puis consommateurs spécialisés (base vs analytics).【F:Kafka.md†L30-L41】
- Mini-projet : ingestion des DPE par département avec consignes de paramétrisation, persistance et points pédagogiques ciblés.【F:Kafka.md†L44-L47】

## MinIO, Data Lake et Iceberg
- MinIO : stockage d’objets compatible S3, utile pour cloud souverain et pédagogie, intégrable avec Python/Spark, scalable du petit au gros volume.【F:MinIO.md†L55-L77】
- Concepts clés : buckets comme conteneurs logiques, différences avec SGBD, construction d’un data lake en couches Bronze/Silver/Gold.【F:MinIO.md†L79-L114】
- Formats et partitionnement : choix JSON/CSV/Parquet, importance du partitionnement sur faible cardinalité pour accélérer les lectures et réduire les coûts.【F:MinIO.md†L115-L199】
- TP : docker-compose MinIO + Python pour récupérer les données ADEME, conversions JSON→CSV→Parquet, vérification de persistance par volumes ; gestion des utilisateurs/policies et connexion à Iceberg pour tables ACID analytiques.【F:MinIO.md†L29-L52】

## Spark : calcul distribué
- Spark permet de traiter de gros volumes en parallèle, au-delà des limites de Pandas, pour logs, pipelines, machine learning et data lakes.【F:Spark.md†L26-L47】
- Architecture : Driver qui planifie et coordonne, Workers qui exécutent les partitions en parallèle dans un cluster.【F:Spark.md†L49-L68】
- Concepts : partitions pour parallélisation, structures RDD/DataFrame, lazy evaluation déclenchée par les actions, usage Python via PySpark, comparaison avec exécution locale.【F:Spark.md†L74-L115】
- TP cluster : construction d'une image Docker Spark, déploiement Master/Workers/History Server via docker-compose et soumission de jobs PySpark pour observer la parallélisation.【F:Spark.md†L124-L150】

## Compétences mises en avant
- Data engineering : ingestion Kafka, consumers Python, stockage PostgreSQL, transformation Spark, data lake Iceberg/MinIO, conteneurisation Docker, compréhension cluster distribué.【F:README.md†L227-L234】
- Data analysis : SQL distribué avec Trino et dashboards Superset sur les données DPE.【F:README.md†L227-L234】
- Cybersécurité & bonnes pratiques : authentification API, isolation réseau Docker, sécurisation basique des services et attention aux versions/ports/volumes.【F:README.md†L237-L248】
