### Buscar ticker de empresa por CNPJ

Retorna os códigos de negociação de uma empresa por CNPJ

**Query Params:**

- `cnpj`: um `string` de 14 dígitos ou apenas os 8 primeiros dígitos de um CNPJ, filtra ações da B3 por CNPJ da empresa.
- `cnpjs`: uma lista de `string` de 14 dígitos ou apenas os 8 primeiros dígitos de CNPJs, separados por vírgulas.

**Exemplo:**

```bash
$ http GET '{URL_BASE}/b3/acoes?cnpj=33000167'
[
  {
    "codigoCVM": "9512",
    "empresaEmissora": "PETR",
    "nomeEmpresa": "PETROLEO BRASILEIRO S.A. PETROBRAS",
    "nomeNegociacao": "PETROBRAS",
    "cnpj": "33000167000101",
    "classificacaoIndustria": "Petróleo. Gás e Biocombustíveis / Petróleo. Gás e Biocombustíveis / Exploração. Refino e Distribuição",
    "classificacaoIndustriaEng": null,
    "atividade": "Pesquisa. lavra. refinação. processamento. comércio e transporte de petróleo. de seus derivados. de gás natural e de outros hidrocarbonetos fluidos. além das atividades vinculadas à energia.",
    "website": "www.petrobras.com.br",
    "temCotacao": null,
    "status": "A",
    "indicatorMercado": "17",
    "mercado": "BOVESPA NIVEL 2",
    "instituicaoComum": "BRADESCO",
    "instituicaoPreferencial": "BRADESCO",
    "codigo": "PETR3",
    "ultimaData": "2022-02-01T02:30:05Z",
    "temEmissoes": false,
    "temBdr": false,
    "tipoBdr": null,
    "categoriaDescritivelBVMF": null,
    "outrosCodigos": [
      {
        "isin": "BRPETRACNOR9",
        "code": "PETR3",
        "codeCvm": "9512"
      },
      {
        "isin": "BRPETRACNPR6",
        "code": "PETR4",
        "codeCvm": "9512"
      },
      {
        "isin": "BRPETRDBS001",
        "code": "PETR-DEB61",
        "codeCvm": "9512"
      },
      {
        "isin": "BRPETRDBS092",
        "code": "PETR-DEB62",
        "codeCvm": "9512"
      }
    ]
  }
]
```

### Buscar indicadores por ticker

Retorna os indicadores fundamentalistas de uma empresa listada na bolsa pelo ticker.

**URL Params:**

- `ticker`: um `string`, _case insensitive_ com o ticker da empresa desejada.
Exemplo: `PETR3` ou `PETR4`.

**Exemplo:**

```bash
$ http GET '{URL_BASE}/b3/acoes/PETR3/indicadores'
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

### Buscar indicadores por lista de tickers

Retorna uma lista de indicadores de empresas listadas na bolsa, filtradas por paramêtros.

**Query Params:**

- `tickers`: uma lista `string`, _case insensitive_ com os tickers das empresas desejadas separados por vírgulas.
  Exemplo: `PETR3,MGLU3,BBAS3`.

**Exemplo:**

```bash
$ http GET '{URL_BASE}/b3/acoes/indicadores?tickers=PETR3,MGLU3'
[
    {
        "empresa": "MAGAZ LUIZA ON NM",
        "ticker": "MGLU3",
        "valorDaFirma": 4.68083E10,
        "valorDeMercado": 4.4138E10,
        "receitaLiquida12Meses": 3.52782E10,
        "setor": "Comercio",
        "subsetor": "Eletrodomesticos",
        "tipoDoAtivo": "ON NM",
        "dataUltimaCotacao": "2022-03-25T03:00:00Z",
        "ultimoBalancoProcessado": "2021-12-31T03:00:00Z",
        "dy": "0.002",
        "pl": "74.73",
        "pvp": "3.92",
        "pebit": "167.34",
        "vpa": "1.67",
        "lpa": "0.09",
        "roic": "0.011",
        "roe": "0.052",
        "liquidezCorrente": "1.61",
        "margemEbit": "0.007",
        "margemBruta": "0.241",
        "margemLiquida": "0.017",
        "evEbitda": "43.31",
        "data": "2022-03-25T03:00:00Z"
    }, {...}
]
```

### Buscar ícone por ticker

Retorna uma url do ícone (sempre 120x120 pixels) de uma empresa listada na bolsa pelo ticker.

**URL params:**

- `ticker`: um `string`, _case insensitive_ com o ticker da empresa desejada.
  Exemplo: `PETR3` ou `PETR4`.

**Exemplo:**

```bash
$ http GET '{URL_BASE}/b3/acoes/PETR3/logo'
{
  "url": "https://raw.githubusercontent.com/thecartera/B3-Assets-Images/main/imgs/PETR3.png"
}
```
