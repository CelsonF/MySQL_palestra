# MySQL_palestra
Schema de Dados

## Nesta Introdução iremos criar coisas simples para enter o funcionamento da ferramenta MySql Workbench


### Cria Base de dados com nome População sem acentuação.
```sql
CREATE DATABASE POPULACAO;
```
### Seleciona qual banco de dados iremos alterar.
```sql
USE POPULACAO;
```

### Cria Tabela Pessoas
```sql 
CREATE TABLE PESSOAS (
ID INT auto_increment primary key,
CPF varchar(14),
NOME varchar(150),
IDADE int,
SEXO char,
CIDADE varchar(250)
);
```

### Simular error
```sql 
-- Erro ao Inserir linha , demonstrar console.
INSERT INTO PESSOA (nome, idade, sexo ,cidade) VALUES
('João', 25, 'M',  'São Paulo'),
('Maria', 30, 'F', 'Rio de Janeiro'),
('Carlos', 22, 'M', 'Belo Horizonte');
```

### Create(Criar)
```sql
INSERT INTO PESSOAS (cpf, nome, idade, sexo ,cidade) VALUES
('013.345.643-20', 'João', 25, 'M', 'São Paulo'),
('022.324.643-40', 'Maria', 30, 'F', 'Rio de Janeiro'),
('904.687.233-44', 'Carlos', 22, 'M', 'Belo Horizonte'),
('561.324.654-12', 'Ana', 28, 'F', 'Salvador'),
('789.456.123-45', 'Pedro', 35, 'M', 'Curitiba'),
('123.987.654-32', 'Laura', 29, 'F', 'Porto Alegre'),
('456.789.321-01', 'Lucas', 24, 'M', 'Fortaleza'),
('987.654.321-12', 'Beatriz', 31, 'F', 'Recife'),
('654.321.987-45', 'Gustavo', 27, 'M', 'Manaus'),
('333.111.555-99', 'Mariana', 26, 'F', 'Brasília'),
('000.111.222-33', 'Rafael', 29, 'M', 'São Paulo'),
('444.555.666-77', 'Amanda', 23, 'F', 'Rio de Janeiro'),
('888.999.000-11', 'Thiago', 30, 'M', 'Belo Horizonte'),
('111.222.333-44', 'Isabela', 28, 'F', 'Salvador'),
('555.666.777-88', 'Matheus', 34, 'M', 'Curitiba'),
('999.000.111-22', 'Juliana', 25, 'F', 'Porto Alegre'),
('333.444.555-66', 'Guilherme', 26, 'M', 'Fortaleza'),
('777.888.999-00', 'Fernanda', 30, 'F', 'Recife'),
('222.333.444-55', 'Vitor', 27, 'M', 'Manaus'),
('666.777.888-99', 'Luana', 29, 'F', 'Brasília'),
('111.222.333-44', 'Ricardo', 33, 'M', 'São Paulo'),
('555.666.777-88', 'Carolina', 24, 'F', 'Rio de Janeiro'),
('999.000.111-22', 'Eduardo', 31, 'M', 'Belo Horizonte');
```

### Relacionamento com outra tabela CHAMADA - EMAIL	
```sql
CREATE TABLE EMAILS (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    PESSOA_ID INT,
    EMAIL VARCHAR(255),
    FOREIGN KEY (PESSOA_ID) REFERENCES PESSOAS(ID) ON DELETE CASCADE
); 
```
 
-- Inserir e-mails fictícios para todas as pessoas na tabela EMAILS
INSERT INTO EMAILS (PESSOA_ID, EMAIL) VALUES
(1, 'joao_01334564320@exemplo.com'),
(2, 'maria_02232464340@exemplo.com'),
(3, 'carlos_90468723344@exemplo.com'),
(4, 'ana_56132465412@exemplo.com'),
(5, 'pedro_78945612345@exemplo.com'),
(6, 'laura_12398765432@exemplo.com'),
(7, 'lucas_45678932101@exemplo.com'),
(8, 'beatriz_98765432112@exemplo.com'),
(9, 'gustavo_65432198745@exemplo.com'),
(10, 'mariana_33311155599@exemplo.com'),
(11, 'rafael_00011122233@exemplo.com'),
(12, 'amanda_44455566677@exemplo.com'),
(13, 'thiago_88899900011@exemplo.com'),
(14, 'isabela_11122233344@exemplo.com'),
(15, 'matheus_55566677788@exemplo.com'),
(16, 'juliana_99900011122@exemplo.com'),
(17, 'guilherme_33344455566@exemplo.com'),
(18, 'fernanda_77788899900@exemplo.com'),
(19, 'vitor_22233344455@exemplo.com'),
(20, 'luana_66677788899@exemplo.com'),
(21, 'ricardo_11122233344@exemplo.com'),
(22, 'carolina_55566677788@exemplo.com'),
(23, 'eduardo_99900011122@exemplo.com');




-- READ(Ler) - Leitura de todos os items da tabela
SELECT * FROM PESSOAS;

-- Leitura de tabela colunas específicos 
SELECT p.nome, p.cidade FROM PESSOAS p;

-- Leitura com condições específicas - neste caso idade
SELECT 
	p.idade,
	p.nome, 
    p.cidade
FROM 
	PESSOAS p
WHERE
    p.idade >= 28 AND p.idade <= 32;


/* 
WHERE p.nome LIKE 'a%': Isso encontra quaisquer valores que comecem com "a".
WHERE p.nome LIKE '%a': Isso encontra quaisquer valores que terminem com "a".
WHERE p.nome LIKE '%or%': Isso encontra quaisquer valores que contenham "or" em qualquer posição.
WHERE p.nome LIKE '_r%': Isso encontra quaisquer valores que tenham "r" na segunda posição.
WHERE p.nome LIKE 'a_%': Isso encontra quaisquer valores que comecem com "a" e tenham pelo menos 2 caracteres de comprimento.
WHERE p.nome LIKE 'a__%': Isso encontra quaisquer valores que comecem com "a" e tenham pelo menos 3 caracteres de comprimento.
WHERE p.nome LIKE 'a%o': Isso encontra quaisquer valores que comecem com "a" e terminem com "o"
*/

-- Leitura de condicional com operador LIKE e nome que começa com a letra C
SELECT 
	p.idade,
	p.nome, 
    p.cidade
FROM 
	PESSOAS p
WHERE
    p.nome LIKE 'c%';


-- UPDATE(ATUALIZAR) é a operação para modificar os arquivos já gravados na tabela.
-- EXEMPLO a ser atualizado ('013.345.643-20', 'João', 25, 'M', 'São Paulo'),
SELECT * FROM PESSOAS p; 

UPDATE 
	PESSOAS p
SET 
	p.cidade = 'Ouro Preto'
WHERE p.id = 1;

SELECT * FROM PESSOAS p;

-- DELETE(Deletar) - Deletado o ID - 1 , Nome João
DELETE FROM PESSOAS p WHERE p.id = 1;

-- Porque não deltar pelo nome 
DELETE FROM PESSOAS p WHERE p.nome = 'João'; 



-- Leitura juntando as 2 tabelas atraves do ID
SELECT p.nome, e.email 
FROM pessoas p , emails e 
WHERE e.id = p.id
