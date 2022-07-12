#### # Limpar dados indesejados  
Funções automáticas dax em uso (conforme Etapas Aplicadas):  

* Fonte conecta a arquivo Excel  
```
= Excel.Workbook(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.4\04_03_Populacao 2001 a 2018.xlsx"), null, true)  
```  
* Navegação (por pela aba da tabela População por Ano)  
```
= Fonte{[Item="População por Ano",Kind="Sheet"]}[Data]  
``` 
* Linhas Principais Removidas (remoção das 3 primeiras linhas da tabela com texto irrelevante no cabeçalho, feita por Página Inicial/Remover linhas)  
```
= Table.Skip(#"População por Ano_Sheet",3)  
```  
* Cabeçalhos Promovidos (clicar no ícone azul de tabela, opção "Usar Primeira Linha como Cabeçalho")  
```
= Table.PromoteHeaders(#"Linhas Principais Removidas", [PromoteAllScalars=true])  
```
* Tipos Alterados (alteração automática de tipos após promoção de cabeçalho)  
```
= Table.TransformColumnTypes(#"Cabeçalhos Promovidos",{{"Unidades da Federação", type text}, {"Região", type text}, {"Publicação", type date}, {"2001", Int64.Type}, {"2002", Int64.Type}, {"2003", Int64.Type}, {"2004", Int64.Type}, {"2005", Int64.Type}, {"2006", Int64.Type}, {"2007", Int64.Type}, {"2008", Int64.Type}, {"2009", Int64.Type}, {"2010", Int64.Type}, {"2011", Int64.Type}, {"2012", Int64.Type}, {"2013", Int64.Type}, {"2014", Int64.Type}, {"2015", Int64.Type}, {"2016", Int64.Type}, {"2017", Int64.Type}, {"2018", type any}})  
```
* Linhas Filtradas (filtro de linhas da tabela preenchidas com "null", selecionadas na seta para baixo pelo cabeçalho da coluna)  
```
= Table.SelectRows(#"Tipo Alterado", each ([Unidades da Federação] <> null))  
```  

---  

#### # Transforme colunas em linhas  
Funções automáticas DAX em uso (conforme Etapas Aplicadas):  

* Colunas Não Dinâmicas (colunas dos Anos tem os valores transpostos para linhas e acrescentadas as colunas Atributo (anos) e Valor (valores de cada ano); tabela transformada com apenas 5 colunas)
```
= Table.UnpivotOtherColumns(#"Linhas Filtradas", {"Unidades da Federação", "Região", "Publicação"}, "Atributo", "Valor")  
```
* Colunas Renomeadas (coluna Atributo renoneada como Anos)
```
= Table.RenameColumns(#"Colunas Não Dinâmicas",{{"Atributo", "Anos"}})  
```  

---  

#### # Utilize o preenchimento para cima e para baixo  
Função automática DAX em uso (conforme Etapas Aplicadas):  
Preenchido Abaixo (preenche linhas vazias com botão Para Baixo)  
```  
= Table.FillDown(#"Colunas Renomeadas",{"Região"})  
```  

---  


#### # A importância dos tipos de dados  
Funções automáticas DAX em uso (conforme Etapas Aplicadas):  

* Tipo Alterado1 (altera tipo de dado em coluna Valor de indefindo - numérico ou texto - para numérico Inteiro; observar barra com sinal vermelho indicando erros de conversao de tipo em linhas da coluna)  
```
= Table.TransformColumnTypes(#"Preenchido Abaixo",{{"Valor", Int64.Type}})  
```
<p align="justify">
Correção de erro de conversao de tipo: localizar caracteres - (*) - causadores do erro, voltar na etapa anterior (Preenchido Abaixo) para alterar com botão
"1->2" de Substituir Valores (desde que os valores estejam alterados adequadamente para texto ou número). Neste caso foi necessário inserir etapa que altera
coluna para tipo Texto, depois houve as substituições e mais conferências de dados para trocar, até a barra da coluna ficar completamente verde sem erros.
</p>

