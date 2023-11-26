[contato]: https://fintz.com.br/#/contato
[postman]: ../../postman
[link_compra]: https://fintz.com.br/#/precos

# Bolsa B3

!!! success "Lembrete"
    Você tem acesso a uma coleção [Postman][postman].

    Também não esqueça que você precisa de uma chave de acesso à API. A chave "chave-de-testes-api-fintz" é extremamente limitada e deve ser utilizada apenas para teste inicial. 
    
    Adquira um de nossos planos para obter sua própria chave [neste link][link_compra]

## Busca e lista de ativos

>**GET** `/bolsa/b3/avista/busca`

Nesse endpoint você consegue buscar e filtrar os ativos da B3 para depois buscar dados deles.
Se não enviar nenhum filtro, retorna todos os ativos da base, inclusive os que não são mais negociados.

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
    "ticker": "BBDC3",
    "nome": "BRADESCO",
    "ativo": true // informa se pode ser negociado ou fechou capital
  }
]
```

## Cotação Histórica OHLC

### JSON

>**GET** `/bolsa/b3/avista/cotacoes/historico`

Retorna, em JSON, os preços OHLC (abertura, maxima, minima, fechamento) do ticker especificado na data especificada. Também retorna volume e quantidade negociada.

É retornado tanto o fechamento quanto o fechamento ajustado por proventos/splits/bonificações.

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

### Arquivo

>**GET** `/bolsa/b3/avista/cotacoes/historico/arquivos`

Retorna link para um arquivo no formato .parquet (similar a CSV) que contém cotação OHLC de todos os tickers, desde 2010 até o último fechamento de mercado. 

Recomendamos o uso deste endpoint apenas para uso local, como para backtests de estratégias.

Como o arquivo é grande/pesado, em sites e dashboards é melhor utilizar as chamadas JSON mesmo, até porque evita de precisar levantar um banco para guardar os dados, implementar a política de cache e configurar as rotinas de atualização.

Também é retornado um fator de ajuste, bastando multiplicá-lo pelos preços OHLC para obter o ajustado.

**Parâmetros**

Esse endpoint não tem parâmetros. O arquivo possui cotação de todos os tickers, desde 2010 até o último fechamento de mercado.

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }

endpoint = URL_BASE + '/bolsa/b3/avista/cotacoes/historico/arquivos'
res = req.get(endpoint, headers=HEADERS)
print(res.json())
```

**Resposta:**

```json
{
  "link": "url"
}
```

## Eventos

### Proventos (Dividendos, JCP, ...)

>**GET** `/bolsa/b3/avista/proventos`

Retorna os proventos em dinheiro (Dividendos, JCPs, ...) referente ao ticker e as datas especificadas na chamada.

obs: por enquanto apenas de ações. Em 15/12/2023 vamos adicionar proventos de FIIs neste mesmo endpoint.

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


### Bonificacoes

>**GET** `/bolsa/b3/avista/bonificacoes`

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

### Desdobramentos

>**GET** `/bolsa/b3/avista/desdobramentos`

Retorna os desdobramentos (splits) e grupamentos do ticker e datas especificados.

Na resposta, o atributo `"proporcao"` indica como ocorreu o evento.
Desdobramento de 1 para 10 tem proporção 0.1
Grupamento de 10 para 1 tem proporção 10

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
PARAMS = { 'ticker': 'BBAS3', 'dataInicio': '2022-01-01' }

endpoint = URL_BASE + '/bolsa/b3/avista/desdobramentos'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "SLCE3",
    "ativoEmitido": "SLCE3",
    "proporcao": 0.1,
    "dataCom": "2023-05-08",
    "dataAnuncio": "2023-04-27",
    "dataIncorporacao": "2023-05-11",
    "valorBase": 23.54
  }
]
```

## Itens contábeis

Os itens contábeis disponíveis/selecionáveis para os próximos endpoints são os seguintes:
```
- AtivoCirculante
- AtivoNaoCirculante
- AtivoTotal
- CaixaEquivalentes
- Custos
- DepreciacaoAmortizacao
- DespesasFinanceiras
- DespesasReceitasOperacionaisAdministrativas
- Disponibilidades
- DividaBruta
- DividaLiquida
- Ebit
- Ebitda
- EquivalenciaPatrimonial
- Impostos
- Lair
- LucroLiquido
- LucroLiquidoOpContinuadas
- LucroLiquidoOpDescontinuadas
- LucroLiquidoSociosControladora
- PassivoCirculante
- PassivoNaoCirculante
- PassivoTotal
- PatrimonioLiquido
- ReceitaLiquida
- ReceitasFinanceiras
- ResultadoBruto
- ResultadoFinanceiro
```

### Histórico por item contábil e ticker

>**GET** `/bolsa/b3/avista/itens-contabeis/historico`

Aqui você escolhe o item contábil e o ticker e recebe o histórico desse item contábil escolhido para a empresa escolhida.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `item`     | `string` | ex: `Ebit` (ver lista completa) | obrigatório
| `ticker`     | `string` | ex: `TRPL4` | obrigatório
| `tipoPeriodo`    | `string` | `12M`, `TRIMESTRAL` ou `ANUAL` | opcional
| `tipoDemonstracao` | `string` | vazio, `CONSOLIDADO` ou `INDIVIDUAL`  | opcional

obs: na dúvida, deixe o parâmetro `"tipoDemonstracao"` vazio, pois é o comportamento esperado na grande maioria dos casos.

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'item': 'Ebit', 'ticker': 'TRPL4', 'tipoPeriodo': '12M' }

endpoint = URL_BASE + '/bolsa/b3/avista/itens-contabeis/historico'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "TRPL4",
    "item": "Ebit",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "ano": 2023,
    "trimestre": 3,
    "valor": 3603826000
  },
  {
    "ticker": "TRPL4",
    "item": "Ebit",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "ano": 2023,
    "trimestre": 2,
    "valor": 3549900000
  }, ...
]
```

