# Exercícios de Modelagem


**17/08/2023**

## Refaça o exercício anterior de modelagem física (banco de dados de catalogo de Filmes e Gêneros) usando somente ferramentas da interface gráfica do phpMyAdmin.


## Exercício resolvido:

1) etapa :
![criação do banco de dados usando interface grafica](criacao_banco_de_dados.png)

2) etapa:
![criação da tabela genêro usando interface grafica](tabela_genero.png)

3) etapa:
![criação da tabela filmes usando interface grafica](tabela_filmes.png)

4) etapa:
![criação da chave estrangeira usando interface grafica](criacao_chave_estrangeira.png)

---

**16/08/2023**

## No phpMyAdmin utilize comandos SQL para fazer a modelagem física do exercício anterior.

Você deve:

- Criar um novo banco de dados (Catálogo de Filmes)
- Criar duas tabelas (Gêneros e Filmes)
- Fazer o relacionamento entre as tabelas

## Exercício resolvido:

```sql

-- Para criar um  banco de dados
CREATE DATABASE catalogo_de_filmes CHARACTER SET utf8mb4;

-- para criar a tabela Genêros 
CREATE TABLE generos(
    id INT NOT NULL PRiMARY KEY AUTO_INCREMENT,
    nome_genero VARCHAR(45) NOT NULL
); 


-- para criar a tabelas Filmes
CREATE TABLE filmes(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    titulo_filme VARCHAR(45) NOT NULL,
    ano_de_lancamento YEAR(4) NOT NULL,
    genero_id INT NOT NULL
);


-- para criar/referênciar a chave estrangeira 
ALTER TABLE filmes
    ADD CONSTRAINT fk_filmes_generos
    FOREIGN KEY (genero_id) REFERENCES generos(id); 


```

**15/08/2023**

## Crie no MySQL Workbench o modelo lógico para 2 entidades:

1) Gêneros
    - Identificador
    - Nome do gênero

2) Filmes
    - Identificador
    - Título do filme
    - Ano do lançamento
    - Gênero do Filme

**Obs.:** o filme deve ter um gênero relacionado à tabela de genêros.

---

## Exercício resolvido:

![Modelagem Filmes e Gêneros](modelo-logico-filmes.png)