# Indexation des données dans Elasticsearch

Fichier insert_data.sh :
```
echo "📤 Insertion des données dans Elasticsearch..."

curl -s -H "Content-Type: application/x-ndjson" -XPOST localhost:9200/receipe/_bulk --data-binary "@receipe.json" &&\
printf "\n✅ Insertion receipe index to elastic node OK ✅ \n"

curl -s -H "Content-Type: application/x-ndjson" -XPOST localhost:9200/accounts/_bulk --data-binary "@accounts.json" &&\
printf "\n✅ Insertion accounts index to elastic node OK ✅ \n"

curl -s -H "Content-Type: application/x-ndjson" -XPOST localhost:9200/movies/_bulk --data-binary "@movies.json" &&\
printf "\n✅ Insertion movies index to elastic node OK ✅ \n"

curl -s -H "Content-Type: application/x-ndjson" -XPOST localhost:9200/products/_bulk --data-binary "@products.json" &&\
printf "\n✅ Insertion products index to elastic node OK ✅ \n"

echo "🎉 Insertion terminée avec succès !"
```

Lancement du fichier script :
```
chmod +x insert_data.sh
./insert_data.sh
```
![alt text](picture/indexation/image.png)
(On peux voir sur l'image que ça n'as pas fonctionné mais j'ai réglé cela. Il fallait créer et 'remplir' les fichier par ligne de commandes "nano nom_du_fichier.json")

## Vérification des données
### Liste des index disponibles
```
curl -XGET "localhost:9200/_cat/indices?v"
```
![alt text](picture/indexation/image-1.png)

### Recherche tous les documents dans l'index movies
```
curl -XGET "localhost:9200/movies/_search?pretty=true"
```
![alt text](picture/indexation/image-2.png)