### Item contábil mais recente para todos os tickers

>**GET** `bolsa/b3/avista/itens-contabeis`

Aqui você escolhe o item contábil e recebe o valor mais recente deste item contábil para todas as empresas.

Na resposta está indicado o ano e trimestre que o dado se refere.
Algumas empresas atualizam essas informações mais rapidamente que outras, então nem todas estão com a mesma data.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `item`     | `string` | ex: `Ebit` (ver lista completa) | obrigatório
| `tipoPeriodo`    | `string` | `12M` `TRIMESTRAL` ou `ANUAL` | opcional
| `tipoDemonstracao` | `string` | vazio, `CONSOLIDADO` ou `INDIVIDUAL`  | opcional

obs: na dúvida, deixe o parâmetro `"tipoDemonstracao"` vazio, pois é o comportamento esperado na grande maioria dos casos.

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'item': 'Ebit', 'tipoPeriodo': '12M' }

endpoint = URL_BASE + '/bolsa/b3/avista/itens-contabeis'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "AESB3",
    "item": "Ebit",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "ano": 2023,
    "trimestre": 3,
    "valor": 926467000
  },
  {
    "ticker": "AGXY3",
    "item": "Ebit",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "ano": 2023,
    "trimestre": 3,
    "valor": 405492000
  }, ...
]
```

### Itens contábeis mais recentes por ticker

!!! abstract "Em breve!"
    Esse endpoint será lançado em 08/12/2023

## Indicadores

Os indicadores disponíveis/selecionáveis para os próximos endpoints são os seguintes:
```
- ROE
- ROA
- ROIC
- GiroAtivos
- MargemBruta
- MargemEbitda
- MargemEbit
- MargemLiquida
- DividaLiquida_PatrimonioLiquido
- DividaLiquida_Ebitda
- DividaLiquida_Ebit
- PatrimonioLiquido_Ativos
- Passivos_Ativos
- LiquidezCorrente
```

### Histórico por indicador e ticker

>**GET** `bolsa/b3/avista/indicadores/historico`

Aqui você escolhe o indicador e o ticker e recebe o histórico desse indicador escolhido para a empresa escolhida.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `indicador`     | `string` | ex: `ROE` (ver lista completa) | obrigatório
| `ticker`     | `string` | ex: `BBAS3` | obrigatório

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'indicador': 'ROE', 'ticker': 'BBAS3' }

endpoint = URL_BASE + '/bolsa/b3/avista/indicadores/historico'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  ...
  {
    "ticker": "BBAS3",
    "indicador": "ROE",
    "data": "2023-09-30",
    "valor": 0.1939291767457561
  },
  {
    "ticker": "BBAS3",
    "indicador": "ROE",
    "data": "2023-06-30",
    "valor": 0.19387026105337873
  },
  ...
]
```

### Indicador mais recente para todos os tickers

>**GET** `bolsa/b3/avista/indicadores`

Aqui você escolhe o indicador e recebe o valor mais recente deste indicador para todas as empresas.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `indicador`     | `string` | ex: `ROE` (ver lista completa) | obrigatório

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'indicador': 'ROE' }

endpoint = URL_BASE + '/bolsa/b3/avista/indicadores'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  ... 
  {
    "ticker": "BBAS3",
    "indicador": "ROE",
    "data": "2023-09-30",
    "valor": 0.1939291767457561
  },
  {
    "ticker": "BBDC3",
    "indicador": "ROE",
    "data": "2023-09-30",
    "valor": 0.08024657432331474
  }, 
  ...
]
```

### Indicadores mais recentes por ticker

!!! abstract "Em breve!"
    Esse endpoint será lançado em 08/12/2023

## DRE, BP, DFC crus da CVM

>**GET** `bolsa/b3/demonstracoes/{tipo}`

!!! abstract "Em breve!"
    Esse endpoint será lançado em 29/01/2024

## Aluguel de ações

!!! abstract "Em breve!"
    Esse endpoint será lançado no primeiro semestre de 2024.

    Caso precise com urgência, [entre em contato][contato] para priorizarmos

## Cotação mercado futuro

!!! info "Restrito!"
    Disponível apenas demanda. Caso tenha interesse, favor entrar em [contato][contato].

## Cotação commodities

!!! info "Restrito!"
    Disponível apenas demanda. Caso tenha interesse, favor entrar em [contato][contato].

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
