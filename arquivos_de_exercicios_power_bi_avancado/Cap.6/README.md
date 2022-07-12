#### # Utilize funções de agregração  
Funções DAX em uso:  
* Cálculo do total de vendas com SUM
```
Soma Vendas = SUM('Pedidos Detalhes'[Total])   
```
* Cálculo do total da meta com SUM  
```
Soma Meta = SUM(Meta[Meta])  
```  
* Cálculo da média de vendas com AVERAGE
```
Media Vendas = AVERAGE('Pedidos Detalhes'[Total])  
```  

---  

#### # Criando uma coluna calculada  
MEDIDAS não criam COLUNAS, são utilizadas apenas dentro de visuais. Colunas criadas com DAX não podem ser visualizadas no Power Query porque foram criadas utilizando funções DAX que não podem ser processadas no Power Query.  
Funções DAX em uso:  
<p align="justify"> 

* Cálculo de desconto aplicado em preço unitário com multiplicação de SUM das colunas da tabela - nova medida calculada "Valor Desconto" para usar em um visual, pois não tem contexto embora esteja armazenada dentro de uma tabela.  
</p>  

```
Valor Desconto = SUM('Pedidos Detalhes'[Preço Unitário]) * SUM('Pedidos Detalhes'[Desconto])  
```
<p align="justify">  

* Cálculo de desconto aplicado em preço unitário com multiplicação direta entre linhas filtradas da tabela - nova coluna calculada "Valor Desconto2" entra na tabela, por ter um contexto de linha.  
</p>

```
Valor Desconto2 = 'Pedidos Detalhes'[Preço Unitário] * 'Pedidos Detalhes'[Desconto]  
```  

---  

#### # Realize uma divisão segura com a DIVIDE  
Funções DAX em uso:  
* Cálculo da relação entre as somas de vendas e de meta anual com DIVIDE - nova medida calculada  
```  
Vendas vs Meta = DIVIDE([Soma Vendas],[Soma Meta],BLANK())  
```
* Cálculo do percentual da relação Vendas vs Meta com reaproveitamento da medida anterior na nova medida calculada(só houve acréscimo de -1 na função DAX)  
```  
Vendas vs Meta = DIVIDE([Soma Vendas],[Soma Meta],BLANK())-1  
```  
Com o reaproveitamento da medida obtém-se um resultado mais significativo para a análise dos dados.  

---  

#### # Introdução à função CALCULATE  
Funções DAX em uso:  
* Cálculo do percentual da categoria Componentes (filtro) comparado a outras categorias na soma de vendas com CALCULATE - nova medida calculada  
```
Vendas Componentes = CALCULATE([Soma Vendas],'Produtos Categorias'[Nome Categoria]="Componentes")  
```  
* Divisão ente valores de linhas da tabela, depois de inseri-los em mesma linha com CALCULATE que alterou o contexto natural do filtro de linhas, para obter a comparação de percentuais entre as categorias.  
```
Comparação Componentes = DIVIDE([Soma Vendas],[Vendas Componentes],BLANK())  
```  

---  

#### # Função ALL e ALLSELECTED  
Funções DAX em uso:  
* Inserir total de vendas na tabela para incluir todas as linhas com CALCULATE e ALL (remove todos os filtros int e ext do visual) - nova medida calculada 
```
Todas as Vendas = CALCULATE([Soma Vendas],ALL('Pedidos Detalhes'))  
```
* Cálculo do percentual de cada categoria sobre o total de vendas com DIVIDE - nova medida calculada  
```
Repres. Categorias = DIVIDE([Soma Vendas],[Todas as Vendas])   
```  
* Inserir todas as vendas selecionadas por país específico (filtro externo) para incluir todas as linhas com CALCULATE e ALLSELECTED (remove filtros int da consulta e inclui ext ao visual) - nova medida calculada  
```
Todas Selecionadas = CALCULATE([Soma Vendas],ALLSELECTED('Pedidos Detalhes'))  
```  
* Cálculo do percentual de cada categoria por país sobre a soma de vendas das categorias com DIVIDE - nova medida calculada  
```  
Repres. Categorias Selecionadas = DIVIDE([Soma Vendas],[Todas Selecionadas])  
```  

---  

