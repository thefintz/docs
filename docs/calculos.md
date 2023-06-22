[indicadores]: ../endpoints/bolsa/#indicadores
[itenscontabeis]: ../endpoints/bolsa/#itens-contabeis-padronizados
[indices]: ../endpoints/indices

# Como calculamos

Aqui você pode entender exatamente como calculamos cada indicador.

Você pode requisitar novas features ou dar feedback pelo nosso email contato@fintz.com.br


???+ ROE
    O cálculo do ROE diverge das seguintes maneiras:
    - usar o patrimônio inicial, médio ou final do período de análise.
    - usar lucro líquido total ou atribuído aos sócios controladores.
    
    Para uma data especificada, o ROE que fornecemos na API é calculado utilizando o lucro líquido atribuído aos sócios controladores e acumulado dos 12 meses anteriores dividido pelo patrimônio líquido final do período.

    Lembrando que fornecemos todos os itens contábeis padronizados para caso você queira calcular do jeito que preferir.
