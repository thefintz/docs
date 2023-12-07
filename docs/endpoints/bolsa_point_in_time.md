[endpoint_cotacao_json]: /endpoints/bolsa/#json
[endpoint_cotacao_arquivo]: /endpoints/bolsa/#arquivo

# Point in Time (backtest)

!!! danger "Importante"
    Os endpoints dessa página são muito úteis para backtest, pois são dados point in time.
    
    Aqui vai uma explicação caso tenha dúvida sobre point in time ou backtest.

    Um exemplo fictício de como isso funciona:
    Lojas Americanas pode reportar, em março de 2022, um lucro de 1B referente a 2021.
    Os sites de investimento e dashboards vão começar a mostrar indicadores, no final de 2021, referentes a esse report. Porém, seu algoritmo de backtest não pode usar as informações publicadas em março de 2022 para testar sua estratégia e comprar/vender ações já em 31 de dezembro de 2021. Isso porque a informação só foi publicada em março de 2022. Se seu algoritmo usar essa info antes, ele vai estar "contaminado" pelo viés de look-ahead, que é utilizar-se de infos futuras.

    Talvez não tenha ficado claro, mas isso é absurdamente importante. Pode ser que seja descoberta uma fraude em Lojas Americanas 1 ano depois e eles façam o ajuste do release de 2021, mudando o lucro de 1B para -2B. Os sites e dashboards vão mostrar que houve prejuízo em 2021, mas seu algoritmo vai ter que levar em consideração quando essa info ficou pública, se não ele vai ser onisciente, já sabendo que é melhor vender esse ativo pela inevitável queda que vai surgir depois, com a descoberta da fraude e republicação dos balanços.

    Assim, a Fintz montou uma base com todos os cuidados necessários, de forma que você pode utilizar os endpoints dessa página já considerando os dados indexadas no tempo que se tornaram públicos (point in time). 

    Também já pensamos e cuidamos desses outros pontos importantes para backtest:
        - sobrevivência (survivorship): empresas delistadas também estão presentes
        - antecipação (look-ahead): os dados em determinada data são os dados disponíveis até aquela data, não depois
        - confiabilidade (data-quality): fornecemos o preço de fechamento ajustado (splits/inplits, dividendos, JCP e bonificações)

Obs: dados disponíveis desde 2010-01-01

## Contexto e Infos Gerais

### Receber Arquivos ou JSON?

Sabemos que modelos de investimentos e backtests demandam bastante processamento. Esse processamento é muitas vezes beneficiado se rodado localmente, com dados já baixados e salvos em um arquivo e carregados em dataframes.

#### Arquivos 
Assim, para você rodar efetivamente seu modelo, você pode baixar todo o histórico de um indicador, por exemplo, para todos os ativos da bolsa em apenas uma chamada para API Fintz. 
Claramente, esse histórico é pesado, por isso a resposta é um link para download do arquivo.

Então fica assim: cada vez que quiser o histórico de todos os ativos, você pode fazer uma chamada para cada item contábil ou indicador que precisar, ao invés de uma chamada para cada ativo, se tornando muito mais fácil e rápido para você.

Os arquivos são em formato `parquet`, que é basicamente um CSV comprimido. Isso porque ele é igualmente fácil de trabalhar no Pandas (ou similar), mas ocupa bem menos espaço do seu computador (e da nossa cloud ;D)

#### JSON

Antes de baixar os grandes arquivos, recomendamos testar com poucos dados, e para isso você tem os endpoints point in time que respondem JSON, com a limitação de um ativo por chamada.

### Frequência de atualização dos dados

Todo dia às 22h (Brasília) os arquivos são atualizados com os novos dados.
Tanto os dados de cotação quanto os novos releases trimestrais (ITRs e DFPs, os "balanços" ou "demonstrativos") das empresas.

Deixando bem claro: só aqui você tem acesso no mesmo dia da publicação. Se uma empresa fizer um release às 20h, no mesmo dia você já tem acesso aos dados estruturados!

## Lista de endpoints

Todos os endpoints tem a seguinte 
`BASE_URL = https://api.fintz.com.br`

No momento, são 2 endpoints:

1. Arquivo: Itens Contábeis: Histórico, todos os tickers, um item contábil: 
    - /bolsa/b3/avista/itens-contabeis/point-in-time/arquivos
2. JSON: Itens Contábeis: Histórico, um ticker, um items contábil:
    - /bolsa/b3/avista/itens-contabeis/point-in-time

Em breve:

1. Arquivo: Indicadores Histórico, um ticker, todos os indicadores:
    - /bolsa/b3/avista/indicadores/point-in-time/arquivos
2. JSON: Indicadores: Histórico, um ticker, um indicador:
    - /bolsa/b3/avista/indicadores/point-in-time

