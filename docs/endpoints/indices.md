[contato]: https://fintz.com.br/#/contato

# Índices, taxas e câmbio

Os índices disponíveis são
```
Índice  | Histórico | Composição
--------------------------------
AGFS    |     ✓     |      ✓
BDRX    |     ✓     |      ✓
GPTW    |     ✓     |      ✓
IBOV    |     ✓     |      ✓
IBRA    |     ✓     |      ✓
IBSD    |     ✓     |      ✓
IBXL    |     ✓     |      ✓
IBXX    |     ✓     |      ✓
ICO2    |     ✓     |      ✓
ICON    |     ✓     |      ✓
IDIV    |     ✓     |      ✓
IDVR    |     ✓     |      ✓
IEEX    |     ✓     |      ✓
IFIL    |     ✓     |      ✓
IFIX    |     ✓     |      ✓
IFNC    |     ✓     |      ✓
IGCT    |     ✓     |      ✓
IGCX    |     ✓     |      ✓
IGNM    |     ✓     |      ✓
IMAT    |     ✓     |      ✓
IMOB    |     ✓     |      ✓
INDX    |     ✓     |      ✓
ISEE    |     ✓     |      ✓
ITAG    |     ✓     |      ✓
IVBX    |     ✓     |      ✓
MLCX    |     ✓     |      ✓
SMLL    |     ✓     |      ✓
UTIL    |     ✓     |      ✓ 
```

Precisa de algum outro índice? [Entre em contato][contato].

Obs: dados disponíveis desde 2000-01-01.

## Índices

### Histórico
**/indices/historico**

Retorna o histórico referente ao índice requisitado.
Obs: dados disponíveis desde 2000-01-01.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `indice`     | `string` | ex: "IBOV" | obrigatório
| `dataInicio` | `string` | (yyyy-mm-dd) | obrigatório
| `dataFim`    | `string` | (yyyy-mm-dd) | opcional
| `ordem`      | `string` | "ASC" ou "DESC" | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }
PARAMS = { 'indice': 'IBOV', 'dataInicio': '2023-01-01' }

res = req.get(f'{URL_BASE}/indices/historico', headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
    {
        "indice": "IBOV",
        "data": "2023-01-02",
        "valor": 106376.0234375
    },
    {
        "indice": "IBOV",
        "data": "2023-01-03",
        "valor": 104165.7421875
    },
    ...
]
```

### Composição
**/indices/composicao**

Retorna a composição atual da carteira referente ao índice requisitado.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `indice`     | `string` | ex: "IBOV" | obrigatório
| `ordem`      | `string` | "ASC" ou "DESC" - Ordena por participação | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }
PARAMS = { 'indice': 'IBOV'}

res = req.get(f'{URL_BASE}/indices/composicao', headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "indice": "IBOV",
    "ticker": "VALE3",
    "participacao": 0.12618,
    "quantidadeTeorica": 4196924316,
    "data": "2024-04-22"
  },
  {
    "indice": "IBOV",
    "ticker": "PETR4",
    "participacao": 0.08782,
    "quantidadeTeorica": 4566445852,
    "data": "2024-04-22"
  },
]
```


## Taxas

As taxas atualmente disponíveis são
```
Código | Taxa
12     | CDI
4391   | CDI acumulada no mês
4392   | CDI acumulada no mês anualizada base 252
4389   | CDI anualizada base 252
27803  | Fator diário Taxa Extramercado
29251  | FII para TCR e TRFC
29252  | FII para TFC
11     | Selic
4390   | Selic acumulada no mês
4189   | Selic acumulada no mês anualizada base 252
1178   | Selic anualizada base 252
254    | Taxa básica financeira pro-rata (TBF pro-rata)
253    | Taxa básica financeira (TBF)
7813   | Taxa básica financeira (TBF) - Primeiro dia do mês
7814   | Taxa básica financeira (TBF) - Primeiro dia do mês anualizada na base 252
256    | Taxa de juros de longo prazo - TJLP
27804  | Taxa Extramercado
27572  | Taxa Jm para TLP
25624  | Taxa referencial do Tesouro - Taxa anual
25623  | Taxa referencial do Tesouro - Taxa diária
227    | Taxa referencial pro-rata (TR pro-rata)
226    | Taxa referencial (TR)
13421  | Taxa referencial (TR) para financiamentos imobiliários prefixados do SFH
7811   | Taxa referencial (TR) - Primeiro dia do mês
7812   | Taxa referencial (TR) - Primeiro dia do mês anualizada base 252
7815   | TJLP mensal
22161  | TRT - Fator diário
```

### Busca

**/taxas/busca**

Retorna todas as taxas que podem ser buscadas. 

Importante pois você vai utilizar o `"codigo"` retornado para buscar o histórico da taxa.

Pode-se utilizar filtro.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `q`     | `string` | ex: "cdi" | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }
PARAMS = { 'q': 'cdi' }

