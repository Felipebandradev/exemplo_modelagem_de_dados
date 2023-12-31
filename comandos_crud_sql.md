# Comandos Para Operações CRUD no Banco de Dados

## Resumo

- C -> CREATE (Inserir dados usando o comando `INSERT`)
- R -> READ (ler dados usando o comando `SELECT`)
- U -> UPDATE (atualizar dados usando o comando `UPDATE`)
- D -> DELETE (excluir dados usando o comando `DELETE`)

## INSERT

### Fabricantes

```sql
-- forma simples
INSERT INTO fabricantes(nome) VALUES('Asus');

INSERT INTO fabricantes(nome) VALUES('Apple');
INSERT INTO fabricantes(nome) VALUES('Dell');

-- concatenado
INSERT INTO fabricantes(nome) 
VALUES('LG'),('Samsung'),('Brastemp');

INSERT INTO fabricantes(nome) 
VALUES('Positivo'),('Microssoft'),('Xiaomi');

```
### Resultados

![Tabela fabricantes depois do CRUD](tabela_fabricantes_depois_do_crud.png)

### Produtos

```sql

INSERT INTO produtos(
    nome, descricao, preco, quantidade, fabricante_id
) 
VALUES (
    'Ultrabook', 
    'Equipamento de Ultima geração cheio de recursos, com processador INTEL core i9 do balacobaco',
    3500,
    7,
    4 -- id do fabricante Dell
);


INSERT INTO produtos(
    nome, descricao, preco, quantidade, fabricante_id
) 
VALUES (
    ' Tablet Android', 
    'Tablet com a versão 14 do sistema operacional android possui tela de 10 polegadas e 128 GB, e 64 GB de RAM porque o ELIEL perguntou',
    1500.99,
    5,
    5 -- id do fabricante LG
);


INSERT INTO produtos(
    nome, descricao, preco, quantidade, fabricante_id
) 
VALUES (
    ' Geladeira', 
    'Refrigerador frost-free com acesso à internet',
    5000,
    12,
    7 -- id do fabricante Brastemp
), (
    'Iphone 18 pro Max',
    'Smart phone apple cheio de frescuras da marca e cara para caramba...coisa de rico',
    12666.66,
    3,
    3 -- id do fabricante Apple
), (
    'iPad mini',
    'Tablet Apple com tele retina display bla bla bla',
    4999.01,
    5,
    3 -- id do fabricante Apple
);
```
### Resultados

![Tabela produtos depois do CRUD](tabela_produtos_depois_do_crud.png)

---

## SELECT (READ)

```sql

-- Query

-- Para exibir todas as colunas da tabela
SELECT * FROM produtos;
SELECT * FROM fabricantes;

-- Para exibir somente os nome e preço dos produtos
SELECT nome, preco FROM produtos;

-- mudando apenas a ordem de exibição
SELECT preco, nome FROM produtos;

-- Sendo mais criterioso
SELECT nome, preco, quantidade FROM produtos
     WHERE preco < 5000;

-- EXERCÍCIO: mostre nome e descrição só dos produtos da apple
SELECT nome, descricao FROM produtos
     WHERE fabricante_id = 3;

```

### Operadores Lógicos: E (AND), OU (OR), NÃO (NOT)


#### E

```sql
SELECT nome, preco FROM produtos 
    WHERE preco >= 2000 AND  preco <= 6000;

-- A query Abaixo não retorna registros 
-- já que as condições não foram totalmente atendidas atendidas
SELECT nome, preco FROM produtos 
    WHERE preco > 5000 AND  preco <= 6000;

```

#### OU

```sql

SELECT nome, preco FROM produtos 
    WHERE preco > 5000 OR  preco <= 3000;

-- EXERCÍCIO: Exiba nome e preço somente dos produtos da apple e da LG
SELECT nome, preco FROM produtos
    WHERE fabricante_id = 3 OR fabricante_id = 5;

-- Versão usando a função IN() 
-- IN = DENTRO
SELECT nome, preco FROM produtos
    WHERE fabricante_id IN(3, 5);

```

#### NÃO 

```sql

SELECT nome, descricao, preco FROM produtos
    WHERE NOT fabricante_id = 9;

-- Versão usando o operador relacional de diferença
-- ! = Diferente 
SELECT nome, descricao, preco FROM produtos
    WHERE  fabricante_id != 9;


SELECT nome, preco FROM produtos
    WHERE fabricante_id NOT IN(3,5);
```

---

## UPDATE

```sql
UPDATE fabricantes SET nome = 'Asus do Brasil'
    WHERE id = 1; -- ⚠️☠️NÃO SE ESQUEÇA DO WHERE!! PERIGO!☠️⚠️

UPDATE produtos SET preco = 6549.74
    WHERE id = 4;
-- Alteres a quantidade dos dos produtos da Apple e da LG para 20

UPDATE produtos SET quantidade = 20
    WHERE fabricante_id IN (3, 5); -- ⚠️☠️NÃO SE ESQUEÇA DO WHERE!! PERIGO!☠️⚠️


```

---

## DELETE

