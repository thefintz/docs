[contato]: https://fintz.com.br/#/contato

# Bolsa B3

Todos os endpoints desta página têm a seguinte URL base:
> `URL_BASE` =  `https://fintz.herokuapp.com/api`

## Cotações

### Cotação atual por ticker

Retorna o último preço de fechamento do ticker especificado, que representa o
código de negociação do ativo na bolsa brasileira (B3).

**Parâmetros**

- `TIPO`: pode ser `acoes`, `bdrs`, `fiis` ou `etfs`
- `TICKER`: uma `string` de 6 caracteres

**Exemplo de chamada:**

```bash
curl '{URL_BASE}/b3/{TIPO}/{TICKER}/preco'
```

**Resposta:**

```json
{
  "ticker": "TAEE11",
  "preco": 43.68
}
```

### Cotação histórica

Retorna os preços de fechamento de todos os tickers especificados no período indicado.

**Parâmetros**

- `TICKERS`: lista de `string`s de 6 caracteres que representam o código de negociação do ativo na bolsa brasileira (B3)
- `dataPregStart`: data no formato AAAA-MM-DD
- `dataPregEnd`: data no formato AAAA-MM-DD

**Exemplo de chamada:**

```bash
curl '{URL_BASE}/b3/ativos/cotacoes?tickers=TAEE11,PETR4&dataPregStart=2022-08-01&dataPregEnd=2022-08-03'
```

**Resposta:**

```json
[
  [
    {
      "precoUltimo": 33.88,
      "precoAbertura": 34.01,
      "precoMaximo": 34.16,
      "precoMinimo": 33.56,
      "precoMedio": 33.87,
      "volumeTotal": 2.220163E9,
      "dataPreg": "2022-08-03",
      "prazoTermo": null,
      "dataVencimento": "9999-12-31",
      "ticker": "PETR4"
    },
    {
      "precoUltimo": 33.83,
      "precoAbertura": 33.77,
      "precoMaximo": 34.5,
      "precoMinimo": 33.48,
      "precoMedio": 33.89,
      "volumeTotal": 2.3435768E9,
      "dataPreg": "2022-08-02",
      "prazoTermo": null,
      "dataVencimento": "9999-12-31",
      "ticker": "PETR4"
    }
  ],
  [
    {
      "precoUltimo": 41.27,
      "precoAbertura": 41.4,
      "precoMaximo": 41.64,
      "precoMinimo": 41.09,
      "precoMedio": 41.37,
      "volumeTotal": 8.845676E7,
      "dataPreg": "2022-08-03",
      "prazoTermo": null,
      "dataVencimento": "9999-12-31",
      "ticker": "TAEE11"
    },
    {
      "precoUltimo": 41.27,
      "precoAbertura": 40.84,
      "precoMaximo": 41.53,
      "precoMinimo": 40.53,
      "precoMedio": 41.3,
      "volumeTotal": 1.0879791E8,
      "dataPreg": "2022-08-02",
      "prazoTermo": null,
      "dataVencimento": "9999-12-31",
      "ticker": "TAEE11"
    }
  ]
]
```

### Cotação mercado futuro

Disponível sob demanda. Caso tenha interesse, favor entrar em [contato][contato].

## Indicadores

### Indicadores por ticker

Retorna os indicadores fundamentalistas de um ativo listado na bolsa pelo ticker.

**Parâmetros**

- `TICKER`: um `string`, _case insensitive_ com o código de negociação do ativo desejado. Exemplo: `TAEE11` ou `PETR4`.

**Exemplo de chamada:**

```bash
curl '{URL_BASE}/b3/acoes/{{TICKER}}/indicadores'
```

