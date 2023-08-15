# Exercícios de Modelagem

**16/08/2023**

## No phpMyAdmin utilize comandos SQL para fazer a modelagem física do exercício anterior.

Você deve:

- Criar um novo banco de dados (Catálogo de Filmes)
- Criar duas tabelas (Gêneros e Filmes)
- Fazer o relacionamento entre as tabelas

## Exercício resolvido:

```sql

CREATE DATABASE catalogo_de_filmes CHARACTER SET utf8mb4;

CREATE TABLE generos(
    id INT NOT NULL PRiMARY KEY AUTO_INCREMENT,
    nome_genero VARCHAR(45) NOT NULL
); 


CREATE TABLE filmes(
    id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
    titulo_filme VARCHAR(45) NOT NULL,
    ano_de_lancamento YEAR(4) NOT NULL,
    genero_id INT NOT NULL
);


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