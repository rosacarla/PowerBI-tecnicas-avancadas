# 📊 Técnicas avançadas de Power BI

<p align="justify"> 
Projeto em Power BI com a base de dados AdventureWorks (uma empresa fictícia criada pela Microsoft), sendo desenvolvido a partir de material e atividades práticas do curso online _Técnicas Avançadas de Power BI_, realizado na plataforma LinkedIn Learning.  
</p>  

#### 📑 **CONTEÚDOS DO CURSO:**

☑️ **0. Introdução**  
- Bem-vindos ao curso avançado de Power BI  
- O que você precisa saber para aproveitar esse curso  


☑️ **1. Conceitos e objetivos do Business Intelligence**  
- Conceito e importância do business intelligence  
<p align="center">
	<img src="" width="500">
</p>

- Apresentação dos arquivos e projeto do curso  

<p align="center">
	<img src="" width="500">
</p>  

[Arquivos de exercícios]()  


☑️ **2. Conhecendo o ecossistema do Power BI**   
- Compreenda as diferentes plataformas da Microsoft para análise de dados  
<p align="center">
	<img src="" width="500">
</p>  

- Conheça outros softwares de Business Intelligence  
<p align="center">
	<img src="" width="500">
</p> 


☑️ **3. Importação de dados**  
- Conheça os diferentes tipos de dados  
Exemplo de funcionalidade: ODBC (conector universal de dados)  
<p align="center">
	<img src="" width="500">
</p>   

- Como importar dados do Excel e funções da linguagem M (Power Query)  
Funções automáticas em uso (conforme Etapas Aplicadas):  
Fonte conecta a arquivo Excel (escolher opção Tabela (ícone azul) para importar, não usar Planilha para evitar importação duplicada, pois tabelas são intervalos delimitados com cabeçalhos e tipos de dados definidos)
``` 
= Excel.Workbook(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.3\03_02_Clientes.xlsx"), null, true)  
```  
Tipo alterado 
``` 
= Table.TransformColumnTypes(DadosClientes_Table,{{"ID Cliente", Int64.Type}, {"Cliente", type text}, {"CEP", type text}, {"Data Pedido", type date}})
```  
- Como importar dados de CSV e TXT  
Funções automáticas em uso (conforme Etapas Aplicadas):  
Fonte conecta a arquivo CSV e TXT  
```
= Csv.Document(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.3\03_03_Taxa Selic.txt"),[Delimiter=";", Columns=11, Encoding=65001, QuoteStyle=QuoteStyle.None])  
```
Exemplo de configuração da função Csv.Document (sintaxe do Power Query)  
<p align="center">
	<img src="" width="500">
</p>  

