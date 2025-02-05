# Modélisation des données dans Elasticsearch
## Commande pour créer un index

```
curl -XPUT 'http://localhost:9200/cities' -H 'Content-Type: application/json' -d '
{
  "settings": {
    "number_of_shards": 2,
    "number_of_replicas": 2
  }
}'
```
![alt text](picture/modielisation/image.png)

## Vérification des paramètres de l'index
```
curl -XGET 'http://localhost:9200/cities/_settings' | jq
```
![alt text](picture/modielisation/image-1.png)

## Insertion de données dans l'index
### Insertion
```
curl -XPOST 'http://localhost:9200/cities/_doc' -H 'Content-Type: application/json' -d '
{
  "city": "London",
  "country": "England"
}'
```
![alt text](picture/modielisation/image-2.png)

### Vérification
```
curl -XGET 'http://localhost:9200/cities/_doc/pquR1oYBQIvdICuNRLuD'
```
![alt text](picture/modielisation/image-3.png)

Format de retour : La réponse de la commande GET montre plusieurs champs :
- index : Le nom de l'index où se trouve le document.
- type : Le type de document.
- id : L'identifiant unique du document.
- version : La version du document.
- source : Le contenu réel du document (dans ce cas, les informations sur la ville et le pays).