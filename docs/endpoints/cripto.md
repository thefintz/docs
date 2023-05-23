[contato]: https://fintz.com.br/#/contato

# Criptomoedas

Esses endpoints estão em fase de beta fechado e vão ser lançados dia 15/10/2023.

Tem interesse em participar do beta? [Entre em contato][contato].

## Cotação

~ em breve

## Logos e ícones

Retorna a URL da logo da criptomoeda baseada no seu código de negociação. Exemplo: Bitcoin é BTC

Suporta ações, BDRs, FIIs, e ETFs.

Nesse endpoint, a URL_BASE não é utilizada, a base deve ser:
> `BASE` = `https://cdn.jsdelivr.net/gh/monneda/B3-Assets-Images`

**Parâmetros**

- `ticker`: um `string`, _case insensitive_ com o ticker do ativo desejado.
  Exemplo: `BTC` ou `ETH`.

**Estrutura de chamada**

```bash
curl '{BASE}/main/imgs/{{ticker}}.png'
```

**Exemplo de chamada**

```bash
curl 'https://raw.githubusercontent.com/thecartera/B3-Assets-Images/main/imgs/ETH.png'
```

**Resposta do exemplo:**

![BDR da Tesla, TSLA34](https://raw.githubusercontent.com/thecartera/B3-Assets-Images/main/imgs/ETH.png)

