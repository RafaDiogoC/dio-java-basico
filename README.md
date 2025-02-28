import requests
import json

SEARCH_SERVICE_NAME = "seu-servico"
API_KEY = "sua-chave-api"
INDEX_NAME = "meu-indice"

url = f"https://{SEARCH_SERVICE_NAME}.search.windows.net/indexes/{INDEX_NAME}?api-version=2023-07-01"
headers = {
    "Content-Type": "application/json",
    "api-key": API_KEY
}

index_config = {
    "name": INDEX_NAME,
    "fields": [
        {"name": "id", "type": "Edm.String", "key": True},
        {"name": "titulo", "type": "Edm.String"},
        {"name": "conteudo", "type": "Edm.String"},
        {"name": "dataCriacao", "type": "Edm.DateTimeOffset"}
    ]
}

response = requests.put(url, headers=headers, json=index_config)
print(response.json())
import requests
import json

SEARCH_SERVICE_NAME = "seu-servico"
API_KEY = "sua-chave-api"
INDEX_NAME = "meu-indice"

url = f"https://{SEARCH_SERVICE_NAME}.search.windows.net/indexes/{INDEX_NAME}/docs/index?api-version=2023-07-01"
headers = {
    "Content-Type": "application/json",
    "api-key": API_KEY
}

documents = {
    "value": [
        {
            "@search.action": "upload",
            "id": "1",
            "titulo": "Introdução ao Azure AI Search",
            "conteudo": "Este documento explica como usar a pesquisa cognitiva no Azure.",
            "dataCriacao": "2024-02-27T12:00:00Z"
        },
        {
            "@search.action": "upload",
            "id": "2",
            "titulo": "Machine Learning no Azure",
            "conteudo": "Uma visão geral sobre aprendizado de máquina no Azure.",
            "dataCriacao": "2024-02-26T15:30:00Z"
        }
    ]
}

response = requests.post(url, headers=headers, json=documents)
print(response.json())
import requests

SEARCH_SERVICE_NAME = "seu-servico"
API_KEY = "sua-chave-api"
INDEX_NAME = "meu-indice"

query = "Azure"
url = f"https://{SEARCH_SERVICE_NAME}.search.windows.net/indexes/{INDEX_NAME}/docs?search={query}&api-version=2023-07-01"

headers = {
    "api-key": API_KEY
}

response = requests.get(url, headers=headers)
print(response.json())