**Resposta:**
```json
{
  "data": "2022-01-19T00:00:00Z",
  "ticker": "PETR3",
  "empresa": "PETROBRAS ON",
  "setor": "Petroleo, Gas e Biocombustiveis",
  "subsetor": "Exploracao, Refino e Distribuicao",
  "tipoDoAtivo": "ON",
  "valorDaFirma": 708584000000,
  "valorDeMercado": 446774000000,
  "ultimoBalancoProcessado": "2021-09-30T00:00:00Z",
  "dy": "0.165",
  "vpa": "28.29",
  "lpa": "10.35",
  "roic": "0.196",
  "roe": "0.366",
  "liquidezCorrente": "1.2",
  "margemEbit": "0.44",
  "margemBruta": "0.511",
  "margemLiquida": "0.346",
  "evEbitda": "2.98",
  "receitaLiquida12Meses": 393450000000,
  "pl": "3.31",
  "pvp": "1.21",
  "pebit": "2.58"
}
```

### Indicadores por lista de tickers

Retorna uma lista de indicadores de empresas listadas na bolsa, filtradas por paramêtros.

**Parâmetros**

- `tickers`: uma lista `string`, _case insensitive_ com os tickers das empresas desejadas separados por vírgulas.
  Exemplo: `PETR3,MGLU3,BBAS3`.

**Exemplo de chamada:**

```bash
curl '{URL_BASE}/b3/acoes/indicadores?tickers=PETR3,MGLU3'
```

**Resposta:**

```json
[
  {
    "valorDaFirma": 2.54413E10,
    "valorDeMercado": 2.05167E10,
    "setor": "Comercio",
    "subsetor": "Eletrodomesticos",
    "tipoDoAtivo": "ON NM",
    "dy": "0",
    "pl": "-342.98",
    "pvp": "1.88",
    "receitaLiquida12Meses": 3.53366E10,
    "dataUltimaCotacao": "2022-08-11T00:00:00Z",
    "ultimoBalancoProcessado": "2022-06-30T00:00:00Z",
    "liquidezCorrente": "1.64",
    "pebit": "73.05",
    "vpa": "1.62",
    "lpa": "-0.01",
    "roic": "0.011",
    "roe": "-0.005",
    "margemEbit": "0.008",
    "margemBruta": "0.254",
    "margemLiquida": "-0.002",
    "evEbitda": "20.34",
    "empresa": "MAGAZ LUIZA ON NM",
    "data": "2022-08-12T00:00:00Z",
    "ticker": "MGLU3"
  },
  {
    "valorDaFirma": 6.88583E11,
    "valorDeMercado": 5.08214E11,
    "setor": "Petroleo, Gas e Biocombustiveis",
    "subsetor": "Exploracao, Refino e Distribuicao",
    "tipoDoAtivo": "ON",
    "dy": "0.468",
    "pl": "3.15",
    "pvp": "1.24",
    "receitaLiquida12Meses": 5.68385E11,
    "dataUltimaCotacao": "2022-08-11T00:00:00Z",
    "ultimoBalancoProcessado": "2022-06-30T00:00:00Z",
    "liquidezCorrente": "1.31",
    "pebit": "1.97",
    "vpa": "31.47",
    "lpa": "12.38",
    "roic": "0.295",
    "roe": "0.393",
    "margemEbit": "0.455",
    "margemBruta": "0.509",
    "margemLiquida": "0.285",
    "evEbitda": "2.07",
    "empresa": "PETROBRAS ON",
    "data": "2022-08-12T00:00:00Z",
    "ticker": "PETR3"
  }
]
```


## Proventos

http://fintz.herokuapp.com/api/b3/proventos?ticker=PETR3&size=1000

**Parâmetros**

- `ticker`: um `string`, _case insensitive_ com o ticker do ativo desejada.
  Exemplo: `PETR4`.
- `size`: quantidade de itens (por página) na resposta
- `page`: página da resposta
- `sort`: usado para ordenar a resposta, podendo escolher o atributo e se é decrescente (desc) ou ascendente (asc)
  Exemplo: `sort=dataCom,desc`

**Estrutura de chamada**

```bash
curl '{URL_BASE}/proventos?ticker=PETR3&size=3'
```

**Exemplo de chamada**

```bash
curl 'https://fintz.herokuapp.com/api/b3/proventos?ticker=PETR3&size=3&sort=dataCom,desc'
```

**Resposta:**