* Valor Substituído
```
= Table.ReplaceValue(#"Tipo Alterado2","(*)","",Replacer.ReplaceText,{"Valor"})  
```
* Valor Substituído1  
```  
= Table.ReplaceValue(#"Valor Substituído","(*)","",Replacer.ReplaceText,{"Valor"})  
```  
* Valor Substituído2 
```
= Table.ReplaceValue(#"Valor Substituído1","(**)","",Replacer.ReplaceText,{"Valor"})  
```
* Valor Substituído3  
```
= Table.ReplaceValue(#"Valor Substituído2","(***)","",Replacer.ReplaceText,{"Valor"})  
```
* Tipo Alterado1  
```
= Table.TransformColumnTypes(#"Valor Substituído3",{{"Valor", Int64.Type}})  
```  

---  

#### # Juntar dados  
<p align="justify">
Para juntar dados de outra tabela (População Ano 2019) com mesma estrutura da tabela principal (População por Ano), importa-se a tabela menor pelo ícone Nova Fonte/Excel; confere a linha indicatica de erro na 
coluna e filtra as linhas preenchidas com "null".  
</p>  

Funções automáticas DAX em uso (conforme Etapas Aplicadas):  

* Fonte conecta à tabela do Excel
```
= Excel.Workbook(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.4\04_07_Populacao 2019.xlsx"), null, true)  
```  
* Navegação (verifica barra indicativa de erro na primeira coluna da tabela)  
```
= Excel.Workbook(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.4\04_07_Populacao 2019.xlsx"), null, true)  
```
* Cabeçalhos Promovidos (alteração automática em tabela importada)  
```
= Table.PromoteHeaders(#"População Ano 2019_Sheet", [PromoteAllScalars=true])  
```
* Tipo Alterado (devido a mudança de cabeçalho)  
``` 
= Table.TransformColumnTypes(#"Cabeçalhos Promovidos",{{"Unidades da Federação", type text}, {"Região", type text}, {"Publicação", type date}, {"Anos", Int64.Type}, {"Valor", Int64.Type}})  
```  
* Linhas Filtradas (para eliminar linhas com null, conforme consulta de erros na barra da coluna)  
```
= Table.SelectRows(#"Tipo Alterado", each ([Unidades da Federação] <> null))  
```
* Tipo Alterado1 (muda coluna Anos de Numeral para Texto, assim se igualará à tabela principal)  
```
= Table.TransformColumnTypes(#"Linhas Filtradas",{{"Anos", type text}})  
```
* Consulta Acrescentada (junta tabela menor com tabela principal em Página Principa/Combinar/Acrescentar Colunas/Duas Tebelas/seleciona nome da tab/ OK)  
```
= Table.Combine({#"Tipo Alterado1", #"População Ano 2019"})  
```
* Linhas Classificadas (aplica na coluna um filtro por ano em ordem descrescente para localizar as linhas de 2019; pode ser excluída pelo X, porque serviu apenas para conferência do acréscimo feito)  
```
= Table.Sort(#"Consulta Acrescentada",{{"Anos", Order.Descending}})  
```   

---  

#### # Mesclar dados  
Funções automáticas DAX em uso (conforme Etapas Aplicadas):   

* Consultas Mescladas (informações de siglas dos estado de outra tabela - Estados e Regiões - são mescladas com a tabela principal, que recebe nova coluna com Table; 
por Página Inicial/Combinar/Mesclar Consultas/selecionar coluna da tab. principal, nome da tab. menor, coluna da tab. menor para mescla, Tipo de Junção Externa Esquerda/OK. Não apagar nenhuma das tabelas de consulta porque estão referenciadas em funções na tab. principal)  
```
= Table.NestedJoin(#"Consulta Acrescentada", {"Unidades da Federação"}, #"Estados e Regiões", {"Estado"}, "Estados e Regiões", JoinKind.LeftOuter)  
```  
* Estados e Regiões Expandido (na nova coluna - Estados e Regioes.Sigla - expandor com filtro por Sigla para visualizar os dados mesclados)  
```
= Table.ExpandTableColumn(#"Consultas Mescladas", "Estados e Regiões", {"Sigla"}, {"Estados e Regiões.Sigla"})  
```  

