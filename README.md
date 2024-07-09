### <p align="center"><strong>[DG-01] Painel de Inteligência do Mercado de Valores Mobiliários (CVM)</strong></p>
### <p align="center"><strong>[Painel CVM](https://app.powerbi.com/view?r=eyJrIjoiNzUyOWFjZTgtNTgwZi00NjJkLWFjOTEtYjA0NmEyMmU1YjlmIiwidCI6IjI4ZThlYTA4LWE5N2EtNGExYS05ZjU0LWZhMGZmMzc1NDNlYSJ9)</strong></p>

#### Objetivo do Documento:
O objetivo do documento é fornecer uma visão clara e detalhada sobre todos os aspectos essenciais do projeto. Isso inclui definir as metas e objetivos do dashboard, descrever os requisitos funcionais e não funcionais, estabelecer os usuários-alvo e suas necessidades específicas, delinear o escopo do projeto, identificar os recursos e tecnologias a serem utilizados.

#### Justificativa do Projeto:
O Portal de Dados Abertos da Comissão de Valores Mobiliários (CVM) é uma plataforma online que disponibiliza informações e dados financeiros relacionados ao mercado de valores mobiliários no Brasil e foi desenvolvido com o objetivo de promover a transparência e a democratização das informações sobre o mercado financeiro. Na plataforma, temos informações de Balanços Patrimoniais, Demonstração de Fluxo de Caixa (DFC), Demonstração de Resultado (DRE) e mais. 

Entretanto, surge a *necessidade de uma visualização centralizada e acessível dos dados essenciais relacionados ao mercado de valores mobiliários*. Ao contrário de conjuntos de dados estáticos, um dashboard interativo permite que os analistas e decisores tenham uma visão instantânea e clara do estado e das tendências do mercado, facilitando análises rápidas e informadas.

#### Responsabilidades das funções:
Diogo Gonçalves (eu): como *Analista de dados*, fui responsável por todas as etapas do projeto: coleta e ingestão de dados, estruturação e modelagem dos dados, Design, DataViz, documentação do projeto, desenvolvimento de funcionalidades analíticas (Regras e Cálculos) e publicação.

#### Escopo:
🎯 Objetivo: descarregar os dados do exercício de 2022 disponíveis no link abaixo e elabore uma apresentação ou dashboard na ferramenta de preferência destacando informações interessantes (ex. variações ano vs ano, melhores empresas em lucratividade, ranking de margens, etc).

🫂 Público-Alvo:  
Pessoas interessadas no mercado financeiro brasileiro e entusiastas de dados e visualizações.

🗓️ Recorrência:  
Toda segunda-feira às 8 horas. 

📗 Descrição:

⚙️ Fontes:  
Formulário de Demonstrações Financeiras Padronizadas (DFP) [(Link)](https://dados.cvm.gov.br/dados/CIA_ABERTA/DOC/DFP/DADOS/)  
Formulário Cadastral (FCA) [(Link)](https://dados.cvm.gov.br/dados/CIA_ABERTA/DOC/FCA/DADOS/)  
Valores Mobiliários Negociados e Detidos (VLMO) [(Link)](https://dados.cvm.gov.br/dados/CIA_ABERTA/DOC/VLMO/DADOS/)

#### Exclusões:
1. Será excluído do processo de captura de dados do site da CVM os períodos acima de um range de 10 anos;
2. O ano corrente será excluído da análise, pois os períodos de entrega de documentos pelas companhias variam significativamente, e nossa comparação será feita em períodos equivalentes.

#### Premissas:
1. O projeto considerará as informações consolidadas e anuais dos arquivos;
2. O foco do projeto será nas demonstrações financeiras: DRE, BP e Fluxo de Caixa;
3. Visualização de Dados no *Power BI*;
4. Ingestão de Dados com *Python*;
5. Tratamento de Dados com *T-SQL* no SQL Server e *Power Query (incluindo Query Folding)* no Power BI;
6. Atualização dos dados com o uso do Gateway e Windows Task Scheduler.

##### Regras de Negócio:
