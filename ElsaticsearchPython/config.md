# 🚀 Lancer Elasticsearch avec Docker

## 📥 Télécharger et exécuter Elasticsearch

```bash
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.11.1
docker run -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.11.1
```
![Téléchargement et exécution](picture/image.png)

### 📌 Extraction de l’image
```bash
docker pull
```
![Extraction de l’image](picture/image-1.png)

```bash
docker pull docker.elastic.co/elasticsearch/elasticsearch:7.11.1
```
![Téléchargement spécifique](picture/image-2.png)

### ▶️ Lancer Elasticsearch en arrière-plan
```bash
docker run -p 9200:9200 -p 9300:9300 -d -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.11.1
```
![Exécution en arrière-plan](picture/image-3.png)

## 🔗 Accès au conteneur Elasticsearch
```bash
docker exec -it 9d717b963a5dcdfcaa59884114d90eb2d8ffd1abba3d8b08e75fcf6979b4199e bash
```
![Connexion au conteneur](picture/image-4.png)

## 🔄 Redémarrer le conteneur
```bash
docker restart 9d717b963a5dcdfcaa59884114d90eb2d8ffd1abba3d8b08e75fcf6979b4199e
```
![Redémarrage du conteneur](picture/image-5.png)

## 🔍 Vérifier les plugins installés
```bash
curl -X GET "http://localhost:9200/_cat/plugins?v"
```
![Vérification des plugins](picture/image-6.png)

## 🏗️ Création d'un index avec analyseur personnalisé
```bash
curl -X PUT "http://localhost:9200/french" -H "Content-Type: application/json" -d '{
  "settings": {
    "analysis": {
      "filter": {
        "french_elision": {
          "type": "elision",
          "articles_case": true,
          "articles": ["l", "m", "t", "qu", "n", "s", "j", "d", "c", "jusqu", "quoiqu", "lorsqu", "puisqu"]
        },
        "french_synonym": {
          "type": "synonym",
          "ignore_case": true,
          "expand": true,
          "synonyms": [
            "réviser, étudier, bosser",
            "mayo, mayonnaise",
            "grille, toaste"
          ]
        },
        "french_stemmer": {
          "type": "stemmer",
          "language": "light_french"
        }
      },
      "analyzer": {
        "french_heavy": {
          "tokenizer": "icu_tokenizer",
          "filter": [
            "french_elision",
            "icu_folding",
            "french_synonym",
            "french_stemmer"
          ]
        },
        "french_light": {
          "tokenizer": "icu_tokenizer",
          "filter": [
            "french_elision",
            "icu_folding"
          ]
        }
      }
    }
  }
}'
```
![Création de l’index](picture/image-7.png)

---

## 🐍 Installation de la librairie Elasticsearch pour Python
```bash
pip install "elasticsearch<7.14"
```
![Installation Elasticsearch Python](picture/image-8.png)

## 📝 Création du fichier `analyzer.py`
```python
from elasticsearch import Elasticsearch
es = Elasticsearch('http://localhost:9200')

doc1 = {"text" : "Une phrase en français 🙂 ..."}
response = es.index(index="french", id=1, body=doc1)

print(response)
```
### ▶️ Exécution du fichier
![Lancement `analyzer.py`](picture/image-9.png)

---

## 📝 Création du fichier `analyzer2.py`
```python
from elasticsearch import Elasticsearch

es = Elasticsearch("http://localhost:9200")

response = es.indices.analyze(index="french", body={
    "text": "Je dois bosser pour mon QCM sinon je vais avoir une sale note :( ..."
})

print(response)
```
### ▶️ Exécution du fichier
![Lancement `analyzer2.py`](picture/image-10.png)
