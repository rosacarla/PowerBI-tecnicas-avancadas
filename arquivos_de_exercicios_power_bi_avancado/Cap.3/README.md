#### # Como importar dados do Excel e funções da linguagem M (Power Query) 
Funções automáticas DAX em uso (conforme Etapas Aplicadas):  

* Fonte conecta a arquivo Excel (escolher opção Tabela (ícone azul) para importar.  
Não usar Planilha para evitar importação duplicada, pois tabelas são intervalos delimitados com cabeçalhos e tipos de dados definidos)
``` 
= Excel.Workbook(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.3\03_02_Clientes.xlsx"), null, true)  
```  

* Tipo alterado 
``` 
= Table.TransformColumnTypes(DadosClientes_Table,{{"ID Cliente", Int64.Type}, {"Cliente", type text}, {"CEP", type text}, {"Data Pedido", type date}})
``` 

---  

#### # Como importar dados de CSV e TXT 
Funções automáticas DAX em uso (conforme Etapas Aplicadas):  

* Fonte conecta a arquivo CSV e TXT  
```
= Csv.Document(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.3\03_03_Taxa Selic.txt"),[Delimiter=";", Columns=11, Encoding=65001, QuoteStyle=QuoteStyle.None])  
```
Exemplo de configuração da função Csv.Document (sintaxe do Power Query)  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/configuracao-funcao-fonte-csv.png" width="750">
</p>  

* Tipo Alterado
```
= Table.TransformColumnTypes(Fonte,{{"Column1", type text}, {"Column2", type text}, {"Column3", type text}, {"Column4", type text}, {"Column5", type text}, {"Column6", type text}, {"Column7", type text}, {"Column8", type text}, {"Column9", type text}, {"Column10", type text}, {"Column11", type text}})  
```  

---  

#### # Como importar dados da pasta
Funções automáticas DAX em uso (conforme Etapas Aplicadas):  

* Fonte conecta a uma Pasta do Windows (arquivos inicialmente importados como conteúdo binário; todas as importações de arquivo para o Power BI ficam dessa forma)
```
= Folder.Files("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.3\03_04_Pedidos")  
```  
* Outras Colunas Removidas (Remover Outras Colunas selecionado com botão direito pelo cabeçalho de uma coluna; removidas colunas com informações irrelevantes de configuração)
```
= Table.SelectColumns(Fonte,{"Content"})  
```
* Personalização Adicionada (aba Adicionar Coluna/Coluna Personalizada; "Excel.Workbook" transforma pasta de trabalho de conteúdo Binary para objeto Table e adiciona a coluna Personalizar) 
```
= Table.AddColumn(#"Outras Colunas Removidas", "Personalizar", each Excel.Workbook([Content]))  
```
* Colunas Removidas (Remover selecionado com botão direito pelo cabeçalho - Content - da coluna a excluir)  
```
= Table.RemoveColumns(#"Personalização Adicionada",{"Content"})  
```  
* Personalizar Expandido (clicar no botão Expandir dentro da coluna Personalizar, desmarcar "Use nome da coluna original como prefixo" para criar colunas da tabela com seus nomes originais sem copiar junto o "Personalizar" da coluna expandida)  
```
= Table.ExpandTableColumn(#"Colunas Removidas", "Personalizar", {"Name", "Data", "Item", "Kind", "Hidden"}, {"Name", "Data", "Item", "Kind", "Hidden"})  
```  
* Linhas Filtradas (por tipo tabela)  
```
= Table.SelectRows(#"Personalizar Expandido", each ([Kind] = "Table"))  
```
* Outras Colunas Removidas1 (Remover Outras Colunas selecionado com botão direito pelo cabeçalho da coluna Data para permanecer só com esta coluna)  
```
= Table.SelectColumns(#"Linhas Filtradas",{"Data"})  
```
* Data (depois de clicar em Expandir, visualiza abertura da coluna - pasta importada - composta por 5 linhas - arquivos - contendo 1 tabela em cada; seleciona uma linha da coluna para expandir informações da tabela correspondente)  
```
= #"Outras Colunas Removidas1"{0}[Data]  
```  
* Data Expandido (clicar no botão Expandir dentro da coluna Data sem prefixo marcado para expansão de todas as tabelas, visualiza-se todas as informações dos 5 arquivos em reunidas em uma tabela)  
```
= Table.ExpandTableColumn(#"Outras Colunas Removidas1", "Data", {"Pedido", "Cód. Cliente", "Data Pedido", "Data Faturamento", "Cód. Item", "Quantidade", "Pais"}, {"Pedido", "Cód. Cliente", "Data Pedido", "Data Faturamento", "Cód. Item", "Quantidade", "Pais"})  
```  

--- 

#### # Como importar dados de fontes da Web utilizando tabelas
Funções automáticas DAX em uso (conforme Etapas Aplicadas):  
* Fonte conecta a conteúdo da Web em tabela  
```
= Web.BrowserContents("https://pt.wikipedia.org/wiki/Lista_de_pa%C3%ADses_por_popula%C3%A7%C3%A3o")  
```  
* Tabela Extraída do HTML  
```
= Html.Table(Fonte, {{"Column1", "TABLE.wikitable.sortable.jquery-tablesorter > * > TR > :nth-child(1)"}, {"Column2", "TABLE.wikitable.sortable.jquery-tablesorter > * > TR > :nth-child(2)"}, {"Column3", "TABLE.wikitable.sortable.jquery-tablesorter > * > TR > :nth-child(3)"}, {"Column4", "TABLE.wikitable.sortable.jquery-tablesorter > * > TR > :nth-child(4)"}, {"Column5", "TABLE.wikitable.sortable.jquery-tablesorter > * > TR > :nth-child(5)"}}, [RowSelector="TABLE.wikitable.sortable.jquery-tablesorter > * > TR"])  
```
* Cabeçalhos Promovidos  
```
= Table.PromoteHeaders(#"Tabela extraída de HTML", [PromoteAllScalars=true])  
```
* Tipo Alterado  
```
= Table.TransformColumnTypes(#"Cabeçalhos Promovidos",{{"Posição", type text}, {"País (ou território dependente)", type text}, {"Estimativa da ONU", type text}, {"Data", Int64.Type}, {"Estimativa Oficial", type text}})  
```

---  

#### # Como importar dados de fontes da Web utilizando exemplos  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/importa-web-exemplos.png" width="750">
</p>  

Funções automáticas DAX em uso (conforme Etapas Aplicadas):  

* Fonte conecta a conteúdo da Web
```
= Web.BrowserContents("https://www.ibge.gov.br/")  
```
* Tabela extraída de HTML  
```
= Html.Table(Fonte, {{"Column1", ".indicador-title"}, {"Column2", ".indicador-value"}, {"Column3", ".indicador-text"}, {"Column4", "SMALL"}, {"Column5", ".dado-periodo"}}, [RowSelector=".indicadores-list A"])  
```
* Tipo Alterado
```
= Table.TransformColumnTypes(#"Tabela extraída de HTML",{{"Column1", type text}, {"Column2", Percentage.Type}, {"Column3", type text}, {"Column4", type text}, {"Column5", type text}})  
```  

---   
