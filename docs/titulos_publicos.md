## Listagem

### Lista de títulos

Retorna os títulos públicos vendidos no tesouro direto.

`GET {URL_BASE}/titulospublicos`

```json
[
  "selic25",
  "selic27",
  "preFix25",
  "preFix29",
  "preFix33comJurosSemestrais",
  "IPCA26",
  "IPCA35",
  "IPCA45",
  "IPCA32comJurosSemestrais",
  "IPCA40comJurosSemestrais",
  "IPCA55comJurosSemestrais",
]
```

## Preços e rentabilidade

### Rentabilidade Título por ticker

Retorna o título público especificado.

`GET {URL_BASE}/titulospublicos?ticker="selic25"`

```json
"selic25": {
  "ticker": "Tesouro Selic 2025",
  "explicacao": "Título com rentabilidade diária vinculada à taxa de juros da economia (taxa Selic). Isso significa que se a taxa Selic aumentar a sua rentabilidade aumenta e se a taxa Selic diminuir, sua rentabilidade diminui.",
  "sobre": "Como não paga juros semestrais, é mais interessante para quem pode deixar o dinheiro render até o vencimento do investimento ou até quando quiser vender",
  "indicacao": "Indicado para aqueles que querem realizar investimentos de curto prazo",
  "vencimento": "2025-03-01T00:00:00",
  "precoUnitario": 11516.67,
  "investimentoMinimo": 115.16,
  "tipo": "SELIC",
  "juros": 0.0714,
  "rentabilidadeAnual": "SELIC + 0,0714%"
}
```