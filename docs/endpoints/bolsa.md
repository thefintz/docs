[contato]: https://fintz.com.br/#/contato

# Bolsa B3

Lembrando que todos os endpoints da API tem a mesma URL base e precisam do header de autenticação com sua chave.
>
```
URL_BASE = https://api.fintz.com.br
x-api-key = {sua chave da API Fintz}
```

## Busca e lista de ativos

** /bolsa/b3/avista/busca **

Nesse endpoint você consegue buscar e filtrar os ativos da B3 para depois buscar dados deles.
Por exemplo, você pode filtrar apenas os ativos do setor de tecnologia, ou mesmo pode conectar a sua search bar para buscar pelo nome ou ticker do ativo.

**Parâmetros**

- `q`: `string` que buscará entre os tickers (ex: "BBAS" vai retornar o "BBAS3")

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'q': 'BBAS' }

res = req.get(f'{URL_BASE}/bolsa/b3/avista/busca', headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "BBAS3",
    "nome": "BRASIL"
  }
]
```

## Cotação

** /bolsa/b3/avista/cotacoes/historico **

Retorna os preços de fechamento do ticker especificado na data especificada.

**Parâmetros**

| Parâmetro | Descrição | |
| :-: | - | :-: |
| `ticker`     | `string` representando o código de negociação | obrigatório
| `dataInicio` | `string` (yyyy-mm-dd) para inicio da busca dos dados históricos | obrigatório
| `dataFim`    | `string` (yyyy-mm-dd) para fim da busca dos dados históricos | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
ENDPOINT = URL_BASE + '/bolsa/b3/avista/cotacoes/historico'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'BBAS3', 'dataInicio': '2023-04-01' }

res = req.get(ENDPOINT, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "BBAS3",
    "data": "2023-04-10",
    "precoFechamentoAjustado": 39.04,
    "precoFechamento": 39.04,
    "precoAbertura": 39.35,
    "precoMinimo": 38.97,
    "precoMaximo": 39.69,
    "precoMedio": 39.29,
    "quantidadeNegocios": 18208,
    "quantidadeNegociada": 10958400,
    "volumeNegociado": 430647843
  },
  {
    "ticker": "BBAS3",
    "data": "2023-04-06",
    "precoFechamentoAjustado": 39.04,
    "precoFechamento": 39.02,
    "precoAbertura": 39.24,
    "precoMinimo": 38.85,
    "precoMaximo": 39.34,
    "precoMedio": 39.09,
    "quantidadeNegocios": 19877,
    "quantidadeNegociada": 6680900,
    "volumeNegociado": 261170772
  }
]
```

## Proventos

** /bolsa/b3/avista/proventos **

Retorna os proventos em dinheiro (Dividendos, JCPs, ...) referente ao ticker e as datas especificadas na chamada.

**Parâmetros**

| Parâmetro | Descrição | |
| :-: | - | :-: |
| `ticker`     | `string` representando o código de negociação | obrigatório
| `dataInicio` | `string` (yyyy-mm-dd) para inicio da busca dos dados históricos | obrigatório
| `dataFim`    | `string` (yyyy-mm-dd) para fim da busca dos dados históricos | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'BBAS3', 'dataInicio': '2023-01-01' }

res = req.get(f'{URL_BASE}/bolsa/b3/avista/proventos', headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "BBAS3",
    "dataCom": "2023-03-13",
    "dataPagamento": "2023-03-31",
    "dataAprovacao": "2023-02-17",
    "valor": 0.35203697246,
    "tipo": "JRS CAP PROPRIO"
  },
  {
    "ticker": "BBAS3",
    "dataCom": "2023-02-23",
    "dataPagamento": "2023-03-03",
    "dataAprovacao": "2023-02-09",
    "valor": 0.2354913913,
    "tipo": "DIVIDENDO"
  }
]
```

## Demonstrações financeiras

Em beta, lançamento dia 25/04/2023.
Terá acesso a balanços, demonstrações de resultados e demonstrações de fluxo de caixa por trimestre e por ano.

## Indicadores

Em beta, lançamento dia 30/04/2023.
Terá acesso ao histórico de indicadores também.

## Cotação mercado futuro

Disponível sob demanda. Caso tenha interesse, favor entrar em [contato][contato].

## Cotação commodities

Disponível sob demanda. Caso tenha interesse, favor entrar em [contato][contato].

## Logos e ícones

URL do ícone de um ativo listado na bolsa pelo ticker.

Suporta ações, BDRs, FIIs, e ETFs.

Esse é o único endpoint da API que utiliza outra URL.

Para acessar o ícone, basta adicionar o `ticker.png` depois da seguinte URL
```https://raw.githubusercontent.com/thefintz/icones-b3/main/icones/```

Então, por exemplo, ícone da Tesla seria TSLA34.png

```
'https://raw.githubusercontent.com/thefintz/icones-b3/main/icones/TSLA34.png'
```

**Resposta do exemplo:**

![BDR da Tesla, TSLA34](https://raw.githubusercontent.com/thefintz/icones-b3/main/icones/TSLA34.png)
