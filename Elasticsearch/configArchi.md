# Configurer une architecture multi-nœuds Docker

## Lancer le cluster
Créer le fichier "docker-compose.yml" puis faire :
```
docker-compose up -d
```

![alt text](picture/configArchi/image-2.png)

## Vérifier que le cluster fonctionne
### Vérifier l’état du cluster :
```
curl 0.0.0.0:9200/_cluster/health?pretty
```
- L’état doit être "green" ou "yellow" (évite "red" = problème).

![alt text](picture/configArchi/image-3.png)

### Voir les nœuds du cluster :
```
curl -X GET "http://0.0.0.0:9200/_cat/nodes?v"
```
- Affiche la liste des nœuds avec leur rôle.

![alt text](picture/configArchi/image-4.png)