Tipo Alterado
```
= Table.TransformColumnTypes(Fonte,{{"Column1", type text}, {"Column2", type text}, {"Column3", type text}, {"Column4", type text}, {"Column5", type text}, {"Column6", type text}, {"Column7", type text}, {"Column8", type text}, {"Column9", type text}, {"Column10", type text}, {"Column11", type text}})  
```  
- Como importar dados da pasta  
Funções automáticas em uso (conforme Etapas Aplicadas):
Fonte conecta a uma Pasta do Windows (arquivos inicialmente importados como conteúdo binário; todas as importações de arquivo para o Power BI ficam dessa forma)
```
= Folder.Files("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.3\03_04_Pedidos")  
```  
Outras Colunas Removidas (Remover Outras Colunas selecionado com botão direito pelo cabeçalho de uma coluna; removidas colunas com informações irrelevantes de configuração)
```
= Table.SelectColumns(Fonte,{"Content"})  
```
Personalização Adicionada (aba Adicionar Coluna/Coluna Personalizada; "Excel.Workbook" transforma pasta de trabalho de conteúdo Binary para objeto Table e adiciona a coluna Personalizar) 
```
= Table.AddColumn(#"Outras Colunas Removidas", "Personalizar", each Excel.Workbook([Content]))  
```
Colunas Removidas (Remover selecionado com botão direito pelo cabeçalho - Content - da coluna a excluir)  
```
= Table.RemoveColumns(#"Personalização Adicionada",{"Content"})  
```  
Personalizar Expandido (clicar no botão Expandir dentro da coluna Personalizar, desmarcar "Use nome da coluna original como prefixo" para criar colunas da tabela com seus nomes originais sem copiar junto o "Personalizar" da coluna expandida)  
```
= Table.ExpandTableColumn(#"Colunas Removidas", "Personalizar", {"Name", "Data", "Item", "Kind", "Hidden"}, {"Name", "Data", "Item", "Kind", "Hidden"})  
```  
Linhas Filtradas (por tipo tabela)  
```
= Table.SelectRows(#"Personalizar Expandido", each ([Kind] = "Table"))  
```
Outras Colunas Removidas1 (Remover Outras Colunas selecionado com botão direito pelo cabeçalho da coluna Data para permanecer só com esta coluna)  
```
= Table.SelectColumns(#"Linhas Filtradas",{"Data"})  
```
Data (depois de clicar em Expandir, visualiza abertura da coluna - pasta importada - composta por 5 linhas - arquivos - contendo 1 tabela em cada; seleciona uma linha da coluna para expandir informações da tabela correspondente)  
```
= #"Outras Colunas Removidas1"{0}[Data]  
```  
Data Expandido (clicar no botão Expandir dentro da coluna Data sem prefixo marcado para expansão de todas as tabelas, visualiza-se todas as informações dos 5 arquivos em reunidas em uma tabela)  
```
= Table.ExpandTableColumn(#"Outras Colunas Removidas1", "Data", {"Pedido", "Cód. Cliente", "Data Pedido", "Data Faturamento", "Cód. Item", "Quantidade", "Pais"}, {"Pedido", "Cód. Cliente", "Data Pedido", "Data Faturamento", "Cód. Item", "Quantidade", "Pais"})  
```  
- Como importar dados do SQL Server  
Funçãio automática em uso (conforme Etapas Aplicadas): 
Fonte conecta ao SQL Server
<p align="center">
	<img src="" width="500">
</p>  

- Como importar dados de fontes da Web utilizando tabelas  
Funções automáticas em uso (conforme Etapas Aplicadas):  
Fonte conecta à conteúdo da Web em tabela  
```
= Web.BrowserContents("https://pt.wikipedia.org/wiki/Lista_de_pa%C3%ADses_por_popula%C3%A7%C3%A3o")  
```  
Tabela Extraída do HTML  
```
= Html.Table(Fonte, {{"Column1", "TABLE.wikitable.sortable.jquery-tablesorter > * > TR > :nth-child(1)"}, {"Column2", "TABLE.wikitable.sortable.jquery-tablesorter > * > TR > :nth-child(2)"}, {"Column3", "TABLE.wikitable.sortable.jquery-tablesorter > * > TR > :nth-child(3)"}, {"Column4", "TABLE.wikitable.sortable.jquery-tablesorter > * > TR > :nth-child(4)"}, {"Column5", "TABLE.wikitable.sortable.jquery-tablesorter > * > TR > :nth-child(5)"}}, [RowSelector="TABLE.wikitable.sortable.jquery-tablesorter > * > TR"])  
```
Cabeçalhos Promovidos  
```
= Table.PromoteHeaders(#"Tabela extraída de HTML", [PromoteAllScalars=true])  
```
Tipo Alterado  
```
= Table.TransformColumnTypes(#"Cabeçalhos Promovidos",{{"Posição", type text}, {"País (ou território dependente)", type text}, {"Estimativa da ONU", type text}, {"Data", Int64.Type}, {"Estimativa Oficial", type text}})  
```
```
= Table.TransformColumnTypes(#"Cabeçalhos Promovidos",{{"Posição", type number}, {"País (ou território dependente)", type text}, {"Estimativa da ONU", type text}, {"Data", Int64.Type}, {"Estimativa Oficial", type text}})  
```  
- Como importar dados de fontes da Web utilizando exemplos 
Funções automáticas em uso (conforme Etapas Aplicadas):  
Fonte conecta à conteúdo da Web
```
= Web.BrowserContents("https://www.ibge.gov.br/")  
```
Tabela extraída de HTML  
```
= Html.Table(Fonte, {{"Column1", ".indicador-title"}, {"Column2", ".indicador-value"}, {"Column3", ".indicador-text"}, {"Column4", "SMALL"}, {"Column5", ".dado-periodo"}}, [RowSelector=".indicadores-list A"])  
```
Tipo Alterado
```
= Table.TransformColumnTypes(#"Tabela extraída de HTML",{{"Column1", type text}, {"Column2", Percentage.Type}, {"Column3", type text}, {"Column4", type text}, {"Column5", type text}})  
```
<p align="center">
	<img src="" width="750">
