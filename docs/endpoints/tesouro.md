# Tesouro Direto

Permite ao usuário consultar dados de todos os títulos do Tesouro Direto, até mesmo o histórico dos títulos que não são mais negociados. 

Os dados são atualizados diariamente.

Lembrando que todos os endpoints da API tem a mesma URL Base e precisam do header "x-api-key" com sua chave.
> `URL_BASE` = `https://api.fintz.com.br`  
> `x-api-key` = `{sua chave da API Fintz}`

Obs: dados disponíveis desde 2003-01-01

## Lista de Títulos

Retorna a lista de títulos públicos disponíveis paginada.

**Parâmetros:**

- `pagina`: opcional. Inteiro que representa o índice de página. O valor
  padrão é 1, índice da primeira página.
- `tamanho`: opcional. Inteiro que indica o tamanho da página a ser retornada.
  O valor padrão é 10.

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }
PARAMS = { 'pagina': '1', 'tamanho': 40 }

endpoint = URL_BASE + '/titulos-publicos/tesouro'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
{
  "pagina": 1,
  "tamanho": 40,
  "total": 112,
  "dados": [
    {
      "codigo": "NTNF20330101",
      "nome": "Tesouro Prefixado com Juros Semestrais 2033",
      "dataVencimento": "2033-01-01",
      "vencido": false,
      "possivelInvestir": true,
      "possivelResgatar": true
    },
    ...
  ]
}
```

## Informações dos Títulos

Retorna informações extras sobre um título, como descrição e estratégia.

**Exemplo:**

Exemplo com o Título de código: `NTNBP20240815`

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }

endpoint = URL_BASE + f'/titulos-publicos/tesouro/{codigo}/informacoes'
res = req.get(endpoint, headers=HEADERS)
print(res.json())
```

**Resposta:**

```json
{
  "codigo": "NTNBP20240815",
  "nome": "Tesouro IPCA+ 2024",
  "dataVencimento": "2024-08-15",
  "indice": "IPCA",
  "vencido": false,
  "possivelInvestir": false,
  "possivelResgatar": true,
  "descricao": "Título pós-fixado, uma vez que parte do seu rendimento acompanha a variação da taxa de inflação (IPCA).",
  "estrategia": "Aumenta o poder de compra do seu dinheiro, pois seu rendimento é composto por uma taxa de juros + a variação da inflação (IPCA). É mais interessante para quem pode deixar o dinheiro render até o vencimento do investimento, pois não paga juros semestrais. Em caso de resgate antecipado, o Tesouro Nacional garante sua recompra pelo seu valor de mercado.",
  "jurosSemestrais": false
}
```

## Histórico de Preços e Taxas

Retorna histórico paginado de preços e taxas de compra e venda, com filtros por datas.

**Parâmetros:**

- `pagina`: opcional. Inteiro que representa o índice de página, para
  paginação. O valor padrão é 1, índice da primeira página.
- `tamanho`: opcional. Inteiro que indica o tamanho da página a ser retornada.
  O valor padrão é 10.
- `dataInicio`: opcional. Data do início do período a ser retornado. Formato AAAA-MM-DD.
- `dataFim`: opcional. Data do fim do período a ser retornado. Formato AAAA-MM-DD.

**Exemplo:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }
PARAMS = { 'dataInicio': '2016-12-31', 'dataFim': '2021-11-01' }

endpoint = URL_BASE + f'/titulos-publicos/tesouro/{codigo}/precos/historico'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
{
  "pagina": 1,
  "tamanho": 10,
  "total": 2597,
  "dados": [
    {
      "codigo": "NTNF20230101",
      "data": "2022-11-01",
      "taxaJurosCompra": 0.1366,
      "taxaJurosVenda": 0.1378,
      "puCompra": 1027.18,
      "puVenda": 1026.48,
      "puBase": 1026.48
    },
    {
      "codigo": "NTNF20230101",
      "data": "2022-10-31",
      "taxaJurosCompra": 0.1366,
      "taxaJurosVenda": 0.1378,
      "puCompra": 1026.66,
      "puVenda": 1025.95,
      "puBase": 1025.95
    },
    ...
  ]
}
```

## Preços e taxas atuais

Retorna preços e taxas dos títulos públicos referentes à data mais atual.
Exclusivo para títulos não vencidos.

**Exemplo:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }

endpoint = URL_BASE + f'/titulos-publicos/tesouro/{codigo}/precos/atual'
res = req.get(endpoint, headers=HEADERS)
print(res.json())
```

**Resposta:**

```json
{
  "codigo": "NTNF20330101",
  "possivelInvestir": true,
  "possivelResgatar": true,
  "taxaJurosCompra": 0.1106,
  "taxaJurosVenda": 0.1118,
  "puCompra": 982.7,
  "puVenda": 976.49,
  "minQtdVenda": 0.01,
  "minValorVenda": 9.76,
  "minValorCompra": 39.3,
  "dataUltAtualizacao": "2023-11-24T15:24:20.063000"
}
```

## Pagamentos de cupons de juros

Retorna preços e taxas dos títulos públicos referentes à data mais atual.
Exclusivo para títulos não vencidos.

**Parâmetros:**

- `pagina`: opcional. Inteiro que representa o índice de página paginação. O
  valor padrão é 1, índice da primeira página.
- `tamanho`: opcional. Inteiro que indica o tamanho da página a ser retornada.
  O valor padrão é 10.

**Exemplo:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }

endpoint = URL_BASE + f'/titulos-publicos/tesouro/{codigo}/cupons'
res = req.get(endpoint, headers=HEADERS)
print(res.json())
```

**Resposta:**

```json
{
  "pagina": 1,
  "tamanho": 10,
  "total": 23,
  "dados": [
    {
      "codigo": "NTNB20450515",
      "dataResgate": "2023-11-16",
      "dataVencimento": "2045-05-15",
      "valor": 122.980671,
      "qtdTotal": 30789.48,
      "valorTotal": 3786510.92
    },
    {
      "codigo": "NTNB20450515",
      "dataResgate": "2023-05-15",
      "dataVencimento": "2045-05-15",
      "valor": 121.758507,
      "qtdTotal": 31102.46,
      "valorTotal": 3786989.1
    },
    ...
  ]
}
```
