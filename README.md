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
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/processo-bi.png" width="380">
</p>

- Apresentação dos arquivos e projeto do curso  
[<<< Arquivos de exercícios >>>](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/tree/main/arquivos_de_exercicios_power_bi_avancado)    
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/arq-projeto.png" width="380">
</p>  


☑️ **2. Conhecendo o ecossistema do Power BI**   
- Compreenda as diferentes plataformas da Microsoft para análise de dados  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/plataformas-desenvolvimento.png" width="750">
</p>  

- Conheça outros softwares de Business Intelligence  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/outros-softwares-bi.png" width="500">
</p> 


☑️ **3. Importação de dados**  
- Conheça os diferentes tipos de dados  
Exemplo de funcionalidade: ODBC (conector universal de dados)  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/conector-universal-dados.png" width="500">
</p>   

- [Como importar dados do Excel e funções da linguagem M (Power Query)](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/arquivos_de_exercicios_power_bi_avancado/Cap.3)  
- [Como importar dados de CSV e TXT](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/arquivos_de_exercicios_power_bi_avancado/Cap.3)  
- [Como importar dados da pasta](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/arquivos_de_exercicios_power_bi_avancado/Cap.3)  
- Como importar dados do SQL Server  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/importa-sql-server.png" width="500">
</p>   

Importa do SQL Server com filtro  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/importa-sqlserver-comfiltro.png" width="750">
</p>  

- [Como importar dados de fontes da Web utilizando tabelas](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/arquivos_de_exercicios_power_bi_avancado/Cap.3)  
- [Como importar dados de fontes da Web utilizando exemplos](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/arquivos_de_exercicios_power_bi_avancado/Cap.3) 


☑️ **4. Tratamento de dados importados**  
- Apresentação da linguagem M  

Linguagem M | Linguagem DAX  
-|-
Realizada por etapas; editor avançado (guia Exibição) agrupa funções por etapas. | Utilizadas para criar cálculos e medidas.
Funções são escritas em inglês e argumentos separados por vírgula.| Pode ser acessada somente dentro do Power BI.
Presente apenas dentro do Power Query. | Não é possível utilizar funções DAX dentro do Power Query.  

- Introdução ao editor de consultas avançado  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/editor-avancado.png" width="500">
</p>  

- [Limpar dados indesejados](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/tree/main/arquivos_de_exercicios_power_bi_avancado/Cap.4%20Renomeado)  
- [Transforme colunas em linhas](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/tree/main/arquivos_de_exercicios_power_bi_avancado/Cap.4%20Renomeado)  
- Utilize o preenchimento para cima e para baixo  
Função automática DAX em uso (conforme Etapas Aplicadas):  
Preenchido Abaixo (preenche linhas vazias com botão Para Baixo)  
```
= Table.FillDown(#"Colunas Renomeadas",{"Região"})  
```  
- [A importância dos tipos de dados](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/tree/main/arquivos_de_exercicios_power_bi_avancado/Cap.4%20Renomeado)  
- [Juntar dados](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/tree/main/arquivos_de_exercicios_power_bi_avancado/Cap.4%20Renomeado)  
- [Mesclar dados](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/tree/main/arquivos_de_exercicios_power_bi_avancado/Cap.4%20Renomeado)  
- [Crie colunas adicionais](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/tree/main/arquivos_de_exercicios_power_bi_avancado/Cap.4%20Renomeado)  
- [Referencia e duplique tabelas](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/tree/main/arquivos_de_exercicios_power_bi_avancado/Cap.4%20Renomeado)  
- [Agrupe dados no Power Query](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/tree/main/arquivos_de_exercicios_power_bi_avancado/Cap.4%20Renomeado)   
- Modifique o endereço de uma fonte de dados
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/modifica-endereco-fonte.png" width="880">
</p>  


☑️ **5. Relacionando dados**  
- Compreenda a cardinalidade dos dados 
Na modelagem de dados, CARDINALIDADE significa o grau de relação entre colunas e tabelas.  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/cardinalidade-dados.png" width="880">
</p>  

