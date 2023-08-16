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


