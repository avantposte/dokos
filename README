# Migration de dokos cloud vers un déploiement auto-hébergé

1. récupération des données sur l'instance dokos cloud sur [l'outil de sauvegarde](https://avantposte.dokos.cloud/app/backups) :
- une sauvegarde de la base de données
- une sauvegarde des fichiers

2. déplacer les fichiers

```sh
mv [DUMP_PATH] ./data/database.sql.gz

mv [PRIVATE_FOLDER_PATH] ./data/private

mv [PUBLIC_FOLDER_PATH] ./data/public

```

3. démarrage et restauration des données et  des fichiers

```sh
# démarrer Dokos
docker compose up -d

# copie de la sauvegarde et des fichiers
docker cp ./data/database.sql.gz dodock-backend-1:/home/frappe/frappe-bench/sites/frontend/private/backups/

docker cp ./data/private/. dodock-backend-1:/home/frappe/frappe-bench/sites/frontend/private/files/

docker cp ./data/public/. dodock-backend-1:/home/frappe/frappe-bench/sites/frontend/public/files/

# restauration de la sauvegarde
docker compose run backend bench --site all restore database.sql.gz

# suppression de l'application dokos_cloud
docker compose run backend bench --site all remove-from-installed-apps dokos_cloud

docker compose run backend bench --site all remove-from-installed-apps bank

```

4. accéder à l'application avec les données de production sur http://localhost:8080