[contato]: https://fintz.com.br/#/contato
[postman]: ../../postman
[link_compra]: https://fintz.com.br/#/precos

# Bolsa B3

!!! success "Lembrete"
    Você tem acesso a uma coleção [Postman][postman].

    Também não esqueça que você precisa de uma chave de acesso à API. A chave "chave-de-teste-api-fintz" é extremamente limitada e deve ser utilizada apenas para teste inicial. 
    
    Adquira um de nossos planos para obter sua própria chave [neste link][link_compra]

Obs: dados disponíveis desde 2010-01-01

## Busca e lista de ativos

>**GET** `/bolsa/b3/avista/busca`

Este endpoint permite buscar e filtrar os ativos negociados no mercado à vista da B3. 
Você pode realizar pesquisas específicas ou obter uma lista completa de todos os ativos disponíveis,
incluindo aqueles que não são mais negociados.

Os ativos abrangem diversas categorias, como ações, Fundos de Investimento Imobiliário (FIIs),
Exchange-Traded Funds (ETFs), Brazilian Depositary Receipts (BDRs), entre outros.

**Uso Comum:**

* Integrar com uma barra de pesquisa para localizar ativos pelo ticker.
* Filtrar apenas os FIIs que são negociados atualmente.

**Parâmetros**

| Parâmetro |   Tipo    | Descrição                          |          |
|:---------:|:---------:|------------------------------------|:--------:|
|    `q`    | `string`  | ex: "BBAS" vai retornar o "BBAS3"  | opcional |
| `classe`  | `string`  | BDRS, ACOES, FUNDOS, FIIS ou TODOS | opcional |
|  `ativo`  | `boolean` | `true` ou `false`                  | opcional |

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'q': 'BBDC' }

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

Este endpoint fornece os dados históricos de cotação dos ativos negociados na B3.
As informações são apresentadas no formato OHLC (Open - High - Low - Close, ou 
Abertura - Máxima - Mínima - Fechamento) para o ticker especificado e dentro do intervalo de datas determinado.
Adicionalmente, são fornecidos dados sobre o volume e a quantidade negociada,
bem como o fechamento ajustado por eventos corporativos como proventos, splits e bonificações.

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

Este endpoint fornece um link para download de um arquivo no formato .parquet (similar ao CSV),
contendo as cotações OHLC (Open - High - Low - Close, ou Abertura - Máxima - Mínima - Fechamento)
de todos os tickers da B3, desde 2010 até o último fechamento de mercado.

Além disso, é retornado um fator de ajuste, que pode ser multiplicado pelos preços OHLC para obter os
valores ajustados por eventos corporativos, como proventos, splits e bonificações.

**Uso Recomendado:**

* Ideal para uso local, como backtests de estratégias de trading.
* Devido ao tamanho e peso do arquivo, é mais adequado para análises offline do que para uso em websites 
e dashboards.


**Parâmetros**

Esse endpoint só possui um parâmetro:

|  Parâmetro  |   Tipo    | Descrição                                                                                                  |          |
|:-----------:|:---------:|------------------------------------------------------------------------------------------------------------|:--------:|
| `preencher` | `boolean` | `true` ou `false`. Preenche os dias sem negociação com a cotação anterior. O comportamento padrão é false. | opcional |

**Funcionalidade do Parâmetro preencher:**

* Quando `preencher` é definido como `true`, preenche os dias sem negociação de ativos com pouca liquidez usando a
cotação do dia anterior, evitando lacunas nos dados.
* Se `preencher` não for especificado, ou for definido como `false`, dias sem negociação não serão preenchidos.

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

Este endpoint retorna os proventos em dinheiro (Dividendos, JCPs, etc.) referentes ao ticker especificado
na chamada. Atualmente, o serviço abrange apenas proventos de ações. A funcionalidade para incluir proventos
de Fundos de Investimento Imobiliário (FIIs) será adicionada a este endpoint em breve.

**Parâmetros**

|  Parâmetro   |   Tipo   | Descrição            |             |
|:------------:|:--------:|----------------------|:-----------:|
|   `ticker`   | `string` | código de negociação | obrigatório |
| `dataInicio` | `string` | (yyyy-mm-dd)         | obrigatório |
|  `dataFim`   | `string` | (yyyy-mm-dd)         |  opcional   |

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

