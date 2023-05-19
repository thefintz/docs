[contato]: https://fintz.com.br/#/contato

# Índices

!!! success "Novidade!"
    Esse endpoint acaba de ser lançado e estamos adicionando índices continuamente.
    
    Tem algum índice que deseja ser adicionado o quanto antes?
    Só mandar pelo email contato@fintz.com.br

** /indices/historico **

Retorna o histórico referente ao índice requisitado.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `indice`     | `string` | ex: "IBOV" | obrigatório
| `dataInicio` | `string` | (yyyy-mm-dd) | obrigatório
| `dataFim`    | `string` | (yyyy-mm-dd) | opcional
| `ordem`      | `string` | "ASC" ou "DESC" | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'indice': 'IBOV', 'dataInicio': '2023-01-01' }

res = req.get(f'{URL_BASE}/indices/historico', headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
    {
        "indice": "IBOV",
        "data": "2023-01-02",
        "valor": 106376.0234375
    },
    {
        "indice": "IBOV",
        "data": "2023-01-03",
        "valor": 104165.7421875
    },
    ...
]
```


Os índices atualmente disponíveis são
```
IBOV
IBX
IFIX
IDIV
SMLL
ITAG
SP500
IGPM
IPCA
CDI
```

Precisa de algum outro índice? [Entre em contato][contato] e adicionamos gratuitamente.