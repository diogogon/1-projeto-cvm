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

**A) Ingestão de Dados**: processo de coletar dados diretamente das fontes de origem, sem aplicar filtros, para garantir a integridade e a abrangência das informações.

1. Cias Abertas: Documentos: Formulário de Demonstrações Financeiras Padronizadas (DFP) [Link](https://dados.cvm.gov.br/dataset/cia_aberta-doc-dfp):  
Tabelas extraídas das Demonstrações Financeiras (BP, DRE e DFC) no conjundo de dados *dfp_cia_aberta*: dfp_cia_aberta_BPA_con, dfp_cia_aberta_BPP_con, dfp_cia_aberta_DFC_MI_con, dfp_cia_aberta_DRE_con, dfp_cia_aberta_parecer e dfp_cia_aberta

2. Cias Abertas: Documentos: Formulário Cadastral (FCA) [Link](https://dados.cvm.gov.br/dataset/cia_aberta-doc-fca):  
Tabelas extraídas do cadastro relativo às companhias e auditores no conjundo de dados *fca_cia_aberta*: fca_cia_aberta_endereco, fca_cia_aberta_auditor, fca_cia_aberta_geral

**B) Integração de Dados**: etapa de integrar e combinar múltiplas fontes de dados. Esse processo, que será realizado localmente por meio do Python (os scripts estão postados na pasta), tem a função de armazenar os arquivos em pastas nomeadas como *"base, extracao e empilhado"*, de acordo com o avanço dessa fase. Portanto, em *"base"* temos todos os arquivos zipados da CVM; em *"extração"*, os arquivos .csv extraídos dos zips; e por fim, em *"empilhado"*, arquivos empilhados que selecionamos por assunto (BP, DRE, DFC, parecer, link, endereco, auditor e geral) que iremos subir para o SQL Server.

**C) Transformação de Dados**: para este conjunto de dados da CVM, focaremos no processo de uniformização de formatos e unidades, seleção e filtragem dos dados relevantes. Essas atividades serão realizadas primeiramente no SQL Server e continuamente no Power Query do Power BI.  
1. SQL Server: na plataforma, seguindo o paradigma de Modelagem Dimensional para organizar as tabelas em dimensões e fatos, será implementado Views para que o Power BI tenha acesso aos dados pertinentes para o projeto. Nesse momento, é preciso destacar apenas as duas fatos; as demais seguem a mesma lógica.
```sql
-- vw_DREcons
SELECT 
      CAST([DT_REFER] AS DATE) AS [DT_REFER], YEAR([DT_REFER]) AS 'ANO',[ESCALA_MOEDA],[VERSAO],[CNPJ_CIA],[DENOM_CIA],[CD_CONTA],[DS_CONTA], TRY_CAST([VL_CONTA] AS DECIMAL(20, 2)) AS [VL_CONTA]
FROM [CVM_DADOS].[dbo].[DRE]
WHERE [ORDEM_EXERC] = 'ÚLTIMO' AND [GRUPO_DFP] = 'DF Consolidado - Demonstração do Resultado'
```
```sql
-- vw_BPcons
SELECT 
	CAST([DT_REFER] AS DATE) AS [DT_REFER], YEAR([DT_REFER]) AS 'ANO',[ESCALA_MOEDA], [VERSAO], [CNPJ_CIA], [DENOM_CIA], [CD_CONTA], [DS_CONTA], TRY_CAST([VL_CONTA] AS DECIMAL(20, 2)) AS [VL_CONTA]
FROM [CVM_DADOS].[dbo].[BPA] AS A
WHERE [ORDEM_EXERC] = 'ÚLTIMO' AND [GRUPO_DFP] = 'DF Consolidado - Balanço Patrimonial Ativo'

UNION

SELECT 
	CAST([DT_REFER] AS DATE) AS [DT_REFER], YEAR([DT_REFER]) AS 'ANO', [ESCALA_MOEDA], [VERSAO], [CNPJ_CIA], [DENOM_CIA], [CD_CONTA], [DS_CONTA], TRY_CAST([VL_CONTA] AS DECIMAL(20, 2)) AS [VL_CONTA]
FROM [CVM_DADOS].[dbo].[BPP] AS P
WHERE [ORDEM_EXERC] = 'ÚLTIMO' AND [GRUPO_DFP] = 'DF Consolidado - Balanço Patrimonial Passivo'
```
2. Power BI: construção das hierarquias para as demonstrações financeiras DRE e BP, tipagem dos campos, agregações e mesclas.

**D) DataViz**: processo de construção de layout, design visual e visualizações adequadas para os dados. Todo o design foi feito no Figma e, para este projeto pessoal, foi interessante seguir os padrões estabelecidos pela [identidade visual](https://www.gov.br/cvm/pt-br/canais_atendimento/imprensa/identidade-visual-manual-da-marca) da CVM, tanto para as cores como para a marca.

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

#### Inconsistências e observações:
1. Delimitador dos arquivos .csv: ";"
2. O campo [VL_CONTA] quando aberto em excel perde a configuração exata do valor, por isso, é importante abrir os arquivos .csv como texto para explorar as informações corretamente;
3. O campo [ORDEM_EXERC] das demonstrações financeiras possuem o "ÚLTIMO" e "PENÚLTIMO" exercício da companhia;
4. O campo [ESCALA_MOEDA] possui registrado os valores de "MIL" e "UNIDADE", levando a crer que há companhias com valores maiores que o esperado em [VL_CONTA];
5. O campo [DT_REFER] refere-se a informações anuais, logo não é necessário saber a data exata de registro das informações de cada companhia;
6. Relevante utilizar a codificação "ANSI" para a exibição correta de caracteres em idiomas europeus ocidentais, incluindo acentos. 

##### Regras de Negócio:
