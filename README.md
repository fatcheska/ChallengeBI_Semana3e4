# Challenge BI - Semanas 3 e 4 - Alura

## Dashboard Financeiro
Desenvolveremos um dashboard tático da área financeira de uma empresa, no qual vamos criar duas páginas, sendo uma delas exibindo um overview de toda a área financeira e a outra página realizando uma análise de cenários.
Teremos duas etiquetas indicando o que precisaremos pensar, sendo elas:
1 - Overview financeiro.
2 - Análise de cenário.

## Base de Dados

A base de dados consiste em quatro bancos de dados no formato SQL:
* financeiro_notas_fiscais.sql
* financeiro_pedidos.sql
* finceiro_produtos.sql
* fianceiro_vendedores.sql

## Ferramentas Utilizadas no Projeto

* Power BI
* MySQL Workbech 8

## Tratamento de Dados

* Formatação e eliminação de valores duplicados na tabela de vendedores;
* Adequação dos valores de venda e freta na tabela de notas fiscais;
* Adequação dos preços e custos na tabela de produtos.

## Métricas

As métricas incluem parâmetros que foram utilizados para a etapa de análise de cenários. Na página principal, o valor dos parâmetros não impacta nos resultados reais.

### Custos
```
Custos = SUMX(tabela_pedidos, [quantidade] * [custo]) * (1 + [% Custo Value])
```

### Despesas
```
Despesas = -([Frete] + [Imposto])
```

### Frete
```
Frete = -SUM(tabela_notas_fiscais[valor_frete_new]) * (1 + [% Cenário Despesa Value])
```

### Imposto
```
Imposto = -SUM(tabela_notas_fiscais[imposto]) * (1 + [% Cenário Despesa Value])
```

### Lucro
```
Lucro = [Receita] + [Frete] + [Imposto] - [Custos]
```

### Métrica_Evolução
Essa métrica foi criada para que se possa escolher qual métrica será mostrada na evolução mensal.
```
Métrica_Evolução = 
IF(
    SELECTEDVALUE('_Seleção de Métrica'[Métrica]) == "Custos",
    [Custos],
    IF(
        SELECTEDVALUE('_Seleção de Métrica'[Métrica]) == "Despesas",
        [Despesas],
       IF(
           SELECTEDVALUE('_Seleção de Métrica'[Métrica]) == "Lucro",
           [Lucro],
           IF(
               SELECTEDVALUE('_Seleção de Métrica'[Métrica]) == "Receita",
               [Receita],
               0
           )
       )
    )
)
```

### Receita
```
Receita = SUMX(tabela_pedidos, [quantidade] * [preço]) * (1 + [% Cenário Demanda Value]) * (1 + [% Cenário Preço Value])
```

## Relacionamentos
* tabela_produtos[id_produto] 1:* tabela_pedidos[id_produto]
* tabela_pedidos[id_pedido] 1:1 tabela_notas_fiscais[id_pedido]
* tabela_vendedores[id_vendedor] 1:* tabela_notas_fiscais[id_vendedor]

## Link do Dashboard
<p><a href ="https://app.powerbi.com/view?r=eyJrIjoiNzkzYjNhM2EtZGY3Mi00ODFiLWE0ZmEtZjlhNzc5ODg5NWJjIiwidCI6IjJiZWZhNWY5LTEyMjUtNGViYi04MjFiLTM4Yzk1MWZkYjgyZSJ9" target = "_blank">Challenge BI - Semanas 3 e 4</a></p>
