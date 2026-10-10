
Still thinking...

```{bash}
curl -X POST "https://api-publica.datajud.cnj.jus.br/api_publica_tjrj/_search" \
  -H "Authorization: APIKey cDZHYzlZa0JadVREZDJCendQbXY6SkJlTzNjLV9TRENyQk1RdnFKZGRQdw==" \
  -H "Content-Type: application/json" \
  -d '{
    "query": {
      "match": {
        "classe.nome": "Procedimento do Juizado Especial Cível"
      }
    },
    "size": 5
  }' | jq .
```