res = req.get(f'{URL_BASE}/taxas/busca', headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "nome": "CDI",
    "codigo": 12,
    "unidade": "% a.d.",
    "descricao": "Taxa média dos empréstimos interbancários com um dia de prazo, comumente usada como referência para investimentos de renda fixa."
  },
  {
    "nome": "CDI acumulada no mês",
    "codigo": 4391,
    "unidade": "% a.m.",
    "descricao": "A taxa CDI acumulada no período mensal."
  },
  {
    "nome": "CDI acumulada no mês anualizada base 252",
    "codigo": 4392,
    "unidade": "% a.a.",
    "descricao": "A taxa CDI mensal, anualizada com base em 252 dias úteis."
  },
  {
    "nome": "CDI anualizada base 252",
    "codigo": 4389,
    "unidade": "% a.a.",
    "descricao": "Taxa CDI anualizada levando em consideração 252 dias úteis."
  }
]
```


### Histórico

**/taxas/historico**

Retorna todas as taxas que podem ser buscadas. 
Pode-se utilizar filtro.

Os codigos das taxas estão disponíveis no endpoint de busca (/taxas/busca) e também listados um pouco abaixo.

Obs: dados disponíveis desde 2000-01-01.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `codigo`     | `string` | ex: "12" (para CDI) | obrigatório
| `dataInicio` | Date | ex: "2023-01-01" | obrigatório
| `dataFim`    | Date | ex: "2023-05-01" | opcional
| `ordem`      | "ASC" ou "DESC" | ex: "ASC" | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }
PARAMS = { 'codigo': '12', 'dataInicio': '2023-01-01' }

res = req.get(f'{URL_BASE}/taxas/historico', headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
  {
    "nome": "CDI",
    "data": "2023-01-02",
    "valor": 0.050788,
    "dataFim": null
  },
  {
    "nome": "CDI",
    "data": "2023-01-03",
    "valor": 0.050788,
    "dataFim": null
  },
  {
    "nome": "CDI",
    "data": "2023-01-04",
    "valor": 0.050788,
    "dataFim": null
  },
  ...
]
```

## Câmbio (PTAX)

### busca

**/cambio/ptax/busca**

Retorna a lista de PTAX que podem ser buscadas. 

Importante pois você vai utilizar o `"codigo"` retornado para buscar o histórico da taxa.

Pode-se utilizar filtro.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `q`     | `string` | ex: "dólar" | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }
PARAMS = { 'q': 'dólar' }

res = req.get(f'{URL_BASE}/cambio/ptax/busca', headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
    {
        "nome": "Dólar australiano",
        "codigo": "AUD",
        "tipoMoeda": "B"
    },
    {
        "nome": "Dólar canadense",
        "codigo": "CAD",
        "tipoMoeda": "A"
    },
    {
        "nome": "Dólar dos Estados Unidos",
        "codigo": "USD",
        "tipoMoeda": "A"
    }
]
```

### histórico

**/cambio/ptax/historico**

Retorna o histórico referente ao PTAX selecionado.

Os codigos dos PTAX estão disponíveis no endpoint de busca (/taxas/busca) e também listados um pouco abaixo.

Há filtro de datas.

Obs: dados disponíveis desde 2000-01-01.

**Parâmetros**

| Parâmetro | Tipo | Descrição | |
| :-: | :-: | - | :-: |
| `codigo`     | `string` | ex: "USD" | obrigatório
| `dataInicio` | `string` | ex: "2023-01-01" | obrigatório
| `dataFim`    | `string` | ex: "2023-05-01" | opcional
| `boletim`    | `string` | "FECHAMENTO" ou "ABERTURA | opcional
| `ordem`      | `string` | "ASC" ou "DESC" | opcional

**Exemplo de chamada:**

```py
import requests as req

URL_BASE = 'https://api.fintz.com.br'
HEADERS = { 'X-API-Key': 'chave-de-testes-api-fintz' }
PARAMS = { 'codigo': 'USD', 'dataInicio': '2020-01-01' }

res = req.get(f'{URL_BASE}/cambio/ptax/historico', headers=HEADERS, params=PARAMS)
print(res.json())
```

**Resposta:**

```json
[
    {
        "codigo": "USD",
        "nome": "Dólar dos Estados Unidos",
        "data": "2023-07-25T13:11:28.371000",
        "cotacaoCompra": 4.749,
        "cotacaoVenda": 4.7496,
        "paridadeCompra": 1.0,
        "paridadeVenda": 1.0,
        "tipoBoletim": "Fechamento",
        "tipoMoeda": "A"
    },
    {
        "codigo": "USD",
        "nome": "Dólar dos Estados Unidos",
        "data": "2023-07-24T13:07:25.216000",
        "cotacaoCompra": 4.7451,
        "cotacaoVenda": 4.7457,
        "paridadeCompra": 1.0,
        "paridadeVenda": 1.0,
        "tipoBoletim": "Fechamento",
        "tipoMoeda": "A"
    }, ...
]
```