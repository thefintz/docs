## Listagem

### Lista de criptomoedas

Retorna o nome de todas as criptomoedas que possuímos.

Hoje temos cotações com 15 minutos de atraso e cotações históricas (2 anos) de mais de 1.350 criptomoedas.

`GET {URL_BASE}/criptomoedas`

```json
[
  "BTC",
  "ETH",
  "DOGE",
  ...
]
```

## Cotações

### Cotação atual

Retorna a mais recente cotação da criptomoeda especificada

`GET {URL_BASE}/criptomoedas/cotacao?ticker=DOGE`

```json
{
  "nome": "DOGE",
  "tipo": "CRIPTO",
  "ticker": "DOGE",
  "preco": 0.66828312,
  "data": "2022-04-08T23:02:39.179058780Z",
  "resumo": "Lançada em 2014 por Billy Markus, um desenvolvedor de software que começou a trabalhar no código da Dogecoin para homenagear o meme do cachorro japonês da raça Shiba Inu, que bombou nas redes sociais em 2013. A imagem do cão é o ícone da moeda.",
  "whitepaper": "link"
}
```

### Cotação histórica/passada

Retorna, para a data especificada, a última cotação da moeda

`GET {URL_BASE}/criptomoedas/cotacao?ticker=DOGE&data=2022-04-01`

```json
{
  "nome": "DOGE",
  "tipo": "CRIPTO",
  "ticker": "DOGE",
  "preco": 0.64901476,
  "data": "2022-04-01",
  "resumo": "Lançada em 2014 por Billy Markus, um desenvolvedor de software que começou a trabalhar no código da Dogecoin para homenagear o meme do cachorro japonês da raça Shiba Inu, que bombou nas redes sociais em 2013. A imagem do cão é o ícone da moeda.",
  "whitepaper": "link"
}
```