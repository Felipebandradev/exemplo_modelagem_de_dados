# Comandos SQL - Referências

## Modelagem Física com comandos DDL

### Criar banco de dados

```
CREATE DATABASE vendas CHARACTER SET utf8mb4;
```

### Criar tabela de fabricantes

```
CREATE TABLE fabricantes(
    id INT NOT NULL PRiMARY KEY AUTO_INCREMENT,
    nome VARCHAR(45) NOT NULL
); 
```