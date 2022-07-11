### Como importar dados de CSV e TXT

Funções automáticas DAX em uso (conforme Etapas Aplicadas):  

* Fonte conecta a arquivo CSV e TXT  
```
= Csv.Document(File.Contents("C:\Users\carla\Área de Trabalho\meu-github\PowerBI-tecnicas-avancadas\arquivos_de_exercicios_power_bi_avancado\Cap.3\03_03_Taxa Selic.txt"),[Delimiter=";", Columns=11, Encoding=65001, QuoteStyle=QuoteStyle.None])  
```
Exemplo de configuração da função Csv.Document (sintaxe do Power Query)  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/configuracao-funcao-fonte-csv.png" width="500">
</p>  

* Tipo Alterado
```
= Table.TransformColumnTypes(Fonte,{{"Column1", type text}, {"Column2", type text}, {"Column3", type text}, {"Column4", type text}, {"Column5", type text}, {"Column6", type text}, {"Column7", type text}, {"Column8", type text}, {"Column9", type text}, {"Column10", type text}, {"Column11", type text}})  
```  