</p>  


☑️ **4. Tratamento de dados importados**  
- Apresentação da linguagem M  
Linguagem M | Linguagem DAX  
-|-
Realizada por etapas; editor avançado (guia Exibição) agrupa as funções por etapas. | Utilizadas para criar cálculos e medidas.
Funções são escritas em inglês e os argumento separados por vírgula.| Pode ser ccessada só dentro do Power BI.
Presente só dentro do Power Query. | Não é possível utilizar funções DAX dentro do Power Query.  

- Introdução ao editor de consultas avançado  
<p align="center">
	<img src="" width="750">
</p>  

- Limpar dados indesejados  
Funções automáticas em uso (conforme Etapas Aplicadas):   
Fonte conecta a arquivo Excel  
```
= Excel.Workbook(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.4\04_03_Populacao 2001 a 2018.xlsx"), null, true)  
```  
Navegação (por pela aba da tabela População por Ano)  
```
= Fonte{[Item="População por Ano",Kind="Sheet"]}[Data]  
``` 
Linhas Principais Removidas (remoção das 3 primeiras linhas da tabela com texto irrelevante no cabeçalho, feita por Página Inicial/Remover linhas)  
```
= Table.Skip(#"População por Ano_Sheet",3)  
```  
Cabeçalhos Promovidos (clicar no ícone azul de tabela, opção "Usar Primeira Linha como Cabeçalho")  
```
= Table.PromoteHeaders(#"Linhas Principais Removidas", [PromoteAllScalars=true])  
```
Tipos Alterados (alteração automática de tipos após promoção de cabeçalho)  
```
= Table.TransformColumnTypes(#"Cabeçalhos Promovidos",{{"Unidades da Federação", type text}, {"Região", type text}, {"Publicação", type date}, {"2001", Int64.Type}, {"2002", Int64.Type}, {"2003", Int64.Type}, {"2004", Int64.Type}, {"2005", Int64.Type}, {"2006", Int64.Type}, {"2007", Int64.Type}, {"2008", Int64.Type}, {"2009", Int64.Type}, {"2010", Int64.Type}, {"2011", Int64.Type}, {"2012", Int64.Type}, {"2013", Int64.Type}, {"2014", Int64.Type}, {"2015", Int64.Type}, {"2016", Int64.Type}, {"2017", Int64.Type}, {"2018", type any}})  
```
Linhas Filtradas (filtro de linhas da tabela preenchidas com "null", selecionadas na seta para baixo pelo cabeçalho da coluna)  
```
= Table.SelectRows(#"Tipo Alterado", each ([Unidades da Federação] <> null))  
```
- Transforme colunas em linhas  
Funções automáticas em uso (conforme Etapas Aplicadas):   
Colunas Não Dinâmicas (colunas dos Anos tem os valores transpostos para linhas e acrescentadas as colunas Atributo (anos) e Valor (valores de cada ano); tabela transformada com apenas 5 colunas)
```
= Table.UnpivotOtherColumns(#"Linhas Filtradas", {"Unidades da Federação", "Região", "Publicação"}, "Atributo", "Valor")  
```
Colunas Renomeadas (coluna Atributo renoneada como Anos)
```
= Table.RenameColumns(#"Colunas Não Dinâmicas",{{"Atributo", "Anos"}})  
```
- Utilize o preenchimento para cima e para baixo  
Função automática em uso (conforme Etapas Aplicadas):  
Preenchido Abaixo (preenche linhas vazias com botão Para Baixo)  
```
= Table.FillDown(#"Colunas Renomeadas",{"Região"})  
```  
- A importância dos tipos de dados  
Funções automáticas em uso (conforme Etapas Aplicadas):  
Tipo Alterado1 (altera tipo de dado em coluna Valor de indefindo - numérico ou texto - para numérico Inteiro; observar barra com sinal vermelho indicando erros de conversao de tipo em linhas da coluna)  
```
= Table.TransformColumnTypes(#"Preenchido Abaixo",{{"Valor", Int64.Type}})  
```
Correção de erro de conversao de tipo: localizar caracteres - (*) - causadores do erro, voltar na etapa anterior (Preenchido Abaixo) para alterar com botão "1->2" de Substituir Valores (desde que os valores estejam alterados adequadamente para texto ou número). Neste caso foi necessário inserir etapa que altera coluna para tipo Texto, depois houve as substituições e mais conferências de dados para trocar, até a barra da coluna ficar completamente verde sem erros.