```json
[
  {
    "nomeEmpresa": "PETROBRAS",
    "valor": "3.366002",
    "dataCom": "2022-08-11",
    "dataPagamento": "2022-08-31",
    "tipo": "Dividendo",
    "categoria": "acao",
    "ticker": "PETR3"
  },
  {
    "nomeEmpresa": "PETROBRAS",
    "valor": "3.366001",
    "dataCom": "2022-08-11",
    "dataPagamento": "2022-09-20",
    "tipo": "Dividendo",
    "categoria": "acao",
    "ticker": "PETR3"
  },
  {
    "nomeEmpresa": "PETROBRAS",
    "valor": "1.42756",
    "dataCom": "2022-05-23",
    "dataPagamento": "2022-06-20",
    "tipo": "Dividendo",
    "categoria": "acao",
    "ticker": "PETR3"
  }
]
```

## Eventos corporativos

Esse endpoint retorna os seguintes tipos de eventos corporativos:
- desdobramentos
- agrupamentos
- bonificações

Suporta qualquer ativo da Bolsa B3 (ações, BDRs, FIIs, e ETFs).

**Parâmetros**

- `ticker` (obrigatório): um `string`, _case insensitive_ com o ticker do ativo desejada.
  Exemplo: `PETR3` ou `PETR4`.
- `tipo`: um `string`, _case insensitive_ que pode ser um dos seguintes valores 'desdobramento' ou 'grupamento' ou 'bonificacao'
- `dataComStart`: um `string` de data no padrão 'AAAA-MM-DD', significando que você vai receber os eventos que ocorreram após essa data.
  Exemplo: `2022-01-01`.
- `dataComEnd`: um `string` de data no padrão 'AAAA-MM-DD', significando que você vai receber os eventos que ocorreram anteriormente à essa data.
  Exemplo: `2022-06-30`.
- `size`: quantidade máxima de itens retornados na chamada
- `sort`: usado para ordenar a resposta por algum atributo
  Exemplo: 'dataCom,desc', que retorna em ordem decrescente de acontecimento (os eventos mais recentes)

**Estrutura de chamada**

```bash
curl '{BASE}/api/b3/eventos?ticker={ticker}&tipo={tipo}'
```

**Exemplo de chamada**

```bash
curl 'https://fintz.herokuapp.com/api/b3/eventos?ticker=AMZO34&dataComStart=2022-04-01&dataComEnd=2022-05-30'
```

**Resposta do exemplo:**

```json
[
  {
    "isin": "BRAMZOBDR002",
    "fator": 20.0,
    "dataAnuncio": "2022-05-25",
    "ativoEmitido": "BRAMZOBDR002",
    "tipo": "DESDOBRAMENTO",
    "dataCom": "2022-05-25",
    "ticker": "AMZO34"
  }
]
```

Neste exemplo, observa-se que o ativo AMZO34 (BDR da Amazon) foi desdobrado em proporção 1:20 no dia 25 de Maio de 2.022. Isso significa que quem tinha X ativos AMZO34 na carteira no dia anterior, passou a ter 20X no dia 25 (e que, portanto, o preço do ativo também foi ajustado).


## Logos e ícones

Retorna a URL da logo de um ativo listado na bolsa pelo ticker.

Suporta ações, BDRs, FIIs, e ETFs.

Nesse endpoint, a URL_BASE não é utilizada, a base deve ser:
> `BASE` = `https://raw.githubusercontent.com/thecartera/B3-Assets-Images/main`

**Parâmetros**

- `ticker`: um `string`, _case insensitive_ com o ticker do ativo desejada.
  Exemplo: `PETR3` ou `PETR4`.

**Estrutura de chamada**

```bash
curl '{BASE}/imgs/{{ticker}}/logo'
```

**Exemplo de chamada**

```bash
curl 'https://raw.githubusercontent.com/thecartera/B3-Assets-Images/main/imgs/TSLA34.png'
```

**Resposta do exemplo:**

![BDR da Tesla, TSLA34](https://raw.githubusercontent.com/thecartera/B3-Assets-Images/main/imgs/TSLA34.png)
