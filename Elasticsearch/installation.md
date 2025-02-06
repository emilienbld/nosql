# 🚀 Lancement d'un conteneur Elasticsearch

```bash
docker run -p 9200:9200 -p 9300:9300 -d -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.14.0
```

### 📌 Explications :
- **Ports 9200 et 9300** : communication avec Elasticsearch et entre les nœuds.
- **Mode détaché (-d)** : exécution en arrière-plan.
- **Mode single-node** : pour le développement/test.

![Lancement Elasticsearch](picture/install/image.png)

---

## ✅ Vérification de l’installation

```bash
curl 0.0.0.0:9200/_cluster/health | jq
```

![Vérification installation](picture/install/image1.png)

---

## 🖥️ Lister les nœuds du cluster

```bash
curl -X GET "http://0.0.0.0:9200/_cat/nodes?v"
```

![Liste des nœuds](picture/install/image-1.png)