Valor Substituído
```
= Table.ReplaceValue(#"Tipo Alterado2","(*)","",Replacer.ReplaceText,{"Valor"})  
```
Valor Substituído1  
```  
= Table.ReplaceValue(#"Valor Substituído","(*)","",Replacer.ReplaceText,{"Valor"})  
```  
Valor Subsstituído2 
```
= Table.ReplaceValue(#"Valor Substituído1","(**)","",Replacer.ReplaceText,{"Valor"})  
```
Valor Substituído3  
```
= Table.ReplaceValue(#"Valor Substituído2","(***)","",Replacer.ReplaceText,{"Valor"})  
```
Tipo Alterado1  
```
= Table.TransformColumnTypes(#"Valor Substituído3",{{"Valor", Int64.Type}})  
```
- Juntar dados  
Para juntar dados de outra tabela (População Ano 2019) com mesma estrutura da tabela principal (População por Ano), importa-se a tabela menor pelo ícone Nova Fonte/Excel; confere a linha indicatica de erro na 
coluna e filtra as linhas preenchidas com "null".
Funções automáticas em uso (conforme Etapas Aplicadas): 
Fonte conecta à tabela do Excel
```
= Excel.Workbook(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.4\04_07_Populacao 2019.xlsx"), null, true)  
```  
Navegação (verifica barra indicativa de erro na primeira coluna da tabela)  
```
= Excel.Workbook(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.4\04_07_Populacao 2019.xlsx"), null, true)  
```
Cabeçalhos Promovidos (alteração automática em tabela importada)  
```
= Table.PromoteHeaders(#"População Ano 2019_Sheet", [PromoteAllScalars=true])  
```
Tipo Alterado (devido a mudança de cabeçalho)  
``` 
= Table.TransformColumnTypes(#"Cabeçalhos Promovidos",{{"Unidades da Federação", type text}, {"Região", type text}, {"Publicação", type date}, {"Anos", Int64.Type}, {"Valor", Int64.Type}})  
```  
Linhas Filtradas (para eliminar linhas com null, conforme consulta de erros na barra da coluna)  
```
= Table.SelectRows(#"Tipo Alterado", each ([Unidades da Federação] <> null))  
```
Tipo Alterado1 (muda coluna Anos de Numeral para Texto, assim se igualará à tabela principal)  
```
= Table.TransformColumnTypes(#"Linhas Filtradas",{{"Anos", type text}})  
```
Consulta Acrescentada (junta tabela menor com tabela principal em Página Principa/Combinar/Acrescentar Colunas/Duas Tebelas/seleciona nome da tab/ OK)  
```
= Table.Combine({#"Tipo Alterado1", #"População Ano 2019"})  
```
Linhas Classificadas (aplica na coluna um filtro por ano em ordem descrescente para localizar as linhas de 2019; pode ser excluída pelo X, porque serviu apenas para conferência do acréscimo feito)  
```
= Table.Sort(#"Consulta Acrescentada",{{"Anos", Order.Descending}})  
```  
- Mesclar dados  
Funções automáticas em uso (conforme Etapas Aplicadas):   
Consultas Mescladas (informações de siglas dos estado de outra tabela - Estados e Regiões - são mescladas com a tabela principal, que recebe nova coluna com Table; 
por Página Inicial/Combinar/Mesclar Consultas/selecionar coluna da tab. principal, nome da tab. menor, coluna da tab. menor para mescla, Tipo de Junção Externa Esquerda/OK. Não apagar nenhuma das tabelas de consulta porque estão referenciadas em funções na tab. principal)  
```
= Table.NestedJoin(#"Consulta Acrescentada", {"Unidades da Federação"}, #"Estados e Regiões", {"Estado"}, "Estados e Regiões", JoinKind.LeftOuter)  
```  
Estados e Regiões Expandido (na nova coluna - Estados e Regioes.Sigla - expandor com filtro por Sigla para visualizar os dados mesclados)  
```
= Table.ExpandTableColumn(#"Consultas Mescladas", "Estados e Regiões", {"Sigla"}, {"Estados e Regiões.Sigla"})  
```

- Crie colunas adicionais  
<p align="center">
	<img src="" width="750">
</p>  

