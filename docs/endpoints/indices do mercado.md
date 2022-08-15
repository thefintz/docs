# Índices do mercado

Todos os endpoints desta página tem a seguinte url base:
> `URL_BASE` = `https://0o1jvhh5z7.execute-api.us-east-2.amazonaws.com`

Permite o usuário consultar dados de todas empresas brasileiras
cadastradas na receita federal através do CNPJ. Os dados são atualizados mensalmente.

## Lista de índices

Retorna a [lista de índices](#lista-de-indices) de mercado disponíveis na API Fintz.

**Exemplo de chamada:**

```bash
curl '{URL_BASE}/indexes'
```

**Resposta:**

```json
[
  { "code": "ibov", "name": "Ibovespa", "shortName": "IBOV" },
  { "code": "spx", "name": "S&P 500", "shortName": "SP500" }
]
```

## Índice entre datas

**Parâmetros:**

- `INDICE`: `spx`, `ibov` ou qualquer outro retornado pela [lista de índices](#lista-de-indices)
- `start`: data inicial no formato AAAA-MM-DD
- `end`: data final no formato AAAA-MM-DD

**Exemplo:**

```bash
curl '{URL_BASE}/indexes/{INDICE}/profitability?start=2022-08-01&end=2022-08-05'
```

```json
[
  { "date": "2022-08-05", "value": 0.041544049932708216 },
  { "date": "2022-08-04", "value": 0.03587319953442192 },
  { "date": "2022-08-03", "value": 0.015158722213008735 },
  { "date": "2022-08-02", "value": 0.011118846968354967 },
  { "date": "2022-08-01", "value": 0.0 }
]
```

## Índice mensal

**Parâmetros:**

- `INDICE`: `spx`, `ibov` ou qualquer outro retornado pela [lista de índices](#lista-de-indices)
- `months`: número inteiro que define quantos meses anteriores o índice escolhido será buscado e retornado

**Exemplo:**

```bash
curl '{URL_BASE}/indexes/{INDICE}/performance/monthly?months=3'
```

```json
[
  { "date": "2022-08", "value": 0.09305093191408154 },
  { "date": "2022-07", "value": 0.04691133297445482 },
  { "date": "2022-06", "value": -0.11502915378767709 }
]
```

## Índice anual

**Parâmetros:**

- `INDICE`: `spx`, `ibov` ou qualquer outro retornado pela [lista de índices](#lista-de-indices)
- `years`: número inteiro que define quantos anos anteriores o índice escolhido será buscado e retornado

**Exemplo:**

```bash
curl '{URL_BASE}/indexes/{INDICE}/performance/yearly?years=4'
```

```json
[
  { "date": "2022", "value": 0.07576450712186511 },
  { "date": "2021", "value": -0.11926679216056335 },
  { "date": "2020", "value": 0.02915723476761256 },
  { "date": "2019", "value": 0.3158371994807625 }
]
```