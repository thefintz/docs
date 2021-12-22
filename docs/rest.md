# Endpoints

Esta página irá listar os endpoints existentes em nossos serviços.

## Empresas

Permite o usuário consultar dados de CNPJs de todas empresas brasileiras
cadastradas na receita federal. Os dados são atualizados mensalmente

### `GET /empresas/{cnpj}`

Retorna os dados da empresa com o CNPJ.

**URL Params:**

- `cnpj`: um `string` contendo os 8 primeiros dígitos do CNPJ da empresa.

**Exemplo:**

```bash
$ http GET '/empresas/00000000'
{
    "cnpj_basico": "00000000",
    "nome_empresarial": "BANCO DO BRASIL SA",
    "natureza_juridica": "2038",
    "qualificacao_do_responsavel": "10",
    "capital_social_da_empresa": "90000000000,00",
    "porte_da_empresa": "5.0",
    "ente_federativo_responsavel": null
}
```

### `GET /b3/{ticker}`

Retorna os dados de uma empresa listada na bolsa.

**URL params:**

- `ticker`: um `string`, _case insensitive_ com o ticker da empresa desejada.
Exemplo: `PETR3` ou `PETR4`.

**Exemplo:**

```bash
$ http GET '/b3/PETR4'
{
    # TODO
}
```

### `GET /b3?cnae={cnae}`

Retorna lista de empresas listadas na bolsa que possuem o determinado [CNAE][1].

**Query params:**

- `cnae`: um `string` de dígitos contendo o código CNAE para ser pesquisado.

**Exemplo:**

```bash
$ http GET '/b3?cnae=0111301'
{
    # TODO
}
```

[1]: https://cnae.ibge.gov.br/