Funções automáticas em uso (conforme Etapas Aplicadas):  
Coluna Condicional Adicionada (conforme regra estabelecida para fixação do ano 2019 como ano atual e demais como Passado em nova coluna "Informação Atual")  
```
= Table.AddColumn(#"Estados e Regiões Expandido", "Informação Atual", each if [Anos] = "2019" then "Ano Atuak" else "Passado")  
```  
Linhas Classificadas (coluna Anos clssificada em ordem descrescente para conferir 2019 e a correspondente Informação Atual; pode ser desfeita com X por ser apenas para vizualização dos dados)  
```
= Table.Sort(#"Coluna Condicional Adicionada",{{"Anos", Order.Descending}})  
```  
Coluna Condicional Adicionada (conforme regra estabelecida para cliassificar populações em Acima 10M e Abaixo 10M em nova coluna Grupo de Tamanho)  
```
= Table.AddColumn(#"Coluna Condicional Adicionada", "Grupo de Tamanho", each if [Valor] > 10000000 then "Acima 10M" else "Abaixo 10M")  
```  
Linhas Filtradas (confere linhas classificadas como Abaixo 10M; pode apagar depois da visualização)  
```
= Table.SelectRows(#"Coluna Condicional Adicionada1", each ([Grupo de Tamanho] = "Abaixo 10M"))  
```

- Referencia e duplique tabelas  
Tabela duplicada permanece com todas as etapas aplicadas da tabela original, é uma nova consulta que referenciou a todos os passos ou a todas as transformações realizadas de uma forma independente, sem fazer nenhuma referência à consulta. Enquanto que a tabela gerada por Referência apresenta só etapa de Fonte mas contém todas as alterações da original, fica marcada como igual à primeira. Duplicar é mais pesado na performance do Power Query, já a Referência aproveita todas as etapas da consulta referenciada. Foi excluída a tabela duplicada e mantida a referenciada.   

Função automática em uso (conforme Etapas Aplicadas):   
Fonte conecta como referência de outra tabela existente
```
= #"População por Ano"  
```  
- Agrupe dados no Power Query   
<p align="center">
	<img src="" width="750">
</p>  

Funções automáticas em uso (conforme Etapas Aplicadas):  
Linhas Filtradas (por ano 2019)  
```
= Table.SelectRows(Fonte, each ([Anos] = "2019"))  
```
Linhas Agrupadas (conforme regra por Região e População)  
```
= Table.Group(#"Linhas Filtradas", {"Região"}, {{"População", each List.Sum([Valor]), type nullable number}})   
```  
Fonte conectada à duplicação de tabela referenciada  
```
= #"População por Ano"  
```  
Linhas Filtradas (por ano 2019 como na tab. de origem)  
```
= Table.SelectRows(Fonte, each ([Anos] = "2019"))  
```  
Regra criada pela engrenagem ao lado da etapa Linhas Filtradas
<p align="center">
	<img src="" width="750">
</p>  

Linhas Agrupadas (conforme regra por Grupo de Tamanho e Qtde de Estados)  
```
= Table.Group(#"Linhas Filtradas", {"Grupo de Tamanho"}, {{"Qtde de Estados", each Table.RowCount(_), Int64.Type}})  
```  
- Modifique o endereço de uma fonte de dados
<p align="center">
	<img src="" width="750">
</p>  


☑️ **5. Relacionando dados**  
- Compreenda a cardinalidade dos dados 
Na modelagem de dados, CARDINALIDADE significa o grau de relação entre colunas e tabelas.  
<p align="center">
	<img src="" width="750">
</p>  

- Explore os tipos de tabelas e colunas do modelo  
Conceitos de tabela fato, tabela dimensão ou cadastro, chave primária e chave estrangeira foram demonstrados através das tabelas que compõem a base de dados [AdventureWorks]() em Access.  
- Compreenda o  motivo de tabelas dimensão e fato  
Diferença entre relatórios e modelo de dados
Relatórios | Modelos de Dados
-|-
Servem para consulta rápida; tem todas as descrições dos campos e possibilitam fazer uma tabela dinâmica usando apenas um conjunto de dados. | No Power BI podemos relacionar tabelas separadas e usar seus campos de modo performático. É possível usar relatórios dentro do Power BI sem explorar suas capacidades.  
- Estabelecendo relacionamento no Power BI  
<p align="center">
	<img src="" width="750">