Este endpoint fornece informações sobre bonificações de empresas listadas na B3.
Bonificações são ações adicionais distribuídas aos acionistas. 
Usando este endpoint, é possível consultar as bonificações por ticker e intervalo de datas.

**Parâmetros**

|  Parâmetro   |   Tipo   | Descrição            |             |
|:------------:|:--------:|----------------------|:-----------:|
|   `ticker`   | `string` | código de negociação | obrigatório |
| `dataInicio` | `string` | (yyyy-mm-dd)         | obrigatório |
|  `dataFim`   | `string` | (yyyy-mm-dd)         |  opcional   |

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

Este endpoint oferece informações sobre desdobramentos (splits) e grupamentos de ativos listados na B3.
Estes eventos ajustam o número de ações em circulação, alterando o valor por ação sem modificar o valor de mercado
da empresa.

**Parâmetros**

|  Parâmetro   |   Tipo   | Descrição            |             |
|:------------:|:--------:|----------------------|:-----------:|
|   `ticker`   | `string` | código de negociação | obrigatório |
| `dataInicio` | `string` | (yyyy-mm-dd)         | obrigatório |
|  `dataFim`   | `string` | (yyyy-mm-dd)         |  opcional   |

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'OIBR3', 'dataInicio': '2022-01-01' }

