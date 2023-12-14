[indicadores]: ../endpoints/bolsa/#indicadores
[itenscontabeis]: ../endpoints/bolsa/#itens-contabeis-padronizados
[indices]: ../endpoints/indices
[taxas]: ../endpoints/indices/#taxas

# Notas de Atualização

Aqui você pode acompanhar as novas funcionalidades da API.

Você pode requisitar novas features ou dar feedback pelo nosso email contato@fintz.com.br

??? note "Dezembro 2023 - Novos indicadores e endpoints"

    Esse mês focamos em adicionar mais indicadores, novos endpoints para atender outros casos de uso, e proventos de FIIs:
    
    - (12/12) Mais 21 indicadores
    - (22/12) Mais 1 endpoint para indicador
    - (22/12) Mais 1 endpoint para itens contábeis
    - (22/12) Proventos FIIs.

    ## +21 Indicadores

    - ValorDeMercado
    - EV
    - P_L
    - P_VP
    - VPA
    - LPA
    - EV_EBITDA
    - EV_EBIT
    - P_EBITDA
    - P_EBIT
    - P_Ativos
    - P_SR
    - P_CapitalDeGiro
    - P_AtivoCirculanteLiquido
    - DividaBruta_PatrimonioLiquido
    - EBIT_Ativos
    - EBIT_DespesasFinanceiras
    - EBITDA_DespesasFinanceiras
    - EBITDA_EV
    - EBIT_EV
    - L_P

??? note "Novembro 2023 - Muitas Novidades"

    Todos os indicadores e itens contábeis foram adicionados tanto em endpoints de arquivo como de JSON, assim como dados point in time e não point in time.

    ## +14 indicadores

    - DL/PL
    - DL/EBITDA
    - DL/EBIT
    - PL/ATIVOS
    - PASSIVOS/ATIVOS
    - LIQ. CORRENTE
    - M. BRUTA
    - M. EBITDA
    - M. EBIT
    - M. LIQ.
    - ROE
    - ROA
    - ROIC
    - GIRO ATIVOS

    ## +28 itens contábeis

    - AtivoCirculante
    - AtivoNaoCirculante
    - AtivoTotal
    - CaixaEquivalentes
    - Custos
    - DepreciacaoAmortizacao
    - DespesasFinanceiras
    - DespesasReceitasOperacionaisAdministrativas
    - Disponibilidades
    - DividaBruta
    - DividaLiquida
    - Ebit
    - Ebitda
    - EquivalenciaPatrimonial
    - Impostos
    - Lair
    - LucroLiquido
    - LucroLiquidoOpContinuadas
    - LucroLiquidoOpDescontinuadas
    - LucroLiquidoSociosControladora
    - PassivoCirculante
    - PassivoNaoCirculante
    - PassivoTotal
    - PatrimonioLiquido
    - ReceitaLiquida
    - ReceitasFinanceiras
    - ResultadoBruto
    - ResultadoFinanceiro

    ## Separando dados Point in Time e comuns.
    
    Também estamos trabalhando para deixar mais clara a diferenciação quando dados são point in time ou não.

??? note "Outubro 2023 - Atualização diária dos dados"
    ## Atualização diária de todos os históricos

    Agora tanto os arquivos `parquet` quanto os endpoints JSONs possuem dados atualizados diariamente, seja de cotações, itens contábeis ou mesmo indicadores.

??? note "Setembro 2023 - Refatoração e Otimização"
    ## Refatoração e preparação para novidades

    Tiramos esse mês para focar em otimizações de algoritmo e refatoração.
    
    Muito do que construímos nos últimos meses foi focado no caso de uso de backtest, com dados point in time. 
    
    E desenvolvemos rápido. Com as demandas dos usuários de que os dados atualizem diariamente, o processamento estava ficando caro e lento. A adição de novas features também estava lenta por questão dos débitos técnicos.

    Agora vamos otimizar tudo isso, permitindo adicionarmos novas features e funcionalidades muito mais rápido nos próximos meses. E também atendermos os casos de uso de dashboards e criação de sites, com vários endpoints que facilitam a vida do usuário.

    Um pouco do que está por vir até o fim do ano:

    - +30 indicadores
    - +30 itens contábeis
    - Separação de endpoints comuns e point in time
    - +3 novos endpoints indicadores:  
        - escolho um indicador e um ticker, vem todo o histórico
        - escolho um indicador, vem o valor mais recente para todos os tickers
        - escolho um ticker, vem o valor mais recente de todos os indicadores
    - +3 novos endpoints itens contábeis:  
        - escolho um item contabil e um ticker, vem todo o histórico
        - escolho um item contabil, vem o valor mais recente para todos os tickers
        - escolho um ticker, vem o valor mais recente de todos os itens contábeis
    - Proventos e indicadores de FIIs

??? note "Agosto 2023 - Adicionadas Taxas e Câmbio"
    ## Taxas e câmbio!

    Agora você tem acesso ao histórico de diversas taxas e câmbios como:

    ```
    CDI e seus acumulados
    Selic e seus acumulados
    Dólar
    Euro
    Libra
    e muito mais
    ```

    Aqui está o link para os [endpoints][taxas]

    ## 3 Novos indicadores

    Adicionados os seguintes indicadores

    ```
    EV
    EV_EBIT
    ValorDeMercado
    ```

    Aqui está o link para o [endpoint de indicadores][indicadores]

    ## Novo: ReceitaLiquida

    Adicionados os seguintes itens contábeis padronizados

    ```
    ReceitaLiquida
    ReceitaLiquida12m
    ```

    Esses itens são úteis para uma série de indicadores, esperamos que gostem.

    Aqui está o link para o [endpoint de itens padronizados][itenscontabeis]

??? note "Julho 2023 - Adicionados índices B3"
    ## +26 índices de mercado

    Esses índices estão disponíveis no [endpoint de índices][indices]

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



??? note "Junho 2023 - Novos indicadores point in time"
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

    Esses indicadores estão disponíveis no [endpoint de indicadores].

    ## 4 Novos itens contábeis

    Adicionados os seguintes itens contábeis padronizados

    ```
    AcoesEmCirculacao
    TotalAcoes
    LucroLiquidoSociosControladora
    LucroLiquidoSociosControladora12m
    ```

    Esses itens são úteis para uma série de indicadores, esperamos que gostem.

    Aqui está o link para o [endpoint de itens padronizados][itenscontabeis]