Serão descontinuados:

- (antigo) Itens Contábeis JSON
- (antigo) Itens Contábeis Arquivo
- (antigo) Indicadores JSON
- (antigo) Indicadores Arquivo

## Cotação Histórica OHLC

### Arquivo

>**GET** `/bolsa/b3/avista/cotacoes/historico/arquivos`

Este endpoint tem o mesmo comportamento point in time e não point in time. Então, para evitar documentarmos duas vezes, aqui está o link dele: [link][endpoint_cotacao_arquivo]

### JSON

>**GET** `/bolsa/b3/avista/cotacoes/historico`

Este endpoint tem o mesmo comportamento point in time e não point in time. Então, para evitar documentarmos duas vezes, aqui está o link dele: [link][endpoint_cotacao_json]

## Itens contábeis

Os itens contábeis disponíveis/selecionáveis para os próximos endpoints são os seguintes:
```
Item Contábil                                   | TRI | 12M |
- ReceitaLiquida                                |  ✓  |  ✓  |
- Custos                                        |  ✓  |  ✓  |
- ResultadoBruto                                |  ✓  |  ✓  |
- DespesasReceitasOperacionaisAdministrativas   |  ✓  |  ✓  |
- Ebit                                          |  ✓  |  ✓  |
- ResultadoFinanceiro                           |  ✓  |  ✓  |
- ReceitasFinanceiras                           |  ✓  |  ✓  |
- Lair                                          |  ✓  |  ✓  |
- Impostos                                      |  ✓  |  ✓  |
- LucroLiquidoOpContinuadas                     |  ✓  |  ✓  |
- LucroLiquidoOpDescontinuadas                  |  ✓  |  ✓  |
- LucroLiquido                                  |  ✓  |  ✓  |
- LucroLiquidoSociosControladora                |  ✓  |  ✓  |
- DepreciacaoAmortizacao                        |  ✓  |  ✓  |
- EquivalenciaPatrimonial                       |  ✓  |  ✓  |
- AtivoCirculante                               |  ✓  |  x  |
- AtivoNaoCirculante                            |  ✓  |  x  |
- AtivoTotal                                    |  ✓  |  x  |
- CaixaEquivalentes                             |  ✓  |  x  |
- DespesasFinanceiras                           |  ✓  |  x  |
- Disponibilidades                              |  ✓  |  x  |
- DividaBruta                                   |  ✓  |  x  |
- DividaLiquida                                 |  ✓  |  x  |
- Ebitda                                        |  ✓  |  x  |
- PassivoCirculante                             |  ✓  |  x  |
- PassivoNaoCirculante                          |  ✓  |  x  |
- PassivoTotal                                  |  ✓  |  x  |
- PatrimonioLiquido                             |  ✓  |  x  |
```

obs: note que não existe (aqui no _point-in-time_), para o parâmetro `tipoPeriodo`, a opção "ANUAL" como existe nos itens contábeis não _point-in-time_. 
Isso é de propósito, pois evita uma grande complexidade para o desenvolvedor/usuário.
Para pegar o último acumulado utilize o "12M".

### Arquivo: Histórico de item contábil para todos os tickers

>**GET** `/bolsa/b3/avista/itens-contabeis/point-in-time/arquivos`

Aqui você escolhe o item contábil recebe um link para arquivo com todo histórico desse item contábil escolhido para todas as empresas.

O arquivo retornado é no formato `parquet`, similar ao CSV, facilmente trabalhado com, por exemplo, a biblioteca Pandas.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `item`     | `string` | ex: `Ebit` (ver lista completa) | obrigatório
| `tipoPeriodo`    | `string` | `12M` ou `TRIMESTRAL` | obrigatório

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'item': 'Ebit', 'tipoPeriodo': '12M' }

endpoint = URL_BASE + '/bolsa/b3/avista/itens-contabeis/point-in-time/arquivos'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
{ "link": "url" }
```

### JSON: Histórico por item contábil e ticker

>**GET** `/bolsa/b3/avista/itens-contabeis/point-in-time`

Aqui você escolhe o item contábil e o ticker e recebe o histórico desse item contábil escolhido para a empresa escolhida.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `item`     | `string` | ex: `Ebit` (ver lista completa) | obrigatório
| `ticker`     | `string` | ex: `TRPL4` | obrigatório
| `tipoPeriodo`    | `string` | `12M` ou `TRIMESTRAL` | obrigatório
| `tipoDemonstracao` | `string` | vazio, `CONSOLIDADO` ou `INDIVIDUAL`  | opcional

obs: na dúvida, deixe o parâmetro `"tipoDemonstracao"` vazio, pois é o comportamento esperado na grande maioria dos casos.

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'item': 'Ebit', 'ticker': 'TRPL4', 'tipoPeriodo': '12M' }

endpoint = URL_BASE + '/bolsa/b3/avista/itens-contabeis/point-in-time'
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
    "data": "2023-10-30",
    "ano": 2023,
    "trimestre": 3,
    "valor": 3603826000
  },
  {
    "ticker": "TRPL4",
    "item": "Ebit",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "data": "2023-07-31",
    "ano": 2023,
    "trimestre": 2,
    "valor": 3549900000
  }, ...
]
```

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