endpoint = URL_BASE + '/bolsa/b3/avista/desdobramentos'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "OIBR3",
    "valorAntes": 10.0,
    "valorDepois": 1.0,
    "dataCom": "2023-01-06",
    "dataAnuncio": "2022-12-01",
    "tipo": "GRUPAMENTO"
  }
]
```

**Interpretação dos Campos `valorAntes` e `valorDepois`:**

Estes campos indicam a proporção do desdobramento ou grupamento.
Por exemplo, um grupamento onde o investidor tinha 10 ações e após o evento passa a ter 1 ação é indicado por
`valorAntes` = 10 e `valorDepois` = 1. Da mesma forma, um desdobramento onde 1 ação se torna 10 é indicado por
`valorAntes` = 1 e `valorDepois` = 10.

## Itens contábeis

Os seguintes itens contábeis podem ser consultados nos próximos endpoints, disponíveis em diferentes periodicidades:
Os itens contábeis disponíveis/selecionáveis para os próximos endpoints são os seguintes:


| Item Contábil                                    | TRI | ANO | 12M |
|--------------------------------------------------|:---:|:---:|:---:|
| ReceitaLiquida                                   |  ✓  |  ✓  |  ✓  |
| Custos                                           |  ✓  |  ✓  |  ✓  |
| ResultadoBruto                                   |  ✓  |  ✓  |  ✓  |
| DespesasReceitasOperacionaisOuAdministrativas    |  ✓  |  ✓  |  ✓  |
| EBIT                                             |  ✓  |  ✓  |  ✓  |
| EBITDA                                           |  ✓  |  ✓  |  ✓  |
| ResultadoFinanceiro                              |  ✓  |  ✓  |  ✓  |
| ReceitasFinanceiras                              |  ✓  |  ✓  |  ✓  |
| LAIR                                             |  ✓  |  ✓  |  ✓  |
| Impostos                                         |  ✓  |  ✓  |  ✓  |
| LucroLiquidoOperacoesContinuadas                 |  ✓  |  ✓  |  ✓  |
| LucroLiquidoOperacoesDescontinuadas              |  ✓  |  ✓  |  ✓  |
| LucroLiquido                                     |  ✓  |  ✓  |  ✓  |
| LucroLiquidoSociosControladora                   |  ✓  |  ✓  |  ✓  |
| DepreciacaoAmortizacao                           |  ✓  |  ✓  |  ✓  |
| EquivalenciaPatrimonial                          |  ✓  |  ✓  |  ✓  |
| AtivoCirculante                                  |  ✓  |  ✓  |  x  |
| AtivoNaoCirculante                               |  ✓  |  ✓  |  x  |
| AtivoTotal                                       |  ✓  |  ✓  |  x  |
| CaixaEquivalentes                                |  ✓  |  ✓  |  x  |
| DespesasFinanceiras                              |  ✓  |  ✓  |  x  |
| Disponibilidades                                 |  ✓  |  ✓  |  x  |
| DividaBruta                                      |  ✓  |  ✓  |  x  |
| DividaLiquida                                    |  ✓  |  ✓  |  x  |
| PassivoCirculante                                |  ✓  |  ✓  |  x  |
| PassivoNaoCirculante                             |  ✓  |  ✓  |  x  |
| PassivoTotal                                     |  ✓  |  ✓  |  x  |
| PatrimonioLiquido                                |  ✓  |  ✓  |  x  |


**Interpretação dos Dados:**

* Dados Trimestrais e Anuais: podem ser consultados para todos os itens listados.
* Os dados anuais são obtidos exclusivamente a partir das Demonstrações Financeiras Padronizadas (DFPs). 
Portanto, estes dados correspondem ao ano fiscal da empresa, que pode diferir do ano calendário.
* Acumulado 12 Meses (12M): aplica-se apenas a certos itens e representa a soma dos valores dos trimestres
que compõem esses 12 meses. Por exemplo, a Receita Líquida pode ser somada ao longo de quatro trimestres para obter o
total acumulado em 12 meses.

**Observações Específicas:**

* Itens do balanço patrimonial, como o Ativo Total, não são acumulativos e, portanto, não são aplicáveis ao conceito
de 12M. Estes representam valores específicos em um determinado momento, refletindo a situação patrimonial da empresa
naquela data.

* Itens como Receita Líquida, que fazem parte da DRE, são acumulativos. Eles podem ser somados ao longo dos
trimestres para calcular o total de 12 meses, oferecendo uma visão ampliada do desempenho financeiro 
da empresa ao longo do ano.

**Explicação do `tipoDemonstracao`:**

As demonstrações consolidadas agregam as informações financeiras de uma empresa matriz e suas subsidiárias,
oferecendo uma visão global do grupo empresarial. Elas removem as transações internas para apresentar a situação
financeira do conjunto. 

As demonstrações individuais focam nos dados financeiros de uma única empresa, sem considerar suas afiliadas
ou subsidiárias, proporcionando uma análise específica daquela empresa. 

Enquanto as consolidadas são úteis para entender o desempenho do grupo como um todo, as individuais são importantes
para avaliar a saúde financeira de uma empresa isolada.

Este parâmetro estará presente nos endpoints de itens contábeis e pode ser usado para escolher uma ou
outra demonstração.

* O comportamento padrão, ao não informar este parâmetro, é exibir dados CONSOLIDADOS se disponíveis. No entanto, 
se apenas dados INDIVIDUAIS estiverem disponíveis, estes serão exibidos.
* A especificação de `CONSOLIDADO` ou `INDIVIDUAL` é necessária apenas se você deseja forçar a exibição de um
tipo específico de dado, ignorando o comportamento padrão.

Observação: Se houver incerteza, é recomendável não informar o parâmetro `tipoDemonstracao`, uma vez que essa é a 
abordagem padrão para a maioria das situações.

### Histórico por Item Contábil e Ticker

>**GET** `/bolsa/b3/avista/itens-contabeis/historico`

Este endpoint possibilita a consulta do histórico financeiro de um item contábil específico para uma empresa
listada na B3, baseado no ticker fornecido.

**Parâmetros**

|     Parâmetro      |   Tipo   | Descrição                                                         |             |
|:------------------:|:--------:|-------------------------------------------------------------------|:-----------:|
|       `item`       | `string` | Nome do item contábil (ex: `EBIT`). Consulte a lista completa.    | obrigatório |
|      `ticker`      | `string` | Código de negociação da empresa (ex: `TRPL4`).                    | obrigatório |
|   `tipoPeriodo`    | `string` | Periodicidade dos dados: `12M`, `TRIMESTRAL` ou `ANUAL`.          | obrigatório |
| `tipoDemonstracao` | `string` | Tipo de demonstração: `CONSOLIDADO`, `INDIVIDUAL` ou não informe. |  opcional   |

Observação: Se houver incerteza, é recomendável não informar o parâmetro `tipoDemonstracao`, uma vez que essa é a 
abordagem padrão para a maioria das situações. Para mais detalhes consulte a explicação deste parâmetro.

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'item': 'EBIT', 'ticker': 'TRPL4', 'tipoPeriodo': '12M' }

endpoint = URL_BASE + '/bolsa/b3/avista/itens-contabeis/historico'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "TRPL4",
    "item": "EBIT",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "ano": 2023,
    "trimestre": 3,
    "valor": 3603826000
  },
  {
    "ticker": "TRPL4",
    "item": "EBIT",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "ano": 2023,
    "trimestre": 2,
    "valor": 3549900000
  }, ...
]
```

