[contato]: https://fintz.com.br/#/contato

# Bolsa B3

!!! warning "Lembrete"
    Você precisa de uma chave de acesso à API. A chave "chave-de-testes-api-fintz" é extremamente limitada e deve ser utilizada apenas para teste inicial. 
    Entre em contato em contato@fintz.com.br para conseguir a sua chave própria e robusta.

## Busca e lista de ativos

** /bolsa/b3/avista/busca **

Nesse endpoint você consegue buscar e filtrar os ativos da B3 para depois buscar dados deles.
Se não enviar nenhum filtro, retorna todos os ativos da base, inclusive o que não são mais negociados.

Todos os ativos da bolsa B3 estão disponíveis (ações, FIIs, ETFs, BDRs, ...).

Um exemplo de uso, você pode filtrar apenas os ativos do setor de tecnologia, ou mesmo pode conectar a sua search bar para buscar pelo nome ou ticker do ativo.

**Parâmetros**

| Parâmetro | Tipo |Descrição | |
| :-: | :-: | - | :-: |
| `q`     | `string` | ex: "BBAS" vai retornar o "BBAS3" | opcional
| `classe` | `string` | BDRS, ACOES, FUNDOS, FIIS ou TODOS | opcional


**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'q': 'BBAS' }

endpoint = URL_BASE + '/bolsa/b3/avista/busca'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
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

## Cotação histórica

** /bolsa/b3/avista/cotacoes/historico **

Retorna os preços de fechamento do ticker especificado na data especificada.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `ticker`     | `string` | código de negociação | obrigatório
| `dataInicio` | `string` | (yyyy-mm-dd) | obrigatório
| `dataFim`    | `string` | (yyyy-mm-dd) | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'BBAS3', 'dataInicio': '2023-04-01' }

endpoint = URL_BASE + '/bolsa/b3/avista/cotacoes/historico'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
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

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `ticker`     | `string` | código de negociação | obrigatório
| `dataInicio` | `string` | (yyyy-mm-dd) | obrigatório
| `dataFim`    | `string` | (yyyy-mm-dd) | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'BBAS3', 'dataInicio': '2023-01-01' }

endpoint = URL_BASE + '/bolsa/b3/avista/proventos'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
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


## Bonificacoes

** /bolsa/b3/avista/bonificacoes **

Retorna as bonificacoes do ticker e datas especificados.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `ticker`     | `string` | código de negociação | obrigatório
| `dataInicio` | `string` | (yyyy-mm-dd) | obrigatório
| `dataFim`    | `string` | (yyyy-mm-dd) | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'BBDC3', 'dataInicio': '2020-01-01' }

endpoint = URL_BASE + '/bolsa/b3/avista/bonificacoes'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "BBDC3",
    "ativoEmitido": "BBDC3",
    "proporcao": 0.1,
    "dataCom": "2022-04-18",
    "dataAnuncio": "2022-03-10",
    "dataIncorporacao": "2022-04-22",
    "valorBase": 4.13
  },
  {
    "ticker": "BBDC3",
    "ativoEmitido": "BBDC3",
    "proporcao": 0.1,
    "dataCom": "2021-04-16",
    "dataAnuncio": "2021-04-07",
    "dataIncorporacao": "2021-04-22",
    "valorBase": 4.53
  },
  ...
]
```

## Desdobramentos

** /bolsa/b3/avista/desdobramentos **

Retorna os desdobramentos (splits) e grupamentos do ticker e datas especificados.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `ticker`     | `string` | do código de negociação | obrigatório
| `dataInicio` | `string` | (yyyy-mm-dd) | obrigatório
| `dataFim`    | `string` | (yyyy-mm-dd) | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'BBAS3', 'dataInicio': '2023-01-01' }

endpoint = URL_BASE + '/bolsa/b3/avista/desdobramentos'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
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

## Indicadores


!!! success "Novidade!"
    Esse endpoint acaba de ser lançado e estamos adicionando indicadores continuamente.
    
    Tem algum indicador que deseja ser adicionado o quanto antes?
    Só mandar pelo email contato@fintz.com.br

** /bolsa/b3/tm/indicadores **

Retorna o histórico referente ao indicador requisitado.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `indicador`  | `string` | ex: "ROE" | obrigatório
| `dataInicio` | `string` | (yyyy-mm-dd) | opcional
| `dataFim`    | `string` | (yyyy-mm-dd) | opcional
| `ticker`     | `string` | código de negociação | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'indicador': 'ROE', 'dataInicio': '2023-01-01' }

endpoint = URL_BASE + '/bolsa/b3/tm/indicadores'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
      "t": "BBAS3", # ticker
      "i": "roe", # indicador
      "di": "2015-02-11T08:24:11.850000", # data inicio
      "df": "2015-03-27T08:18:34.097000", # data fim
      "v": 0.14519 # valor
  },
  {
      "t": "BBAS3",
      "i": "roe",
      "di": "2015-03-27T08:18:34.097000",
      "df": "2015-05-14T08:26:41.240000",
      "v": 0.15617
  },
  ...
]
```