</p>  

☑️ **6. Introdução à Linguagem DAX**  
- Introdução ao DAX  
Linguagem DAX é acrônimo para _Data Analysis Expressions_ (em português, expressões de análises de dados), que é uma linguagem utilizada no Power BI para cálculos.  
<p align="center">
	<img src="" width="750">
</p>  

- Utilize funções de agregação  
Funções DAX em uso:
Cálculo do total de vendas com SUM
```
Soma Vendas = SUM('Pedidos Detalhes'[Total])   
```
Cálculo do total da meta com SUM  
```
Soma Meta = SUM(Meta[Meta])  
```  

Cálculo da média de vendas com AVERAGE
```
Media Vendas = AVERAGE('Pedidos Detalhes'[Total])  
```  
- Compreenda a lógica de cálculo de funções DAX  
<p align="center">
	<img src="" width="750">
</p>   

- Criando uma coluna calculda  
MEDIDAS não criam COLUNAS, são utilizadas apenas dentro de visuais. Colunas criadas com DAX não podem ser visualizadas no Power Query porque foram criadas utilizando funções DAX que não podem ser processadas no Power Query.  
Funções DAX em uso:
Cálculo de desconto aplicado em preço unitário com multiplicação de SUM das colunas da tabela - nova medida calculada "Valor Desconto" para usar em um visual, pois não tem contexto embora esteja armazenada dentro de uma tabela.
```
Valor Desconto = SUM('Pedidos Detalhes'[Preço Unitário]) * SUM('Pedidos Detalhes'[Desconto])  
```
Cálculo de desconto aplicado em preço unitário com multiplicação direta entre linhas filtradas da tabela - nova coluna calculada "Valor Desconto2" entra na tabela, por ter um contexto de linha.
```
Valor Desconto2 = 'Pedidos Detalhes'[Preço Unitário] * 'Pedidos Detalhes'[Desconto]  
```  
- Realize uma divisão segura com a DIVIDE  
Funções DAX em uso:
Cálculo da relação entre as somas de vendas e de meta anual com DIVIDE - nova medida calculada  
```  
Vendas vs Meta = DIVIDE([Soma Vendas],[Soma Meta],BLANK())  
```
Cálculo do percentual da relação Vendas vs Meta com reaproveitamento da medida anterior na nova medida calculada(só houve acréscimo de -1 na função DAX)  
```  
Vendas vs Meta = DIVIDE([Soma Vendas],[Soma Meta],BLANK())-1  
```  
Com o reaproveitamento da medida obtém-se um resultado mais significativo para a análise dos dados.  
- Introdução à função CALCULATE  
Funções DAX em uso:  
Cálculo do percentual da categoria Componentes (filtro) comparado a outras categorias na soma de vendas com CALCULATE - nova medida calculada  
```
Vendas Componentes = CALCULATE([Soma Vendas],'Produtos Categorias'[Nome Categoria]="Componentes")  
```  
Foi feita uma divisão ente valores de linhas da tabela, depois de inseri-los em mesma linha com CALCULATE que alterou o contexto natural do filtro de linhas, para obter a comparação de percentuais entre as categorias.  
```
Comparação Componentes = DIVIDE([Soma Vendas],[Vendas Componentes],BLANK())  
```  
- Função ALL e ALLSELECTED  
Funções DAX em uso:
Inserir total de vendas na tabela para incluir todas as linhas com CALCULATE e ALL (remove todos os filtros int e ext do visual) - nova medida calculada 
```
Todas as Vendas = CALCULATE([Soma Vendas],ALL('Pedidos Detalhes'))  
```
Cálculo do percentual de cada categoria sobre o total de vendas com DIVIDE - nova medida calculada  
```
Repres. Categorias = DIVIDE([Soma Vendas],[Todas as Vendas])   
```  
Inserir todas as vendas selecionadas por país específico (filtro externo) para incluir todas as linhas com CALCULATE e ALLSELECTED (remove filtros int da consulta e inclui ext ao visual) - nova medida calculada  
```
Todas Selecionadas = CALCULATE([Soma Vendas],ALLSELECTED('Pedidos Detalhes'))  
```  
Cálculo do percentual de cada categoria por país sobre a soma de vendas das categorias com DIVIDE - nova medida calculada  
```  
Repres. Categorias Selecionadas = DIVIDE([Soma Vendas],[Todas Selecionadas])  
```  

