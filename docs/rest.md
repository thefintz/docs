# Endpoints

Todos os endpoints tem a URL_BASE = "https://fintz.herokuapp.com/api"

## Empresas e estabelecimentos

Permite o usuário consultar dados de todas empresas brasileiras
cadastradas na receita federal através do CNPJ. Os dados são atualizados mensalmente.

### `GET /empresas`

Retorna uma lista de empresas, contendo informações comuns da empresa entre seus estabelecimentos (matriz e filiais), filtrados por parâmetros

**Query Params:**

- `cnae`: um `string`, filtra empresas que o estabelecimento matriz contém o [CNAE][1] específicado entre o cnae principal
e os secundários. É possível também filtrar por toda a [estrutura][2] dos cnaes enviando apenas o início da `string`, exemplos:
  - `cnae=41`: busca pela divisão `41 - Construção de edificios`
  - `cnae=411`: busca pelo grupo `41.1 Incorporação de empreendimentos imobiliários`
  - `cnae=41107`: busca pela classe `41.10-7 Incorporação de empreendimentos imobiliários`
  - `cnae=4110700`: busca pela subclasse `4110-7/00 Incorporação de empreendimentos imobiliários`
- `negociadaB3`: um `boolean`, filtra por empresas negociadas na B3

**Exemplo:**

```bash
$ http GET '{URL_BASE}/empresas?negociadaB3=true&cnae=4711302'
[
  {
    "negociadaB3": true,
    "cnpjBasico": "47960950",
    "capitalSocial": 12552162000,
    "nomeEmpresarial": "MAGAZINE LUIZA S/A",
    "naturezaJuridica": {
      "codigo": "2046",
      "descricao": "Sociedade Anônima Aberta"
    },
    "qualificacaoResponsavel": {
      "codigo": "10",
      "descricao": "Diretor"
    },
    "porte": {
      "codigo": "05",
      "descricao": "DEMAIS"
    },
    "cnpjsEstabelecimentos": [
      "47960950056500",
      ...
      "47960950052601"
    ]
  },
  {...}
]
```
  
### `GET /empresas/{cnpj}`

Retorna os dados da empresa comuns entre todos os estabelecimentos,
além de uma lista com todos os CNPJs dos estabelecimentos.

**URL Params:**

- `cnpj`: um `string` contendo os 14 dígitos ou apenas os 8 primeiros dígitos, sem pontuação, do CNPJ da empresa.

**Exemplo:**

```bash
$ http GET '{URL_BASE}/empresas/44174296'
{
  "negociadaB3": false,
  "cnpjBasico": "44174296",
  "capitalSocial": 100000,
  "nomeEmpresarial": "CARTERA SOFTWARE LTDA",
  "naturezaJuridica": {
    "codigo": "2062",
    "descricao": "Sociedade Empresária Limitada"
  },
  "qualificacaoResponsavel": {
    "codigo": "49",
    "descricao": "Sócio-Administrador"
  },
  "porte": {
    "codigo": "01",
    "descricao": "MICRO EMPRESA"
  },
  "cnpjsEstabelecimentos": [
    "44174296000132"
  ]
}
```

### `GET /estabelecimentos`

Retorna uma lista de estabelecimentos, filtrados por parâmetros

**Query Params:**

- `cnae`: um `string`, filtra estabelecimentos que contém o [CNAE][1] específicado entre o cnae principal
  e os secundários. É possível também filtrar por toda a [estrutura][2] dos cnaes enviando apenas o início da `string`, exemplos:
  - `cnae=41`: busca pela divisão `41 - Construção de edificios`
  - `cnae=411`: busca pelo grupo `41.1 Incorporação de empreendimentos imobiliários`
  - `cnae=41107`: busca pela classe `41.10-7 Incorporação de empreendimentos imobiliários`
  - `cnae=4110700`: busca pela subclasse `4110-7/00 Incorporação de empreendimentos imobiliários`
- `negociadaB3`: um `boolean`, filtra estabelecimentos que a empresa é negociada na B3

**Exemplo:**

```bash
$ http GET '{URL_BASE}/estabelecimentos?negociadaB3=true&cnae=4711302'
[
  {
    "cnpj": "47508411000156",
    "cnaesSecundarios": [
      "4711302",
      ...
    ],
    "empresa": {
      "negociadaB3": true,
      ...
    },
    "identificadorMatrizFilial": {
      "codigo": "1",
      "descricao": "MATRIZ"
    },
    "nomeFantasia": null,
    "situacaoCadastral": {
      "codigo": "02",
      "descricao": "ATIVA"
    },
    "dataSituacaoCadastral": "2004-11-01T03:00:00Z",
    "motivoSituacaoCadastral": {
      "codigo": "00",
      "descricao": "SEM MOTIVO"
    },
    "nomeCidadeExterior": null,
    "pais": null,
    "dataInicioAtividade": "1980-11-01T03:00:00Z",
    "situacaoEspecial": null,
    "dataSituacaoEspecial": null,
    "cnaePrincipal": {
      "codigo": "4789099",
      "descricao": "Comércio varejista de outros produtos não especificados anteriormente"
    },
    "endereco": {...},
    "contato": {...}
  },
  {...}
]
```

