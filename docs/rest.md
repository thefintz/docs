# Endpoints

Todos os endpoints tem a URL_BASE = "https://fintz.herokuapp.com/api"

## Empresas

Permite o usuário consultar dados de todas empresas brasileiras
cadastradas na receita federal através do CNPJ. Os dados são atualizados mensalmente

### `GET /empresas`

Retorna uma lista de empresas e seus estabelecimentos filtrados por parâmetros

**Query Params:**

- `cnae`: um `string`, filtra empresas que o estabelecimento matriz contém o [CNAE][1] específicado entre o cnae principal
e os secundários.
- `listadaB3`: um `boolean`, filtra empresas listadas ou não na B3 

**Exemplo:**

```bash
$ http GET '{URL_BASE}/empresas?listadaB3=true&cnae=1033301'
[
  {
    "estabelecimentos": [...],
    "listadaB3": true,
    "natureza": {
      "codigo": "2046",
      "descricao": "Sociedade Anônima Aberta"
    },
    "qualificacao": {	
      "codigo": "10",
      "descricao": "Diretor"
    },
    "porte": {	
      "codigo": "05",
      "descricao": "DEMAIS"
    },
    "capitalSocial": 14874743000,
    "nomeEmpresarial": "AMERICANAS S.A.",
    "cnpjBasico": "00776574"
  },
  {...}
]
```
  
### `GET /empresas/{cnpj}`

Retorna os dados da empresa com o CNPJ, além dos dados do estabelecimento matriz e das filiais.

**URL Params:**

- `cnpj`: um `string` contendo os 14 dígitos ou apenas os 8 primeiros dígitos, sem pontuação, do CNPJ da empresa.

**Exemplo:**

```bash
$ http GET '{URL_BASE}/empresas/44174296'
{
  "estabelecimentos": [
    {
      "identificadorMatrizFilial": {
        "codigo": "1",
        "descricao": "MATRIZ"
      },
      "situacaoCadastral": {
        "codigo": "02",
        "descricao": "ATIVA"
      },
      "nomeFantasia": "CARTERA",
      "dataSituacaoCadastral": "2020-11-01T00:00:00Z",
      "motivoSituacaoCadastral": {
        "codigo": "00",
        "descricao": "SEM MOTIVO"
      },
      "nomeCidadeExterior": null,
      "dataInicioAtividade": "2020-11-01T00:00:00Z",
      "situacaoEspecial": null,
      "dataSituacaoEspecial": null,
      "pais": null,
      "cnaesSecundarios": [
        "6201501",
        "6201502",
        "6202300",
        "6204000",
        "6209100",
        "8599603"
      ],
      "endereco": {...},
      "contato": {...},
      "cnaePrincipal": "6203100",
      "cnpj": "44174296000132"
    }
  ],
  "listadaB3": false,
  "natureza": {
    "codigo": "2062",
    "descricao": "Sociedade Empresária Limitada"
  },
  "qualificacao": {
    "codigo": "49",
    "descricao": "Sócio-Administrador"
  },
  "porte": {
    "codigo": "01",
    "descricao": "MICRO EMPRESA"
  },
  "capitalSocial": 100000,
  "nomeEmpresarial": "CARTERA SOFTWARE LTDA",
  "cnpjBasico": "44174296"
}
```

### GET /b3/acoes

Retorna uma lista de empresas negociadas na bolsa e informações gerais

**Query Params:**

- `cnpj`: um `string` de 14 dígitos ou apenas os 8 primeiros dígitos de um CNPJ, filtra ações da B3 por CNPJ da empresa.

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
    "ultimaData": "2022-01-26T23:31:05Z",
    "temEmissões": false,
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
### `GET /b3/acoes/{ticker}/fundamentos`

Retorna os fundamentos e indicadores de uma empresa listada na bolsa pelo ticker.

**URL params:**

- `ticker`: um `string`, _case insensitive_ com o ticker da empresa desejada.
Exemplo: `PETR3` ou `PETR4`.

**Exemplo:**

```bash
$ http GET '{URL_BASE}/b3/acoes/PETR3/fundamentos'
{
  "data": "2022-01-19T00:00:00Z",
  "papel": "PETR3",
  "empresa": "PETROBRAS ON",
  "setor": "Petroleo, Gas e Biocombustiveis",
  "tipo": "ON",
  "subsetor": "Exploracao, Refino e Distribuicao",
  "valorDaFirma": 708584000000,
  "valorDeMercado": 446774000000,
  "ultBalancoProcessado": "2021-09-30T00:00:00Z",
  "divYield": 0.165,
  "vpa": 28.29,
  "lpa": 10.35,
  "roic": 0.196,
  "roe": 0.366,
  "liquidezCorr": 1.2,
  "margEbit": 0.44,
  "margBruta": 0.511,
  "margLiquida": 0.346,
  "evEbitda": 2.98,
  "receitaLiquida12Meses": 393450000000,
  "pl": 3.31,
  "pvp": 1.21,
  "pebit": 2.58
}
```

[1]: https://cnae.ibge.gov.br/