```sql
DELETE FROM fabricantes WHERE id = 1;  -- ⚠️☠️NÃO SE ESQUEÇA DO WHERE!! PERIGO!☠️⚠️

-- A query abaixo NÃO FUNCIONA devido à restrição de chave estrangeira/relacionamento, ou seja, existem produtos associados ao fabricante 3 (Apple)
-- DELETE FROM fabricantes WHERE id = 3;

```

---

## SELECT: outras formas de uso

### Classificando
```sql
SELECT nome, preco FROM produtos ORDER BY nome;
SELECT nome, preco FROM produtos ORDER BY preco;
SELECT nome, preco FROM produtos ORDER BY preco DESC;

-- DESC: classificação em ordem decrescente
-- ASC (padrão): Classificação em ordem Crescente

SELECT nome, preco FROM produtos
    WHERE quantidade = 20 ORDER BY nome;
```

### Busca de dados

```sql
SELECT nome, descricao FROM produtos 
    WHERE descricao LIKE '%sistema%';

SELECT nome, descricao FROM produtos 
    WHERE descricao LIKE '%tela%' OR nome LIKE '%variavel%';

-- Usamos o operador LIKE e o Caractere coringa (%) para permitir uma busca da palavra indicada em qualquer posição dentro do texto. Neste contexto, o % significa 'qualquer texto' antes da palavra ou depois da palavra
```

### Operações e Funções de agregação

```sql
SELECT SUM(preco)  FROM produtos; -- SOMA
SELECT SUM(preco) as Total FROM produtos; -- Alias/apelido

-- Exemplo de alias/apelido para outras colunas
SELECT nome as Produto, preco as "Preço" FROM produtos;
SELECT nome  Produto, preco  "Preço" FROM produtos;

--Média e ARREDONDAMENTO
SELECT AVG(preco) as "Média dos Preços" FROM produtos;
SELECT ROUND(AVG(preco)) as "Média dos Preços" FROM produtos;
-- Arredondamento com a casa decimal
SELECT ROUND(AVG(preco),2) as "Média dos Preços" FROM produtos;


--Contagem

SELECT COUNT(id) as "Qtd de Produtos" FROM produtos;


--  DISTINCT é uma cláusula/flag que evita a duplicidade na contagem de registros
-- Usando o DISTINCT para evitar a contagem de itens repitidos
SELECT COUNT(DISTINCT fabricante_id) as "Qtd de Fabricantes com Produtos" FROM produtos;
```

### Operações Matemáticas

```sql
SELECT nome, preco, quantidade, (preco * quantidade) as Total
FROM produtos;
```

### Segmentação/Agrupamento de resultados

```sql
SELECT fabricante_id, SUM(preco) as Total FROM produtos
GROUP BY fabricante_id;
```

---

## Consultas (Queries) em duas ou mais tabelas relacionadas (JUNÇÃO/JOIN0)

### Exibir nome do produtos e nome do fabricante

```sql
-- SELECT tabela.coluna, tabela.nome
SELECT produtos.nome as produto, fabricantes.nome as fabricante
-- INNER JOIN é o comando q permite JUNTAR as tebelas
    FROM produtos INNER JOIN fabricantes 
-- ON comando para indicar a forma/critério da junção
        ON produtos.fabricante_id = fabricantes.id;
```

### Nome do produto, nome do fabricante, ordenados pelo nome do produto

```sql
SELECT
    produtos.nome as Produto,
    fabricantes.nome as Fabricante,
    produtos.preco as "Preço"
FROM produtos INNER JOIN fabricantes
ON produtos.fabricante_id = fabricantes.id
ORDER BY Produto; -- Ou produtos.nome
```


### Fabricante, soma dos preços quantidade de produtos

```sql
SELECT
    fabricantes.nome as Fabricante, 
    SUM(produtos.preco) as Total,
    COUNT(produtos.fabricante_id) as "Qtd de Produtos"
FROM produtos INNER JOIN fabricantes
ON produtos.fabricante_id = fabricantes.id
GROUP BY Fabricante
ORDER BY Total;
```
#### Trazer a quantidade de produtos de cada Fabricante e a soma dos estoque destes produtos, SOMENTE dos FABRICANTES QUE POSSUEM PRODUTOS

```sql
SELECT 
    fabricantes.nome as Fabricante,
    COUNT(produtos.fabricante_id) as "Qtd de Produtos",
    SUM(produtos.quantidade) as "Total em Estoque"
FROM produtos INNER JOIN fabricantes
ON produtos.fabricante_id = fabricantes.id
GROUP BY Fabricante
ORDER BY SUM(produtos.quantidade) DESC;
```

#### Trazer a quantidade de produtos de cada Fabricante e a soma dos estoque destes produtos, MESMO os FABRICANTES QUE NÃO POSSUEM PRODUTOS.

```sql
SELECT 
    fabricantes.nome as Fabricante,
    COUNT(produtos.fabricante_id) as "Qtd de Produtos",
    SUM(produtos.quantidade) as "Total em Estoque"
--    LEFT JOIN    |      RIGHT JOIN
-- FROM fabricantes LEFT JOIN produtos
FROM produtos RIGHT JOIN fabricantes
ON produtos.fabricante_id = fabricantes.id
GROUP BY Fabricante
ORDER BY SUM(produtos.quantidade) DESC;
```
