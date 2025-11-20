# Fundamentos de SQL

## Introdução

SQL (Structured Query Language) é uma linguagem padrão para gerenciar e manipular dados em sistemas de gerenciamento de banco de dados relacional (SGBDR). Este documento apresenta os conceitos fundamentais necessários para trabalhar com SQL.

---

## 1. O que é SQL?

SQL é uma linguagem declarativa usada para:
- **Criar** estruturas de dados (tabelas, índices, etc.)
- **Inserir** dados em um banco de dados
- **Consultar** dados existentes
- **Atualizar** dados existentes
- **Deletar** dados
- **Controlar** permissões e segurança

---

## 2. Conceitos Básicos

### 2.1 Banco de Dados
Um banco de dados é um repositório organizado de dados. É uma coleção de tabelas, índices, procedures e outras estruturas que armazenam informações de forma estruturada.

### 2.2 Tabelas
Uma tabela é a estrutura principal de armazenamento de dados em um banco de dados relacional. Ela é organizada em **linhas** (registros) e **colunas** (campos/atributos).

```
┌─────────────────────────────────────────┐
│          Tabela: tb_funcionario         │
├─────────┬──────────┬──────────┬─────────┤
│   ID    │  NOME    │ SALARIO  │ DEPTO   │
├─────────┼──────────┼──────────┼─────────┤
│    1    │  João    │  3000    │   10    │
│    2    │  Maria   │  3500    │   10    │
│    3    │  Pedro   │  2800    │   20    │
└─────────┴──────────┴──────────┴─────────┘
```

### 2.3 Colunas (Campos)
Cada coluna possui um nome e um tipo de dados que define que tipo de informação ela pode conter.

### 2.4 Linhas (Registros)
Cada linha representa um registro único em uma tabela.

---

## 3. Tipos de Dados Comuns

| Tipo | Descrição | Exemplo |
|------|-----------|---------|
| **INT** | Números inteiros | `123`, `-45` |
| **FLOAT** | Números com decimais | `123.45`, `3.14` |
| **VARCHAR(n)** | Texto variável | `"João Silva"` |
| **CHAR(n)** | Texto fixo | `"M"` (sexo) |
| **DATE** | Data | `2024-01-15` |
| **TIMESTAMP** | Data e hora | `2024-01-15 14:30:00` |
| **BOOLEAN** | Verdadeiro/Falso | `TRUE`, `FALSE` |
| **SERIAL** | Inteiro auto-incrementável | Gerado automaticamente |

---

## 4. Componentes Principais de SQL

SQL é dividido em três linguagens principais:

### 4.1 DDL (Data Definition Language)
Define a estrutura do banco de dados.

**Comandos:**
- `CREATE` - Criar objetos (tabelas, índices, etc.)
- `ALTER` - Modificar objetos existentes
- `DROP` - Remover objetos

**Exemplo:**
```sql
CREATE TABLE tb_cargo(
    id INT PRIMARY KEY,
    nome VARCHAR(20) NOT NULL,
    salario FLOAT
);
```

### 4.2 DML (Data Manipulation Language)
Manipula os dados dentro das tabelas.

**Comandos:**
- `INSERT` - Inserir novos registros
- `UPDATE` - Modificar registros existentes
- `DELETE` - Remover registros

**Exemplo:**
```sql
INSERT INTO tb_cargo (id, nome, salario) 
VALUES (1, 'Analista', 5000);
```

### 4.3 DQL (Data Query Language)
Consulta os dados armazenados.

**Comando:**
- `SELECT` - Recuperar dados

**Exemplo:**
```sql
SELECT id, nome, salario 
FROM tb_cargo 
WHERE salario > 3000;
```

---

## 5. Restrições (Constraints)

Restrições garantem a integridade e qualidade dos dados:

### 5.1 PRIMARY KEY
Identifica unicamente cada registro na tabela. Não pode ser NULL e deve ser único.

```sql
CREATE TABLE tb_aluno(
    cpf VARCHAR(12) PRIMARY KEY,
    nome VARCHAR(40) NOT NULL
);
```

### 5.2 FOREIGN KEY
Estabelece uma relação entre duas tabelas. A coluna deve conter um valor que existe na tabela referenciada.

```sql
CREATE TABLE tb_turma(
    id SERIAL PRIMARY KEY,
    cursoId INT NOT NULL,
    FOREIGN KEY(cursoId) REFERENCES tb_curso(id)
);
```

### 5.3 NOT NULL
Garante que a coluna sempre tenha um valor.

```sql
CREATE TABLE tb_cargo(
    id INT PRIMARY KEY,
    nome VARCHAR(20) NOT NULL
);
```

### 5.4 UNIQUE
Garante que todos os valores na coluna sejam únicos.

```sql
ALTER TABLE tb_funcionario 
ADD CONSTRAINT uk_email UNIQUE(email);
```

### 5.5 DEFAULT
Define um valor padrão se nenhum valor for fornecido.

```sql
CREATE TABLE tb_evento(
    id INT PRIMARY KEY,
    status VARCHAR(20) DEFAULT 'Planejado'
);
```

### 5.6 CHECK
Valida dados com uma condição específica.

```sql
CREATE TABLE tb_curso(
    id INT PRIMARY KEY,
    cargaHoraria INT CHECK(cargaHoraria > 0)
);
```

