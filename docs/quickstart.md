# Primeiros passos

Para usar a API Fintz, você precisa se autenticar através de um token de acesso. Porém, antes de nos contactar para recebê-lo, você pode comprovar rapidamente a funcionalidade da nossa API, pois liberamos aqui dois endpoints de testes que podem ser chamados sem autenticação. Fique a vontade para testá-los. 

Depois, pode nos contactar através [desse link][contatoFintz]

[contatoFintz]: https://fintz.com.br/#/contato

## Caso de uso: página de indicadores de ação

Digamos que você queira construir uma página no seu site ou app com indicadores fundamentalistas e financeiros de papeis da bolsa, como FIIs, ETFs, ações ou BDRs.

Você pode fazer isso tranquilamente em apenas 1 passo utilizando a API Fintz com a seguinte chamada:

```GET https://fintz.herokuapp.com/api/b3/acoes/indicadores?tickers=PETR3```

Essa chamada vai retornar o seguinte json:

```json
[
    {
        "ticker": "PETR3",
        "empresa": "PETROBRAS ON",
        "valorDaFirma": 722335000000,
        "valorDeMercado": 456557000000,
        "setor": "Petroleo, Gas e Biocombustiveis",
        "subsetor": "Exploracao, Refino e Distribuicao",
        "tipoDoAtivo": "ON",
        "dy": "0.161",
        "pl": "4.28",
        "pvp": "1.18",
        "pebit": "2.4",
        "vpa": "29.69",
        "lpa": "8.18",
        "roic": "0.216",
        "roe": "0.275",
        "margemEbit": "0.421",
        "margemBruta": "0.485",
        "margemLiquida": "0.237",
        "dataUltimaCotacao": "2022-03-25T00:00:00Z",
        "ultimoBalancoProcessado": "2021-12-31T00:00:00Z",
        "liquidezCorrente": "1.25",
        "evEbitda": "2.78",
        "receitaLiquida12Meses": 452668000000,
        "data": "2022-03-25T00:00:00Z"
    }
]
```

## Caso de uso: Buscar dados de CNPJ

Digamos que você precise de informações gerais acerca de uma empresa. Você pode conseguir facilmente através do CNPJ da empresa que lhe interessa.

```GET https://fintz.herokuapp.com/api/estabelecimentos/33000167066129`

```json
{
    "nomeFantasia": "PETROBRAS",
    "cnpj": "33000167066129",
    "empresa": {
        "negociadaB3": true,
        "cnpjBasico": "33000167",
        "naturezaJuridica": {
            "codigo": "2038",
            "descricao": "Sociedade de Economia Mista"
        },
        "qualificacaoResponsavel": {
            "codigo": "10",
            "descricao": "Diretor"
        },
        "capitalSocial": 205431960000,
        "nomeEmpresarial": "PETROLEO BRASILEIRO S A PETROBRAS",
        "porte": {
            "codigo": "05",
            "descricao": "DEMAIS"
        }
    },
    "cnaePrincipal": {
        "codigo": "4681801",
        "descricao": "Comércio atacadista de álcool carburante, biodiesel, gasolina e demais derivados de petróleo, exceto lubrificantes, não realizado por transportador re"
    },
    "cnaesSecundarios": [],
    "endereco": {
        "tipoDeLogradouro": "AVENIDA",
        "logradouro": "GUARDA MOR LOBO VIANA",
        "numero": "1111",
        "complemento": null,
        "bairro": null,
        "cep": "11600200",
        "uf": "SP",
        "municipio": {
            "codigo": "7115",
            "descricao": "SAO SEBASTIAO"
        }
    },
    "contato": {
        "email": "atendimentofiscossco@petrobras.com.br",
        "telefone1": "2132243025",
        "telefone2": "2132243022"
    },
    "identificadorMatrizFilial": {
        "codigo": "2",
        "descricao": "FILIAL"
    },
    "situacaoCadastral": {
        "codigo": "02",
        "descricao": "ATIVA"
    },
    "dataSituacaoCadastral": "2004-11-01T00:00:00Z",
    "motivoSituacaoCadastral": {
        "codigo": "00",
        "descricao": "SEM MOTIVO"
    },
    "dataInicioAtividade": "1968-10-31T00:00:00Z",
    "nomeCidadeExterior": null,
    "situacaoEspecial": null,
    "dataSituacaoEspecial": null,
    "pais": null
}
```

