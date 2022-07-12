#### # Introdução às funções iterantes  
Função DAX em uso: 
<p align="justify">  
* Substituir coluna calculada por uma medida calculada (tem menos custo computacional) com SUMX, assim há modificação do contexto de filtro. 
SUMX a medida cria um cálculo diferente considerando todas as linhas do cocntexto inserido. Sempre que uma função pede uma tabela como argumento é iterante.  
</p>  

```
Valor Desconto 3 = SUMX('Pedidos Detalhes','Pedidos Detalhes'[Preço Unitário]*'Pedidos Detalhes'[Desconto])  
```  

---  

#### # Crie tabelas de parâmetro  
Fazer uma tabela de parâmetro, criar uma variação de custo e descobrir seu lucro a partir da variação inserida no parâmetro.  
Funções DAX em uso:  
* Cria-se um contexto de filtro, observando cada linha da tabela Pedidos Detalhes e cada quantidade é multiplicada pelos custos relacionados na tabela Produtos, na coluna Custo Padrão, obtém-se Soma Custo com SUMX e RELATED.
```
Soma Custo = SUMX('Pedidos Detalhes', 'Pedidos Detalhes'[Quantidade]*RELATED(Produtos[Custo Padrão]))  
```  
* Cálculo do lucro  
``` 
Lucro = [Soma Vendas]-[Soma Custo]  
```  
<p align="justify">  
* Tabela de parâmetro para criar a variação que é aplicada em Soma Custo para calcular o Lucro de acordo com o cenário escolhido pelos usuários do relatório.  
</p>  

```
Parâmetro = GENERATESERIES(0.01, 0.09, 0.001)  
```  
* Medida Parametro Valor criada automaticamente junto com Parâmetro  
```
Parâmetro Valor = SELECTEDVALUE('Parâmetro'[Parâmetro], 0)  
```  

---  

#### # Como criar medidas dinâmicas  
Funcões DAX em uso:  
* Cálculo do custo de variação, somando Soma Custo com multiplicação entre Soma Custo e Parâmetro Valor
```
Soma Custo Variação = Produtos[Soma Custo] + Produtos[Soma Custo]*'Parâmetro'[Parâmetro Valor]  
```  
<p align="justify">   
Aplicável em simulações de novos investimentos com aumento do custo em 5,80%, em que é avalido o cenário daqui,
se compensa ou não aumentar o custo em 5,80% para ter o lucro calculado na tabela que aponta para a soma de custos.   
</p>  

* Cálculo de Lucro Variação  
```
Lucro Variação = [Soma Vendas]-Produtos[Soma Custo Variação]  
```  
Para as categorias que apresentam valores negativos é recomendado ajuste do investimento para que todas gerem lucro.  

---  

#### # Calcule o ano anterior com a SAMEPERIODLASTYEAR  
Função DAX em uso:  
<p align="justify">   
* Exibe vendas do ano anterior ao lado da coluna dos meses do ano atual com CALCULATE que muda o contexto de filtro e SAMEPERIODLASYEAR que filtra os dados.  
</p>  

```
Vendas Ano Anterior = CALCULATE([Soma Vendas],SAMEPERIODLASTYEAR('Calendário'[Data]))  
```  

---  

#### # Calcule o mês anterior com DATEADD  
Função DAX em uso:   
<p align="justify">     
DATEADD desloca um período conforme os argumentos inseridos nessa função, com CALCULATE o contexto de filtro é mudado e o mês anterior é trazido para outra
Coluna da tabela.   
</p>  

* Comparam-se as performances de vendas de mês atual e mês anterior, por isso é acrescentado -1 como argumento do intervalo filtrado.
```  
Vendas Mes Passado = CALCULATE([Soma Vendas],DATEADD('Calendário'[Data],-1,MONTH))
```  

---  

#### # Acumule valores con funções de TOTALYDT, QTD, e MTD  
TOTALYTD acumula valores conforme o contexto de filtro atual. Sigla YTD significa Year To Date.  
Funções DAX em uso:  
* Mostra acumulado de valores até o final do ano com CALCULATE e TOTALYTD, que recomeça a contagem a cada mudança de ano. 
```  
Acumulado Year To Date 2 = TOTALYTD([Soma Vendas],'Calendário'[Data])   
```  
* Mostra acumulado de valores por trimestre do ano com CALCULATE e TOTALQTD, que recomeça a contagem ao mudar de ano.  
``` 
Acumulado Year To Date Quarter = TOTALQTD([Soma Vendas],'Calendário'[Data])   
```  

---  