- Explore os tipos de tabelas e colunas do modelo  
Conceitos de tabela fato, tabela dimensão ou cadastro, chave primária e chave estrangeira foram demonstrados através das tabelas que compõem a base de dados [AdventureWorks](https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/arquivos_de_exercicios_power_bi_avancado/Cap.5/AdventureWorks.accdb) em Access.   
- Compreenda o  motivo de tabelas dimensão e fato  
Diferença entre relatórios e modelo de dados  

Relatórios | Modelos de Dados
-|-
Servem para consulta rápida; tem todas as descrições dos campos e possibilitam fazer uma tabela dinâmica usando apenas um conjunto de dados. | No Power BI podemos relacionar tabelas separadas e usar seus campos de modo performático. É possível usar relatórios dentro do Power BI sem explorar suas capacidades.  
- Estabelecendo relacionamento no Power BI  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/relacionamenos-adventure.png" width="750">
</p>  

☑️ **6. Introdução à Linguagem DAX**  
- Introdução ao DAX  
Linguagem DAX é acrônimo para _Data Analysis Expressions_ (em português, expressões de análises de dados), que é uma linguagem utilizada no Power BI para cálculos.  
<p align="center">
	<img src="https://github.com/rosacarla/PowerBI-tecnicas-avancadas/blob/main/images/dax-funcoes-sintaxe.png" width="880">
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
Função DAX em uso:  
Exibe vendas do ano anterior ao lado da coluna dos meses do ano atual com CALCULATE que muda o contexto de filtro e SAMEPERIODLASYEAR que filtra os dados. 
```
Vendas Ano Anterior = CALCULATE([Soma Vendas],SAMEPERIODLASTYEAR('Calendário'[Data]))  
```  
- Calcule o mês anterior com DATEADD  
DATEADD desloca um período conforme os argumentos inseridos nessa função, com CALCULATE o contexto de filtro é mudado e o mês anterior é trazido para outra coluna da tabela. No exemplo comparam-se as performances de vendas de mês atual e mês anterior, por isso é acrescentado -1 como argumento do intervalo filtrado.  
```  
Vendas Mes Passado = CALCULATE([Soma Vendas],DATEADD('Calendário'[Data],-1,MONTH))
```  
- Acumule valores com funções de TOTALYDT, QTD, e MTD  
TOTALYTD acumula valores conforme o contexto de filtro atual. Sigla YTD significa Year To Date.
Funções DAX em uso:
Mostra acumulado de valores até o final do ano com CALCULATE e TOTALYTD, que recomeça a contagem a cada mudança de ano. 
```  
Acumulado Year To Date 2 = TOTALYTD([Soma Vendas],'Calendário'[Data])   
```  
Mostra acumulado de valores por trimestre do ano com CALCULATE e TOTALQTD, que recomeça a contagem ao mudar de ano.  
``` 
Acumulado Year To Date Quarter = TOTALQTD([Soma Vendas],'Calendário'[Data])   
```  

☑️ **8. Organizando os visuais e compartilhando o projeto**  
- Organização e publicação do relatório  
Visualização do relatório Adventure_Report na [web](https://app.powerbi.com/reportEmbed?reportId=6fcd1e60-7567-480d-be1d-fac0cd7e1157&autoAuth=true&ctid=8a1ef6c3-8324-4103-bf4a-1328c5dc3653&config=eyJjbHVzdGVyVXJsIjoiaHR0cHM6Ly93YWJpLXNvdXRoLWNlbnRyYWwtdXMtcmVkaXJlY3QuYW5hbHlzaXMud2luZG93cy5uZXQvIn0%3D). 

- Formas de consumo de dados no Power BI  
 Versão do relatório Adventure_Report em Dashboard  
   
<p align="center">
	<img src="" width="750">
</p>  


☑️ **Conclusão**  
Próximos passos para explorar seus conhecimentos e continuar aprendendo
Leitura sobre atualizações mensais do Power BI no site oficial, sobretudo na seção do blog: https://powerbi.microsoft.com/pt-br/blog/.  

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
