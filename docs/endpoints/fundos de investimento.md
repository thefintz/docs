# Fundos de Investimento

Todos os endpoints desta página tem a seguinte url base:
> `URL_BASE` = `https://0o1jvhh5z7.execute-api.us-east-2.amazonaws.com`

## Dados cadastrais

**Exemplo de chamada**

```bash
curl '{URL_BASE}/funds/20458815000126/info'
```

**Resposta do exemplo**
```json
{
  "id": 29236,
  "tp_fundo": "FI",
  "cnpj_fundo": "20.458.815/0001-26",
  "denom_social": "ASA HEDGE FUNDO DE INVESTIMENTO EM COTAS DE FUNDOS DE INVESTIMENTO MULTIMERCADO",
  "dt_reg": "2014-08-20",
  "dt_const": "2014-08-19",
  "cd_cvm": "231371",
  "dt_cancel": null,
  "sit": "EM FUNCIONAMENTO NORMAL",
  "dt_ini_sit": "2014-09-01",
  "dt_ini_ativ": "2014-09-01",
  "dt_ini_exerc": "2022-07-01",
  "dt_fim_exerc": "2023-06-30",
  "classe": "Fundo Multimercado",
  "dt_ini_classe": "2014-08-19",
  "rentab_fundo": null,
  "condom": "Aberto",
  "fundo_cotas": "S",
  "fundo_exclusivo": "N",
  "trib_lprazo": "S",
  "publico_alvo": "Público Geral",
  "entid_invest": null,
  "taxa_perfm": 20.0,
  "inf_taxa_perfm": "O fundo cobrara 20.00 % do que exceder 100.00 % o indice CDIE. A taxa de performance sera paga no(s) mes(es) de Janeiro e Julho",
  "taxa_adm": 2.0,
  "inf_taxa_adm": null,
  "vl_patrim_liq": 645066940.57,
  "dt_patrim_liq": "2022-08-10",
  "diretor": "CARLOS ALBERTO SARAIVA",
  "cnpj_admin": "02.201.501/0001-61",
  "admin": "BNY MELLON SERVICOS FINANCEIROS DTVM S.A.",
  "pf_pj_gestor": "PJ",
  "cpf_cnpj_gestor": "19.807.960/0001-96",
  "gestor": "ASA ASSET 2 GESTÃO DE RECURSOS LTDA.",
  "cnpj_auditor": "57.755.217/0001-29",
  "auditor": "KPMG AUDITORES INDEPENDENTES LTDA.",
  "cnpj_custodiante": "42.272.526/0001-70",
  "custodiante": "BNY MELLON BANCO S.A.",
  "cnpj_controlador": "02.201.501/0001-61",
  "controlador": "BNY MELLON SERVICOS FINANCEIROS DTVM S.A."
}
```

## Dados diários

**Exemplo de chamada**
```bash
curl '{URL_BASE}/funds/20458815000126/info/daily'
```

**Resposta do exemplo**
```json
{
  "id": 65615,
  "tp_fundo": "FI",
  "cnpj_fundo": "20.458.815/0001-26",
  "dt_comptc": "2022-08-11",
  "vl_total": 653659975.77,
  "vl_quota": 272.34085014,
  "vl_patrim_liq": 653606761.94,
  "captc_dia": 8268478.19,
  "resg_dia": 1995437.33,
  "nr_cotst": 8162
}
```

## Rentabilidade 

### Rentabilidade por mês


**Exemplo de chamada**
```bash
curl '{URL_BASE}/funds/20458815000126/variation/monthly?months=12'
```

**Resposta do exemplo**
```json
[
  { "date": "2022-08", "value": 0.02883744379895803  },
  { "date": "2022-07", "value": -0.013607396787985504  },
  { "date": "2022-06", "value": 0.049128080597900636  },
  { "date": "2022-05", "value": -0.011539345430285564  },
  { "date": "2022-04", "value": 0.04933599712901815  },
  { "date": "2022-03", "value": 0.0734138721740174  },
  { "date": "2022-02", "value": 0.04878253757898032  },
  { "date": "2022-01", "value": 0.0412624934152348  },
  { "date": "2021-12", "value": 0.012115505474624255  },
  { "date": "2021-11", "value": 0.01033438875093462  },
  { "date": "2021-10", "value": 0.01623116529351365  },
  { "date": "2021-09", "value": 0.031492725839284974  }
]
```

### Rentabilidade por ano

**Exemplo de chamada**
```bash
curl '{URL_BASE}/funds/20458815000126/variation/yearly?years=4'
```

**Resposta do exemplo**
```json
[
  { "date": "2022", "value": 0.29452939036592873  },
  { "date": "2021", "value": 0.03921573955793067  },
  { "date": "2020", "value": 0.1294212686886682  },
  { "date": "2019", "value": 0.08729201011281318  }
]
```

### Rentabilidade por data

**Exemplo de chamada**
```bash
curl '{URL_BASE}/funds/20458815000126/returns?start=2021-12-028&end=2022-01-01'
```

**Resposta do exemplo**
```json
[
    { "date": "2021-12-31", "value": 0.2624618907530425  },
    { "date": "2021-12-30", "value": 0.2639520824256263  },
    { "date": "2021-12-29", "value": 0.26204329621649003  },
    { "date": "2021-12-28", "value": 0.2585482210180916  }
]
```