---  

#### # Crie colunas adicionais  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/coluna-condicional.png" width="750">
</p>  

Funções automáticas DAX em uso (conforme Etapas Aplicadas):  

* Coluna Condicional Adicionada (conforme regra estabelecida para fixação do ano 2019 como ano atual e demais como Passado em nova coluna "Informação Atual")  
```
= Table.AddColumn(#"Estados e Regiões Expandido", "Informação Atual", each if [Anos] = "2019" then "Ano Atuak" else "Passado")  
```  
* Linhas Classificadas (coluna Anos clssificada em ordem descrescente para conferir 2019 e a correspondente Informação Atual; pode ser desfeita com X por ser apenas para vizualização dos dados)  
```
= Table.Sort(#"Coluna Condicional Adicionada",{{"Anos", Order.Descending}})  
```  
* Coluna Condicional Adicionada (conforme regra estabelecida para cliassificar populações em Acima 10M e Abaixo 10M em nova coluna Grupo de Tamanho)  
```
= Table.AddColumn(#"Coluna Condicional Adicionada", "Grupo de Tamanho", each if [Valor] > 10000000 then "Acima 10M" else "Abaixo 10M")  
```  
* Linhas Filtradas (confere linhas classificadas como Abaixo 10M; pode apagar depois da visualização)  
```
= Table.SelectRows(#"Coluna Condicional Adicionada1", each ([Grupo de Tamanho] = "Abaixo 10M"))  
```  

---  

#### # Referencie e duplique tabelas  
<p align="justify">  
Tabela duplicada permanece com todas as etapas aplicadas da tabela original, é uma nova consulta que referenciou a todos os passos ou a todas as 
transformações realizadas de uma forma independente, sem fazer nenhuma referência à consulta. Enquanto que a tabela gerada por Referência apresenta 
só etapa de Fonte mas contém todas as alterações da original, fica marcada como igual à primeira. Duplicar é mais pesado na performance do Power
Query, já a Referência aproveita todas as etapas da consulta referenciada. Foi excluída a tabela duplicada e mantida a referenciada.  
</p>  

Função automática DAX em uso (conforme Etapas Aplicadas):  

* Fonte conecta como referência de outra tabela existente
```
= #"População por Ano"  
```  

---  

#### # Agrupe dados no Power Query  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/agrupa-power-query.png" width="750">
</p>  

Funções automáticas em uso (conforme Etapas Aplicadas):  

* Linhas Filtradas (por ano 2019)  
```
= Table.SelectRows(Fonte, each ([Anos] = "2019"))  
```
* Linhas Agrupadas (conforme regra por Região e População)  
```
= Table.Group(#"Linhas Filtradas", {"Região"}, {{"População", each List.Sum([Valor]), type nullable number}})   
```  
* Fonte conectada à duplicação de tabela referenciada  
```
= #"População por Ano"  
```  
* Linhas Filtradas (por ano 2019 como na tab. de origem)  
```
= Table.SelectRows(Fonte, each ([Anos] = "2019"))  
```  
Regra criada pela engrenagem ao lado da etapa Linhas Filtradas
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/agrupa-contar-linhas.png" width="600">
</p>  

* Linhas Agrupadas (conforme regra por Grupo de Tamanho e Qtde de Estados)  
```
= Table.Group(#"Linhas Filtradas", {"Grupo de Tamanho"}, {{"Qtde de Estados", each Table.RowCount(_), Int64.Type}})  
```  

---  
