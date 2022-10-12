[CNAE]: https://cnae.ibge.gov.br/
[CNAE_ESTRUTURA]: https://cnae.ibge.gov.br/?view=estrutura


# Empresas

Todos os endpoints desta página tem a seguinte url base:
> `URL_BASE` = `https://fintz.herokuapp.com/api`

## Empresas

Permite o usuário consultar dados de todas empresas brasileiras
cadastradas na receita federal através do CNPJ. Os dados são atualizados mensalmente.

### `GET /empresas`

Retorna uma lista de empresas, contendo informações comuns da empresa entre seus estabelecimentos (matriz e filiais), filtrados por parâmetros

**Parâmetros**

- `cnae`: um `string`, sem pontuação, que filtra empresas que o estabelecimento matriz contém o [CNAE][CNAE] específicado no cnae principal.
É possível também filtrar por toda a [estrutura][CNAE_ESTRUTURA] dos cnaes enviando apenas o início da `string`, exemplos:
    - `cnae=41`: busca pela divisão `41 - Construção de edificios`
    - `cnae=411`: busca pelo grupo `41.1 Incorporação de empreendimentos imobiliários`
    - `cnae=41107`: busca pela classe `41.10-7 Incorporação de empreendimentos imobiliários`
    - `cnae=4110700`: busca pela subclasse `4110-7/00 Incorporação de empreendimentos imobiliários`
- `cnaes`: uma lista de `string`, sem pontuação, com o comportamento similar ao `cnae`, porém busca as empresas que o estabelecimento matriz
contém qualquer um dos [CNAEs][1] específicados no cnae principal. Exemplo:
    - `cnaes=62,631`
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

## Estabelecimentos
### `GET /estabelecimentos`

Retorna uma lista de estabelecimentos, filtrados por parâmetros

**Parâmetros**

- `cnae`: um `string`, sem pontuação, que filtra estabelecimentos que contém o [CNAE][1] específicado no cnae principal.
É possível também filtrar por toda a [estrutura][2] dos cnaes enviando apenas o início da `string`, exemplos:
    - `cnae=41`: busca pela divisão `41 - Construção de edificios`
    - `cnae=411`: busca pelo grupo `41.1 Incorporação de empreendimentos imobiliários`
    - `cnae=41107`: busca pela classe `41.10-7 Incorporação de empreendimentos imobiliários`
    - `cnae=4110700`: busca pela subclasse `4110-7/00 Incorporação de empreendimentos imobiliários`
- `cnaes`: uma lista de `string`, sem pontuação, com comportamento similar ao `cnae`, porém busca os estabelecimentos
que contém qualquer um dos [CNAEs][1] específicados no cnae principal. Exemplo:
    - `cnaes=62,631`
- `negociadaB3`: um `boolean`, filtra estabelecimentos que a empresa é negociada na B3

**Exemplo:**

```bash
$ http GET '{URL_BASE}/estabelecimentos?negociadaB3=true&cnae=4711302'
[
  {
    "cnaesSecundarios": [
      "4619200",
      "8299702"
    ],
    "empresa": {
      "negociadaB3": true,
      "cnpjBasico": "06057223",
      "capitalSocial": 786730240,
      "nomeEmpresarial": "SENDAS DISTRIBUIDORA S/A",
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
      }
    },
    "identificadorMatrizFilial": {
      "codigo": "1",
      "descricao": "MATRIZ"
    },
    "nomeFantasia": "ASSAI ATACADISTA",
    "situacaoCadastral": {
      "codigo": "02",
      "descricao": "ATIVA"
    },
    "dataSituacaoCadastral": "2003-10-31T02:00:00Z",
    "motivoSituacaoCadastral": {
      "codigo": "00",
      "descricao": "SEM MOTIVO"
    },
    "nomeCidadeExterior": null,
    "pais": null,
    "dataInicioAtividade": "2003-12-01T02:00:00Z",
    "situacaoEspecial": null,
    "dataSituacaoEspecial": null,
    "cnpj": "06057223000171",
    "cnaePrincipal": {
      "codigo": "4711302",
      "descricao": "Comércio varejista de mercadorias em geral, com predominância de produtos alimentícios - supermercados"
    },
    "endereco": {
      "tipoDeLogradouro": "AVENIDA",
      "logradouro": "AYRTON SENNA",
      "numero": "06000",
      "complemento": "      LOT 2 PAL 48959           ANEXO A",
      "bairro": "JACAREPAGUA",
      "cep": "22775005",
      "uf": "RJ",
      "municipio": {
        "codigo": "6001",
        "descricao": "RIO DE JANEIRO"
      }
    },
    "contato": {
      "email": "PARALEGAL@ASSAI.COM.BR",
      "telefone1": "1134115000",
      "telefone2": null,
      "fax": "1138860599"
    }
  }
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
  "cnaesSecundarios": [
    "6201501"
  ],
  "empresa": {
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
    }
  },
  "identificadorMatrizFilial": {
    "codigo": "1",
    "descricao": "MATRIZ"
  },
  "nomeFantasia": "CARTERA",
  "situacaoCadastral": {
    "codigo": "02",
    "descricao": "ATIVA"
  },
  "dataSituacaoCadastral": "2020-11-01T03:00:00Z",
  "motivoSituacaoCadastral": {
    "codigo": "00",
    "descricao": "SEM MOTIVO"
  },
  "nomeCidadeExterior": null,
  "pais": null,
  "dataInicioAtividade": "2020-11-01T03:00:00Z",
  "situacaoEspecial": null,
  "dataSituacaoEspecial": null,
  "cnpj": "44174296000132",
  "cnaePrincipal": {
    "codigo": "6203100",
    "descricao": "Desenvolvimento e licenciamento de programas de computador não-customizáveis"
  },
  "endereco": {
    "tipoDeLogradouro": "RODOVIA",
    "logradouro": "",
    "numero": "",
    "complemento": "",
    "bairro": "ITACORUBI",
    "cep": "88034101",
    "uf": "SC",
    "municipio": {
      "codigo": "8105",
      "descricao": "FLORIANOPOLIS"
    }
  },
  "contato": {
    "email": "BUENO@CARTERA.COM.BR",
    "telefone1": "4191875540",
    "telefone2": null,
    "fax": null
  }
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

## Buscar ação na bolsa por CNPJ

Retorna o código de negociação da empresa (se negociada na bolsa) e informações gerais

**Parâmetros**

- `cnpj`: um `string` de 14 dígitos ou apenas os 8 primeiros dígitos de um CNPJ, filtra ações da B3 por CNPJ da empresa.
- `cnpjs`: uma lista de `string` de 14 dígitos ou apenas os 8 primeiros dígitos de CNPJs, separados por vírgulas.

**Exemplo de chamada:**

```bash
curl '{URL_BASE}/b3/acoes?cnpj=33000167'
```

**Resposta:**

```json
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