Os indicadores atualmente disponíveis são
```
ROE
ROIC
LPA
P_L
L_P
EV
EV_EBIT
ValorDeMercado
```

Precisa de algum outro indicador? [Entre em contato][contato] e adicionamos gratuitamente.


## Itens contábeis padronizados

** /bolsa/b3/tm/demonstracoes **

Retorna o histórico referente ao item contábil padronizado.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `item`  | `string` | ex: "LucroLiquido12m" | obrigatório
| `dataInicio` | `string` | (yyyy-mm-dd) | opcional
| `dataFim`    | `string` | (yyyy-mm-dd) | opcional
| `ticker`     | `string` | código de negociação | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'item': 'LucroLiquido12m', 'dataInicio': '2023-01-01' }

endpoint = URL_BASE + '/bolsa/b3/tm/demonstracoes'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
      "t": "BBAS3", # ticker
      "i": "LucroLiquido12m", # item contábil
      "di": "2012-02-14T09:49:04.487000", # data inicial
      "df": "2012-03-30T18:15:39.613000", # data final
      "v": 12247330000.0 # valor
  },
  {
      "t": "BBAS3",
      "i": "LucroLiquido12m",
      "di": "2012-03-30T18:15:39.613000",
      "df": "2012-05-03T10:08:04.667000",
      "v": 12736912000.0
  },
  ...
]
```


Os itens contábeis atualmente disponíveis são
```
PatrimonioLiquido
LucroLiquido12m
LucroLiquido
ReceitaLiquida
ReceitaLiquida12m
DividaBruta
DividaLiquida
Disponibilidades
Ebit
Ebit12m
Impostos
Impostos12m
AcoesEmCirculacao
TotalAcoes
LucroLiquidoSociosControladora
LucroLiquidoSociosControladora12m
```

Precisa de algum outro item contábil? [Entre em contato][contato] e adicionamos gratuitamente.

## DRE, BP, DFC crus da CVM

** /bolsa/b3/demonstracoes/{tipo} **

Retorna a demonstração financeira especificada, de maneira completa e crua (sem padronização), como está na CVM.

Hoje, a API retorna dados para as seguintes demonstrações financeiras ({tipo})  
- `dre`: Demonstração de Resultados  
- `bpa`: Balanço Patrimonial Ativo  
- `bpp`: Balanço Patrimonial Passivo  
- `dfc`: Demonstração do Fluxo de Caixa  
No caso da DFC, retornamos tanto o MD (método direto) quanto o MI (método indireto).
Para todos os casos, retornamos tanto o Consolidado quanto o Individual.

Atenção: o {tipo} é em letra minúscula, por exemplo:  
`/bolsa/b3/demonstracoes/dre`

**Parâmetros**

| Parâmetro   | Tipo     | Exemplo | |
| :-:         | :-:      | - | :-: |
| `ticker`    | `string` | BBAS3 | obrigatório
| `ano`       | `string` | 2022 | obrigatório
| `trimestre` | `string` | 4 | obrigatório

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'BBAS3', 'ano': '2022', 'trimestre': '4' }

endpoint = URL_BASE + '/bolsa/b3/demonstracoes/DRE'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "nome": "BCO BRASIL S.A.",
    "tipo_demonstracao": "CONSOLIDADO",
    "data_inicio_exercicio": "2022-01-01",
    "data_fim_exercicio": "2022-12-31",
    "codigo_conta": "3.01",
    "descricao_conta": "Receitas de Intermediação Financeira",
    "valor_conta": 236549051000,
    "demonstracao": "DRE"
  },
  {
    "nome": "BCO BRASIL S.A.",
    "tipo_demonstracao": "CONSOLIDADO",
    "data_inicio_exercicio": "2022-01-01",
    "data_fim_exercicio": "2022-12-31",
    "codigo_conta": "3.01.01",
    "descricao_conta": "Receita de Juros",
    "valor_conta": 236549051000,
    "demonstracao": "DRE"
  },
  ...
]
```


Precisa de alguma outra demonstração financeira? [Entre em contato][contato] e adicionamos gratuitamente.

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
