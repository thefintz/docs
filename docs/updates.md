[indicadores]: ../endpoints/bolsa/#indicadores
[itenscontabeis]: ../endpoints/bolsa/#itens-contabeis-padronizados
[indices]: ../endpoints/indices

# Notas de Atualização

Aqui você pode acompanhar as novas funcionalidades da API.

Você pode requisitar novas features ou dar feedback pelo nosso email contato@fintz.com.br


???+ note "2023-06-22"
    ## 26 novos índices B3

    Esses índices estão disponíveis no endpoint de [índices][indices]

    | Índice | Descrição |
    | :-: | |
    `IBOV` | Composto pelas ações mais negociadas na B3.
    `SMLL` | O Índice Small Cap (empresas com menor valor de mercado).
    `IDIV` | O Índice Dividendos (empresas conhecidas por pagar bons dividendos).
    `IFIX` | Índice de Fundos de Investimentos Imobiliários (FIIs mais negociados).
    `IBXX` | IBRX 100 (100 ativos de maior negociabilidade e representatividade).
    `IBXL` | IBRX 50 (50 ativos de maior negociabilidade e representatividade).
    `ITAG` | Empresas que favorecem acionistas minoritários na venda da companhia (tag-along).
    `BDRX` | Índice de BDRs Não Patrocinados-GLOBAL.
    `AGFS` | Índice Agronegócio Free Float Setorial.
    `GPTW` | Empresas certificadas pela GPTW como as melhores ambientes para trabalhar.
    `IBRA` | Critérios de inclusão relacionados à governança corporativa e liquidez.
    `ICO2` | O Índice Carbono Eficiente (empresas que reportam emissão).
    `ICON` | O Índice de Consumo (empresas de consumo cíclico, não cíclico e saúde).
    `IEEX` | Índice de Energia Elétrica.
    `IFIL` | Índice de Fundos de Investimentos Imobiliários de Alta Liquidez.
    `IFNC` | Índice Financeiro (setores financeiro e de seguros).
    `IGCT` | Índice de Governança Corporativa Trade.
    `IGCX` | Índice de Ações com Governança Corporativa Diferenciada.
    `IGNM` | Empresas que apresentem bons níveis de governança e listadas no Novo Mercado.
    `IMAT` | Índice de Materiais Básicos.
    `IMOB` | Índice Imobiliário.
    `INDX` | Índice do Setor Industrial.
    `ISEE` | Índice de Sustentabilidade Empresarial.
    `IVBX` | Empresas classificadas a partir da 11ª posição (market cap e liquidez).
    `MLCX` | O Índice MidLarge Cap (ações de médio e grande porte mais negociadas).
    `UTIL` | O Índice Utilidade Pública (setores de eletricidade, água e gás)



???+ note "2023-06-21"
    ## Novos indicadores P/L e L/P

    O L/P tem um objetivo de ordenação, onde se sabe que quanto maior L/P, melhor.  
    O inverso disso não é verdadeiro para P/L, por conta dos valores negativos, veja abaixo.

    Distribuição do P/l
    ```
    Alto -> Caro (ruim)
    Baixo -> Barato (bom)
    Negativo -> Caríssimo (ruim)
    ```
    
    O barato fica no centro, o que é ruim para criar rankings. Quando usamos L/P fica assim:

    Distribuição L/P
    ```
    Alto -> Barato
    Baixo -> Caro (ruim)
    Negativo -> Caríssimo (ruim)
    ```

    Assim podemos ordenar sem problemas.

    Esses indicadores estão disponíveis no endpoint de [indicadores].


???+ note "2023-06-19"
    ## 4 Novos itens contábeis

    Adicionados os seguintes itens contábeis padronizados

    ```
    AcoesEmCirculacao
    TotalAcoes
    LucroLiquidoSociosControladora
    LucroLiquidoSociosControladora12m
    ```

    Esses itens são úteis para uma série de indicadores, esperamos que gostem.

    [Aqui está o link para o endpoint de itens padronizados][itenscontabeis]