### Valor Mais Recente de Item Contábil para Todos os Tickers

>**GET** `bolsa/b3/avista/itens-contabeis`

Este endpoint permite consultar o valor mais recente de um item contábil específico para todas as empresas
listadas na B3. A resposta inclui o ano e o trimestre aos quais os dados se referem, refletindo que algumas empresas
podem atualizar as suas informações mais rapidamente que outras.

**Parâmetros**

|     Parâmetro      |   Tipo   | Descrição                                                       |             |
|:------------------:|:--------:|-----------------------------------------------------------------|:-----------:|
|       `item`       | `string` | Nome do item contábil (ex: `EBIT`). Consulte a lista completa.  | obrigatório |
|   `tipoPeriodo`    | `string` | Periodicidade dos dados: `12M`, `TRIMESTRAL` ou `ANUAL`.        |  opcional   |
| `tipoDemonstracao` | `string` | ipo de demonstração: `CONSOLIDADO`, `INDIVIDUAL` ou não informe |  opcional   |

Observação: Se houver incerteza, é recomendável não informar o parâmetro `tipoDemonstracao`, uma vez que essa é a 
abordagem padrão para a maioria das situações. Para mais detalhes consulte a explicação deste parâmetro.

O parâmetro `tipoPeriodo` é definido como `12M` por padrão. É aconselhável sempre especificar este parâmetro para garantir
clareza e explicitar o comportamento desejado.

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'item': 'EBIT', 'tipoPeriodo': '12M' }

endpoint = URL_BASE + '/bolsa/b3/avista/itens-contabeis'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "AESB3",
    "item": "EBIT",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "ano": 2023,
    "trimestre": 3,
    "valor": 926467000
  },
  {
    "ticker": "AGXY3",
    "item": "EBIT",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "ano": 2023,
    "trimestre": 3,
    "valor": 405492000
  }, ...
]
```

### Itens Contábeis Mais Recentes por Ticker


>**GET** `bolsa/b3/avista/itens-contabeis/por-ticker`

Este endpoint permite que você selecione um ticker de empresa listada na B3 e obtenha todos os itens contábeis 
mais recentes relacionados a esse ticker.

As datas na resposta podem parecer antigas, mas refletem a data de referência do último informe trimestral divulgado,
que é a última atualização disponível. Estes dados permanecem válidos até uma nova atualização.

**Parâmetros**

|     Parâmetro      |   Tipo   | Descrição                      |             |
|:------------------:|:--------:|--------------------------------|:-----------:|
|      `ticker`      | `string` | Código do ativo, ex: TAEE11.   | obrigatório |
|   `tipoPeriodo`    | `string` | `12M`, `TRIMESTRAL` ou `ANUAL` |  opcional   |
| `tipoDemonstracao` | `string` | `CONSOLIDADO` ou `INDIVIDUAL`  |  opcional   |

Observação: Se houver incerteza, é recomendável não informar o parâmetro `tipoDemonstracao`, uma vez que essa é a 
abordagem padrão para a maioria das situações. Para mais detalhes consulte a explicação deste parâmetro.

Caso o `tipoPeriodo` não seja especificado, a resposta incluirá apenas uma versão de período para cada item
contábil, com prioridade para `12M`, seguido por `TRIMESTRAL`. Por exemplo, apenas `EBIT 12M` será retornado para o 
EBIT, enquanto `AtivoTotal TRIMESTRAL` será retornado para o Ativo Total. Se `tipoPeriodo` for especificado, somente
itens desse período específico serão retornados.



**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'TAEE11' }

endpoint = URL_BASE + '/bolsa/b3/avista/itens-contabeis/por-ticker'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "ticker": "TAEE11",
    "item": "EBIT",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "ano": 2023,
    "trimestre": 3,
    "valor": 1844690000.0
  },
  {
    "ticker": "TAEE11",
    "item": "ReceitaLiquida",
    "tipoPeriodo": "12M",
    "tipoDemonstracao": "CONSOLIDADO",
    "ano": 2023,
    "trimestre": 3,
    "valor": 2567241000.0
  }
  ...
]
```

## Indicadores

Selecione "Ações" ou "FIIs" para ver os indicadores disponíveis para cada classe de ativo.