### Arquivo: Histórico de indicador para todos os tickers

!!! abstract "Em breve!"
    Esse endpoint será lançado em 15/12/2023

### JSON: Histórico por item contábil e ticker

!!! abstract "Em breve!"
    Esse endpoint será lançado em 15/12/2023

## (antigo) Indicadores

>**GET** `/bolsa/b3/tm/indicadores/arquivos`

!!! info "Atenção"
    Este endpoint vai parar de funcionar em 01/03/2024. 
    
    A nova versão, aprimorada e com mais dados será lançada em 15/12/2023 e será documentada nesta mesma página.

Retorna link para um arquivo no formato .parquet (similar a CSV) que contém o histórico do indicador selecionado, para todos os tickers, desde 2010 até o último fechamento de mercado.

Não é possível passar uma lista de indicadores, pois o arquivo já é grande.

Caso queira mais de um indicador, basta fazer mais chamadas.
Caso não precise de todo o histórico, temos outro endpoint que retorna em JSON ao invés de arquivos e para apenas um ticker.

**Parâmetros**

| Parâmetro   | Tipo     | Exemplo | |
| :-:         | :-:      | - | :-: |
| `indicador` | `string` | ROE | obrigatório

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'indicador': 'ROE' }

endpoint = URL_BASE + '/bolsa/b3/tm/indicadores/arquivos'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
{
  "link": "url"
}
```

## (antigo) Arquivo: Itens contábeis

>**GET** `/bolsa/b3/tm/demonstracoes/arquivos`

!!! warning "Atenção"
    A nova versão deste endpoint já está disponível nesta página de documentação, basta olhar os endpoints sem a marcação `(antigo)`

    Este endpoint vai parar de funcionar em 01/03/2024.

Retorna link para um arquivo no formato .parquet (similar a CSV) que contém o histórico do item contábil selecionado, para todos os tickers, desde 2010 até o último fechamento de mercado.

Não é possível passar uma lista de itens contábeis, apenas um por chamada.

Caso queira mais de um item contábel, basta fazer mais chamadas.
Caso não precise de todo o histórico, temos outro endpoint que retorna em JSON ao invés de arquivos e para apenas um ticker.

**Parâmetros**

| Parâmetro   | Tipo     | Exemplo | |
| :-:         | :-:      | - | :-: |
| `item` | `string` | LucroLiquido12m | obrigatório

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'item': 'LucroLiquido12m' }

endpoint = URL_BASE + '/bolsa/b3/tm/demonstracoes/arquivos'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
{
  "link": "url"
}
```


## (antigo) Itens Contábeis Padronizados JSON

>**GET** `/bolsa/b3/tm/demonstracoes`

!!! warning "Atenção"
    A nova versão deste endpoint já está disponível nesta página de documentação, basta olhar os endpoints sem a marcação `(antigo)`

    Este endpoint vai parar de funcionar em 01/03/2024.

Retorna o histórico referente ao item contábil padronizado.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `item`  | `string` | ex: "LucroLiquido12m" | obrigatório
| `ticker`     | `string` | código de negociação | obrigatório
| `dataInicio` | `string` | (yyyy-mm-dd) | opcional
| `dataFim`    | `string` | (yyyy-mm-dd) | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = {
  'ticker': 'BBAS3',
  'item': 'LucroLiquido12m',
  'dataInicio': '2023-01-01'
}

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


## (antigo) Indicadores JSON

>**GET** `/bolsa/b3/tm/indicadores`

!!! warning "Atenção"
    A nova versão deste endpoint já está disponível nesta página de documentação, basta olhar os endpoints sem a marcação `(antigo)`

    Este endpoint vai parar de funcionar em 01/03/2024.

Retorna o histórico referente ao indicador requisitado.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `indicador`  | `string` | ex: "ROE" | obrigatório
| `ticker`     | `string` | código de negociação | obrigatório
| `dataInicio` | `string` | (yyyy-mm-dd) | opcional
| `dataFim`    | `string` | (yyyy-mm-dd) | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'BBAS3', 'indicador': 'ROE', 'dataInicio': '2023-01-01' }

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
