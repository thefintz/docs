# Endpoints

Esta página irá listar os endpoints existentes em nossos serviços.

## Empresas

Permite o usuário consultar dados de CNPJs de todas empresas brasileiras
cadastradas na receita federal. Os dados são atualizados mensalmente

### `GET /empresas/{cnpj}`

Retorna, de foma paginada, todas as empresas.

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

### `GET /empresas/{cnpj}/socios`

Retorna, de forma paginada, todos os sócios da empresa.

**Exemplo:**

```bash
$ http GET /empresas/09346601/socios
{
    "cnpj_basico": "09346601",
    "identificador_de_socio": "2",
    "nome_do_socio": "DANIEL SONDER",
    "cnpj_cpf_do_socio": "***092178**",
    "qualificacao_do_socio": "10",
    "data_de_entrada_sociedade": "20130821",
    "pais": null,
    "representante_legal": "***000000**",
    "nome_do_representante": "",
    "qualificacao_do_representante": "0",
    "faixa_etaria": "5"
}
```
