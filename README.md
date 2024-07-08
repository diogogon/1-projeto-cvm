#### [DG-01] Painel de Inteligência do Mercado de Valores Mobiliários (CVM)
 
##### Objetivo do Documento:

##### Justificativa do Projeto:
O Portal de Dados Abertos da Comissão de Valores Mobiliários (CVM) é uma plataforma online que disponibiliza informações e dados financeiros relacionados ao mercado de valores mobiliários no Brasil e foi desenvolvido com o objetivo de promover a transparência e a democratização das informações sobre o mercado financeiro. Na plataforma, temos informações de Balanços Patrimoniais, Demonstração de Fluxo de Caixa (DFC), Demonstração de Resultado (DRE) e mais. 

Entretanto, surge a *necessidade de uma visualização centralizada e acessível dos dados essenciais relacionados ao mercado de valores mobiliários*. Ao contrário de conjuntos de dados estáticos, um dashboard interativo permite que os analistas e decisores tenham uma visão instantânea e clara do estado e das tendências do mercado, facilitando análises rápidas e informadas.

##### Responsabilidade das funções:

##### Escopo:
🎯 Objetivo:

🗓️ Recorrência:

📗 Descrição:

⚙️ Fontes:  
1. [Formulário de Demonstrações Financeiras Padronizadas (DFP)](https://dados.cvm.gov.br/dados/CIA_ABERTA/DOC/DFP/DADOS/)  
2. [Formulário Cadastral (FCA)](https://dados.cvm.gov.br/dados/CIA_ABERTA/DOC/FCA/DADOS/)  
3. [Valores Mobiliários Negociados e Detidos (VLMO)](https://dados.cvm.gov.br/dados/CIA_ABERTA/DOC/VLMO/DADOS/)

##### Exclusões:
1. Será excluído do processo de captura de dados do site da CVM os períodos acima de um range de 10 anos;
2. O ano corrente será excluído da análise, pois os períodos de entrega de documentos pelas companhias variam significativamente, e nossa comparação será feita em períodos equivalentes.

##### Premissas:
1. O projeto considerará as informações consolidadas e anuais dos arquivos;
2. O foco do projeto será nas demonstrações financeiras: DRE, BP e Fluxo de Caixa;
3. Visualização de Dados no *Power BI*;
4. Ingestão de Dados com *Python*;
5. Tratamento de Dados com *T-SQL* no SQL Server e *Power Query (incluindo Query Folding)* no Power BI;
6. Atualização dos dados com o uso do Gateway e Windows Task Scheduler.

##### Regras de Negócio:
