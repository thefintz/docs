# Títulos públicos - Tesouro Direto

Permite ao usuário consultar dados de todos os títulos públicos da plataforma
[Tesouro Direto](https://www.tesourodireto.com.br/). Os dados são atualizados
diariamente.

Todos os endpoints desta página tem a seguinte URL base:
> `URL_BASE` = `https://api.fintz.com.br/titulos-publicos/`

## Lista de títulos

Retorna a [lista de títulos públicos](#lista-de-titulos) disponíveis paginada.

**Parâmetros:**

- `pagina`: opcional. Inteiro que representa o índice de página. O valor
  padrão é 1, índice da primeira página.
- `tamanho`: opcional. Inteiro que indica o tamanho da página a ser retornada.
  O valor padrão é 10.

**Exemplo de chamada:**

```bash
curl '{URL_BASE}/tesouro?pagina=1&tamanho=40'
```

**Resposta:**

```json
{
  "pagina": 1,
  "tamanho": 40,
  "total": 112,
  "dados": [
    {
      "codigo": "NTNF20330101",
      "nome": "Tesouro Prefixado com Juros Semestrais 2033",
      "dataVencimento": "2033-01-01",
      "vencido": false,
      "possivelInvestir": true,
      "possivelResgatar": true
    },
    ...
  ]
}
```

## Informações dos títulos

Retorna informações extras sobre um título, como descrição e estratégia.

**Exemplo:**

```bash
curl '{URL_BASE}/tesouro/{codigo}/informacoes'
```

**Resposta:**

```json
{
  "codigo": "NTNBP20240815",
  "nome": "Tesouro IPCA+ 2024",
  "dataVencimento": "2024-08-15",
  "indice": "IPCA",
  "vencido": false,
  "possivelInvestir": false,
  "possivelResgatar": true,
  "descricao": "Título pós-fixado, uma vez que parte do seu rendimento acompanha a variação da taxa de inflação (IPCA).",
  "estrategia": "Aumenta o poder de compra do seu dinheiro, pois seu rendimento é composto por uma taxa de juros + a variação da inflação (IPCA). É mais interessante para quem pode deixar o dinheiro render até o vencimento do investimento, pois não paga juros semestrais. Em caso de resgate antecipado, o Tesouro Nacional garante sua recompra pelo seu valor de mercado.",
  "jurosSemestrais": false
}
```

## Histórico de preços e taxas

Retorna histórico paginado de preços e taxas, com filtros por datas.

**Parâmetros:**

- `pagina`: opcional. Inteiro que representa o índice de página, para
  paginação. O valor padrão é 1, índice da primeira página.
- `tamanho`: opcional. Inteiro que indica o tamanho da página a ser retornada.
  O valor padrão é 10.
- `dataInicio`: opcional. Data do início do período a ser retornado. Formato AAAA-MM-DD.
- `dataFim`: opcional. Data do fim do período a ser retornado. Formato AAAA-MM-DD.

**Exemplo:**

```bash
curl '{URL_BASE}/tesouro/{codigo}/precos/historico?dataInicio=2016-12-31&dataFim=2021-12-31'
```

**Resposta:**

```json
{
  "pagina": 1,
  "tamanho": 10,
  "total": 2597,
  "dados": [
    {
      "codigo": "NTNF20230101",
      "data": "2022-11-01",
      "taxaJurosCompra": 0.1366,
      "taxaJurosVenda": 0.1378,
      "puCompra": 1027.18,
      "puVenda": 1026.48,
      "puBase": 1026.48
    },
    {
      "codigo": "NTNF20230101",
      "data": "2022-10-31",
      "taxaJurosCompra": 0.1366,
      "taxaJurosVenda": 0.1378,
      "puCompra": 1026.66,
      "puVenda": 1025.95,
      "puBase": 1025.95
    },
    ...
  ]
}
```

## Preços e taxas atuais

Retorna preços e taxas dos títulos públicos referentes à data mais atual.
Exclusivo para títulos não vencidos.

**Exemplo:**

```bash
curl '{URL_BASE}/tesouro/{codigo}/precos/atual'
```

**Resposta:**

```json
{
  "codigo": "NTNF20230101",
  "possivelInvestir": false,
  "possivelResgatar": true,
  "taxaJurosCompra": 0.0,
  "taxaJurosVenda": 13.78,
  "puCompra": 0.0,
  "puVenda": 1027.0,
  "minQtdVenda": 0.01,
  "minValorVenda": 10.27,
  "minValorCompra": 0.0,
  "dataUltAtualizacao": "2022-11-01T15:21:01.080000"
}
```

## Pagamentos de cupons de juros

Retorna preços e taxas dos títulos públicos referentes à data mais atual.
Exclusivo para títulos não vencidos.

**Parâmetros:**

- `pagina`: opcional. Inteiro que representa o índice de página paginação. O
  valor padrão é 1, índice da primeira página.
- `tamanho`: opcional. Inteiro que indica o tamanho da página a ser retornada.
  O valor padrão é 10.

**Exemplo:**

```bash
curl '{URL_BASE}/tesouro/{codigo}/cupons?pagina=1&tamanho=20'
```

**Resposta:**

```json
{
  "pagina": 1,
  "tamanho": 20,
  "total": 20,
  "dados": [
    {
      "codigo": "NTNB20450515",
      "dataResgate": "2017-05-15",
      "dataVencimento": "2045-05-15",
      "valor": 88.406696,
      "qtdTotal": 53576.98,
      "valorTotal": 4736563.78
    },
    {
      "codigo": "NTNB20450515",
      "dataResgate": "2016-11-16",
      "dataVencimento": "2045-05-15",
      "valor": 87.022858,
      "qtdTotal": 55416.61,
      "valorTotal": 4822511.79
    },
    ...
  ]
}
```