---

## 6. Operações CRUD

CRUD representa as quatro operações básicas em dados:

### 6.1 CREATE (Inserir)
```sql
INSERT INTO tb_cargo (id, nome, salario)
VALUES (1, 'Gerente', 5500);
```

### 6.2 READ (Consultar)
```sql
SELECT * FROM tb_cargo;
```

### 6.3 UPDATE (Atualizar)
```sql
UPDATE tb_cargo 
SET salario = 6000 
WHERE id = 1;
```

### 6.4 DELETE (Deletar)
```sql
DELETE FROM tb_cargo 
WHERE id = 1;
```

---

## 7. Estrutura Básica de uma Consulta SELECT

```sql
SELECT coluna1, coluna2, ...
FROM tabela1
WHERE condição
GROUP BY coluna
HAVING condição_grupo
ORDER BY coluna [ASC|DESC];
```

**Cláusulas:**
- **SELECT** - Define quais colunas exibir
- **FROM** - Especifica a(s) tabela(s)
- **WHERE** - Filtra linhas com condições
- **GROUP BY** - Agrupa linhas por valores
- **HAVING** - Filtra grupos com condições
- **ORDER BY** - Ordena o resultado

**Exemplo:**
```sql
SELECT nome, salario
FROM tb_funcionario
WHERE salario > 3000
ORDER BY salario DESC;
```

---

## 8. Relacionamentos entre Tabelas

### 8.1 Um-para-Um (1:1)
Uma linha em uma tabela se relaciona com exatamente uma linha em outra tabela.

### 8.2 Um-para-Muitos (1:N)
Uma linha em uma tabela se relaciona com múltiplas linhas em outra tabela.

```
tb_curso (1)
    ↓
    └─→ tb_turma (N)
```

### 8.3 Muitos-para-Muitos (N:N)
Múltiplas linhas em uma tabela se relacionam com múltiplas linhas em outra tabela. Requer uma tabela intermediária.

```
tb_aluno (N)
    ↓
    ↔ tb_aluno_turma (associativa)
    ↑
tb_turma (N)
```

---

## 9. Boas Práticas

### 9.1 Naming Conventions (Convenções de Nomenclatura)
- Use nomes descritivos e em minúsculas: `tb_funcionario`
- Use prefixos para tabelas: `tb_` ou apenas o nome
- Use snake_case para colunas: `data_nascimento`, `codigo_departamento`
- Evite palavras reservadas como nomes

### 9.2 Chaves Primárias
- Toda tabela deve ter uma chave primária
- Prefira chaves simples quando possível
- Use SERIAL ou AUTO_INCREMENT para IDs

### 9.3 Organização de Código
- Use indentação consistente
- Coloque constraints em linhas separadas
- Use comentários para explicar estruturas complexas

### 9.4 Integridade dos Dados
- Use NOT NULL quando apropriado
- Implemente FOREIGN KEYs para manter referencial
- Use CHECK para validação de negócio

---

## 10. Exemplo Completo

```sql
-- Criar tabela de Departamentos
CREATE TABLE tb_departamento(
    id INT PRIMARY KEY,
    nome VARCHAR(30) NOT NULL,
    sigla VARCHAR(5) UNIQUE
);

-- Criar tabela de Cargos
CREATE TABLE tb_cargo(
    id INT PRIMARY KEY,
    nome VARCHAR(20) NOT NULL,
    salario FLOAT CHECK(salario > 0)
);

-- Criar tabela de Funcionários
CREATE TABLE tb_funcionario(
    id INT PRIMARY KEY,
    nome VARCHAR(40) NOT NULL,
    data_admissao DATE NOT NULL,
    codigo_cargo INT NOT NULL,
    codigo_departamento INT NOT NULL,
    FOREIGN KEY(codigo_cargo) REFERENCES tb_cargo(id),
    FOREIGN KEY(codigo_departamento) REFERENCES tb_departamento(id)
);

-- Inserir dados
INSERT INTO tb_departamento (id, nome, sigla) 
VALUES (1, 'Recursos Humanos', 'RH');

INSERT INTO tb_cargo (id, nome, salario) 
VALUES (1, 'Analista RH', 4500);

INSERT INTO tb_funcionario (id, nome, data_admissao, codigo_cargo, codigo_departamento)
VALUES (1, 'João Silva', '2023-01-15', 1, 1);

-- Consultar dados
SELECT f.nome, c.nome AS cargo, d.nome AS departamento
FROM tb_funcionario f
JOIN tb_cargo c ON f.codigo_cargo = c.id
JOIN tb_departamento d ON f.codigo_departamento = d.id;
```

---

## 11. Próximos Passos

Após compreender estes fundamentos, você deve estudar:
1. **Consultas Avançadas** - JOINs, subconsultas, agregações
2. **Normalização** - Estruturação eficiente de tabelas
3. **Índices e Performance** - Otimização de consultas
4. **Transações** - Garantir consistência de dados
5. **Triggers e Procedures** - Automação de operações

---

## Referências

- Este repositório contém exemplos práticos de todos esses conceitos
- Consulte a pasta "4 - SQL DDL e DML" para exemplos de DDL e DML
- Consulte a pasta "5 - Consultas SQL" para exemplos de DQL