=== "Ações"

    ```
    ValorDeMercado 
    EV 
    P_L
    P_VP 
    VPA
    LPA
    DividendYield
    EV_EBITDA
    EV_EBIT
    P_EBITDA 
    P_EBIT 
    P_Ativos 
    P_SR 
    P_CapitalDeGiro
    P_AtivoCirculanteLiquido 
    ROE
    ROA
    ROIC 
    GiroAtivos 
    MargemBruta
    MargemEBITDA 
    MargemEBIT 
    MargemLiquida
    DividaLiquida_PatrimonioLiquido
    DividaLiquida_EBITDA 
    DividaLiquida_EBIT 
    PatrimonioLiquido_Ativos 
    Passivos_Ativos
    LiquidezCorrente 
    DividaBruta_PatrimonioLiquido
    EBIT_Ativos
    EBIT_DespesasFinanceiras 
    EBITDA_DespesasFinanceiras 
    EBITDA_EV
    EBIT_EV
    L_P
    ```

=== "FIIs"

    ```
    P_VP
    DividendYield
    PatrimonioLiquido
    VP_QuantidadeCotas
    Caixa
    Caixa_VP
    NumeroCotistas
    QuantidadeCotas
    ```

### Histórico de Indicadores por Ticker

>**GET** `bolsa/b3/avista/indicadores/historico`

Este endpoint permite a consulta do histórico de um indicador financeiro específico para uma empresa listada na B3,
usando seu ticker.

**Parâmetros**

|  Parâmetro  |   Tipo   | Descrição                                          |             |
|:-----------:|:--------:|----------------------------------------------------|:-----------:|
| `indicador` | `string` | Nome do indicador, ex: ROE. Veja a lista completa. | obrigatório |
|  `ticker`   | `string` | Código do ativo, ex: BBAS3.                        | obrigatório |

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

Observação: As datas na resposta representam a data de referência do documento de origem do indicador. Embora alguns
indicadores trimestrais possam parecer desatualizados, todos os indicadores estão sempre atualizados,
com aqueles baseados em preços refletindo as datas mais recentes

### Valor Mais Recente de Indicador para Todos os Tickers

>**GET** `bolsa/b3/avista/indicadores`

Este endpoint oferece a possibilidade de selecionar um indicador financeiro e obter o seu valor mais recente para todas
as empresas listadas na B3.

**Parâmetros**

|  Parâmetro  |   Tipo   | Descrição                                                                         |             |
|:-----------:|:--------:|-----------------------------------------------------------------------------------|:-----------:|
| `indicador` | `string` | Nome do indicador, ex: ROE. Consulte a lista completa de indicadores disponíveis. | obrigatório |
| `classe` | `string` | 'ACOES' ou 'FIIS'. Se não colocar, é 'ACOES' |

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

Observação: As datas na resposta representam a data de referência do documento de origem do indicador. Embora alguns
indicadores trimestrais possam parecer desatualizados, todos os indicadores estão sempre atualizados,
com aqueles baseados em preços refletindo as datas mais recentes.


### Indicadores Mais Recentes por Ticker


>**GET** `bolsa/b3/avista/indicadores/por-ticker`

Este endpoint permite selecionar um ticker de uma empresa listada na B3 e acessar todos os indicadores financeiros mais
recentes para esse ticker.

Alguns indicadores podem não ser aplicáveis a certos tipos de empresas, como `DividaLiquida_EBITDA` para empresas
financeiras. Nestes casos, esses indicadores específicos não serão incluídos na resposta.

**Parâmetros**

| Parâmetro |   Tipo   | Descrição                    |             |
|:---------:|:--------:|------------------------------|:-----------:|
| `ticker`  | `string` | Código do ativo, ex: TAEE11. | obrigatório |

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-teste-api-fintz' }
PARAMS = { 'ticker': 'TAEE11' }

endpoint = URL_BASE + '/bolsa/b3/avista/indicadores/por-ticker'
res = req.get(endpoint, headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  ... 
  {
    "ticker": "TAEE11",
    "indicador": "P_L",
    "data": "2023-12-19",
    "valor": 11.2687
  },
  {
    "ticker": "TAEE11",
    "indicador": "ROE",
    "data": "2023-11-08",
    "valor": 0.13662
  }, 
  ...
]
```

## DRE, BP, DFC crus da CVM

>**GET** `bolsa/b3/demonstracoes/{tipo}`

!!! abstract "Em breve!"
    Esse endpoint será lançado em 15/05/2024

## Aluguel de ações

!!! abstract "Em breve!"
    Esse endpoint não está em desenvolvimento.

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