### `GET /estabelecimentos/{cnpj}`

Retorna os dados de um estabelecimento, como dados de endereço, contato, CNAEs, situação cadastral, entre outros

**URL Params:**

- `cnpj`: um `string` contendo os 14 dígitos, sem pontuação, do CNPJ do estabelecimento.

**Exemplo:**

```bash
$ http GET '{URL_BASE}/estabelecimentos/44174296000132'
{
  "cnpj": "44174296000132",
  "nomeFantasia": "CARTERA",
  "cnaePrincipal": {
    "codigo": "6203100",
    "descricao": "Desenvolvimento e licenciamento de programas de computador não-customizáveis"
  },
  "cnaesSecundarios": [
    "6201501",
    "6201502",
    "6202300",
    "6204000",
    "6209100",
    "8599603"
  ],
  "empresa": {
    "negociadaB3": false,
    "naturezaJuridica": {...},
    "qualificacaoResponsavel": {...},
    "cnpjBasico": "44174296",
    "capitalSocial": 100000,
    "nomeEmpresarial": "CARTERA SOFTWARE LTDA",
    "porte": {...},
    "cnpjsEstabelecimentos": [...]
  },
  "identificadorMatrizFilial": {
    "codigo": "1",
    "descricao": "MATRIZ"
  },
  "situacaoCadastral": {
    "codigo": "02",
    "descricao": "ATIVA"
  },
  "motivoSituacaoCadastral": {
    "codigo": "00",
    "descricao": "SEM MOTIVO"
  },
  "dataSituacaoCadastral": "2020-11-01T03:00:00Z",
  "nomeCidadeExterior": null,
  "pais": null,
  "dataInicioAtividade": "2020-11-01T03:00:00Z",
  "situacaoEspecial": null,
  "dataSituacaoEspecial": null,
  "endereco": {...},
  "contato": {...}
}
```

### `GET /estabelecimentos/{cnpj}/cnaes`

Retorna detalhes dos cnaes principal e secundários de um estabelecimento, como subclasse, classe, grupo,
divisão e seção, além de observações.

**URL Params:**

- `cnpj`: um `string` contendo os 14 dígitos, sem pontuação, do CNPJ do estabelecimento.

**Exemplo:**

```bash
$ http GET '{URL_BASE}/estabelecimentos/44174296000132/cnaes'
{
  "cnaePrincipal": {
    "subclasseId": "6203100",
    "subclasseDescricao": "DESENVOLVIMENTO E LICENCIAMENTO DE PROGRAMAS DE COMPUTADOR NÃO-CUSTOMIZÁVEIS",
    "classeId": "62031",
    "classeDescricao": "DESENVOLVIMENTO E LICENCIAMENTO DE PROGRAMAS DE COMPUTADOR NÃO-CUSTOMIZÁVEIS",
    "classeObservacoes": "Esta classe compreende - o desenvolvimento de sistemas ou programas de computador...",
    "grupoId": "620",
    "grupoDescricao": "ATIVIDADES DOS SERVIÇOS DE TECNOLOGIA DA INFORMAÇÃO",
    "divisaoId": "62",
    "divisaoDescricao": "ATIVIDADES DOS SERVIÇOS DE TECNOLOGIA DA INFORMAÇÃO",
    "secaoId": "J",
    "secaoDescricao": "INFORMAÇÃO E COMUNICAÇÃO"
  },
  "cnaesSecundarios": [
    {
      "subclasseId": "6201502",
      "subclasseDescricao": "WEB DESIGN",
      "classeId": "62015",
      "classeDescricao": "DESENVOLVIMENTO DE PROGRAMAS DE COMPUTADOR SOB ENCOMENDA",
      "classeObservacoes": "Esta classe compreende - o desenvolvimento de sistemas para atender às...",
      "grupoId": "620",
      "grupoDescricao": "ATIVIDADES DOS SERVIÇOS DE TECNOLOGIA DA INFORMAÇÃO",
      "divisaoId": "62",
      "divisaoDescricao": "ATIVIDADES DOS SERVIÇOS DE TECNOLOGIA DA INFORMAÇÃO",
      "secaoId": "J",
      "secaoDescricao": "INFORMAÇÃO E COMUNICAÇÃO"
    },
    {...}
  ]
}
```

## B3

### `GET /b3/acoes`

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

### `GET /b3/acoes/{ticker}/indicadores`

Retorna os indicadores fundamentalistas de uma empresa listada na bolsa pelo ticker.

**URL params:**

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

### `GET /b3/acoes/{ticker}/logo`

Retorna uma url da logo de uma empresa listada na bolsa pelo ticker.

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

[1]: https://cnae.ibge.gov.br/
[2]: https://cnae.ibge.gov.br/?view=estrutura