☑️ **7. Cálculos avançados com DAX**  
- Introdução às funções iterantes  
Função DAX em uso:  
Substituir coluna calculada por uma medida calculada (tem menos custo computacional) com SUMX, assim há modificação do contexto de filtro. Em SUMX a medida cria um cálculo diferente considerando todas as linhas do cocntexto inserido. Sempre que uma função pede uma tabela como argumento é iterante.
```
Valor Desconto 3 = SUMX('Pedidos Detalhes','Pedidos Detalhes'[Preço Unitário]*'Pedidos Detalhes'[Desconto])  
```  
- Crie tabelas de parâmetros  
Fazer uma tabela de parâmetro, criar uma variação de custo e descobrir seu lucro a partir da variação inserida no parâmetro. 
Funções DAX em uso:
Cria-se um contexto de filtro, observando cada linha da tabela Pedidos Detalhes e cada quantidade é multiplicada pelos custos relacionados na tabela Produtos, na coluna Custo Padrão, obtém-se Soma Custo com SUMX e RELATED
```
Soma Custo = SUMX('Pedidos Detalhes', 'Pedidos Detalhes'[Quantidade]*RELATED(Produtos[Custo Padrão]))  
```  
Cálculo do lucro  
``` 
Lucro = [Soma Vendas]-[Soma Custo]  
```  
Tabela de parâmetro para criar a variação que é aplicada em Soma Custo para calcular o Lucro de acordo com o cenário escolhido pelos usuários do relatório  
```
Parâmetro = GENERATESERIES(0.01, 0.09, 0.001)  
```  
Medida Parametro Valor criada automaticamente junto com Parâmetro  
```
Parâmetro Valor = SELECTEDVALUE('Parâmetro'[Parâmetro], 0)  
```  
- Como criar medidas dinâmicas  
Funcões DAX em uso:
Cálculo do custo de variação, somando Soma Custo com multiplicação entre Soma Custo e Parâmetro Valor
```
Soma Custo Variação = Produtos[Soma Custo] + Produtos[Soma Custo]*'Parâmetro'[Parâmetro Valor]  
```  
Aplicável em simulações de novos investimentos com aumento do custo em 5,80%, em que é avalido o cenário daqui, se compensa ou não aumentar o custo em 5,80% para ter o lucro calculado na tabela que aponta para a soma de custos.  
Cálculo de Lucro Variação  
```
Lucro Variação = [Soma Vendas]-Produtos[Soma Custo Variação]  
```  
Para as categorias que apresentam valores negativos é recomendado ajuste do investimento para que todas gerem lucro.  
- Calcule o ano anterior com a SAMEPERIODLASTYEAR  

- Calcule o mês anterior com a DATEADD  
- Acumule valores com funções de TOTALYDT, QTD, e MTD  

Exemplos de:  
- [XXXX]().  
- [XXX]().  
- [XXXX]().  


☑️ **8. Organizando os visuais e compartilhando o projeto**  
- Organização e publicação do relatório  
- Formas de consumo de dados no Power BI  

Exemplo...  
<p align="center">
	<img src="" width="750">
</p>  


☑️ **Conclusão**  
Próximos passos para explorar seus conhecimentos e continuar aprendendo

---

#### ✍️ AUTORA  
Carla Edila Silveira  
Contato: rosa.carla@pucpr.edu.br  

---

#### ©️ LICENÇA

[MIT](https://choosealicense.com/licenses/mit/)  

---  

#### 🔗 LINKS ÚTEIS  

[[DATAB Live] Linguagem M - Avançado de Verdade](https://www.youtube.com/watch?v=vYb-89PZf7U)  
[LINGUAGEM DAX: TUDO PARA COMEÇAR A USAR DO JEITO CERTO](https://educaenter.com/aprenda-usar-a-linguagem-dax/)  
[Linguagem de fórmula Power Query M](https://docs.microsoft.com/pt-br/powerquery-m/)
[Power BI: Linguagens M e DAX](https://www.eng.com.br/artigo.cfm?id=7506&post=power-bi-linguagens-m-e-dax)  
[Referência de DAX (Data Analysis Expressions)](https://docs.microsoft.com/pt-br/dax/)  
[RLS (segurança em nível de linha) com o Power BI](https://docs.microsoft.com/pt-br/power-bi/enterprise/service-admin-rls)  


---
