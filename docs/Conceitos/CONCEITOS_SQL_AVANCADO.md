# Conceitos Avançados de SQL

## Introdução

Este documento explora os conceitos mais avançados da linguagem SQL, incluindo consultas complexas, relacionamentos sofisticados e otimizações de performance. Estes conceitos são essenciais para trabalhar com banco de dados em aplicações profissionais.

---

## 1. JOINs - Combinando Tabelas

### 1.1 INNER JOIN
Retorna apenas as linhas que possuem correspondência em ambas as tabelas.

```sql
SELECT 
    f.nome AS funcionario,
    c.nome AS cargo,
    c.salario
FROM tb_funcionario f
INNER JOIN tb_cargo c ON f.codigo_cargo = c.id;
```

**Diagrama:**
```
Tabela A        Tabela B
┌─────┐        ┌─────┐
│  1  │────────│  1  │
│  2  │        │  3  │
│  3  │────────│  4  │
└─────┘        └─────┘
   Resultado: 1, 3
```

### 1.2 LEFT JOIN (LEFT OUTER JOIN)
Retorna todas as linhas da tabela esquerda e as correspondentes da direita.

```sql
SELECT 
    d.nome AS departamento,
    COUNT(f.id) AS total_funcionarios
FROM tb_departamento d
LEFT JOIN tb_funcionario f ON d.id = f.codigo_departamento
GROUP BY d.id, d.nome;
```

### 1.3 RIGHT JOIN (RIGHT OUTER JOIN)
Retorna todas as linhas da tabela direita e as correspondentes da esquerda.

```sql
SELECT 
    c.nome AS cargo,
    f.nome AS funcionario
FROM tb_funcionario f
RIGHT JOIN tb_cargo c ON f.codigo_cargo = c.id;
```

### 1.4 FULL OUTER JOIN
Retorna todas as linhas de ambas as tabelas, preenchendo com NULL onde não há correspondência.

```sql
SELECT 
    f.nome AS funcionario,
    c.nome AS cargo
FROM tb_funcionario f
FULL OUTER JOIN tb_cargo c ON f.codigo_cargo = c.id;
```

### 1.5 CROSS JOIN
Retorna o produto cartesiano de duas tabelas (todas as combinações possíveis).

```sql
SELECT 
    d.nome AS departamento,
    c.nome AS cargo
FROM tb_departamento d
CROSS JOIN tb_cargo c;
```

### 1.6 SELF JOIN
Uma tabela se junta a si mesma.

```sql
SELECT 
    f1.nome AS funcionario,
    f2.nome AS supervisor
FROM tb_funcionario f1
LEFT JOIN tb_funcionario f2 ON f1.codigo_supervisor = f2.id;
```

---

## 2. Funções de Agregação

Funções que operam em conjunto de dados retornando um único valor.

### 2.1 COUNT
Conta o número de linhas ou valores não-nulos.

```sql
SELECT COUNT(*) AS total_funcionarios FROM tb_funcionario;
SELECT COUNT(data_demissao) AS demitidos FROM tb_funcionario;
```

### 2.2 SUM
Soma os valores de uma coluna numérica.

```sql
SELECT 
    codigo_departamento,
    SUM(salario) AS folha_pagamento
FROM tb_funcionario
GROUP BY codigo_departamento;
```

### 2.3 AVG
Calcula a média dos valores de uma coluna numérica.

```sql
SELECT 
    codigo_departamento,
    AVG(salario) AS salario_medio
FROM tb_funcionario
GROUP BY codigo_departamento;
```

### 2.4 MIN e MAX
Retorna o valor mínimo ou máximo de uma coluna.

```sql
SELECT 
    codigo_departamento,
    MIN(salario) AS menor_salario,
    MAX(salario) AS maior_salario
FROM tb_funcionario
GROUP BY codigo_departamento;
```

### 2.5 STRING_AGG / GROUP_CONCAT
Concatena valores de uma coluna em uma string (variação por SGBD).

```sql
-- PostgreSQL
SELECT 
    codigo_departamento,
    STRING_AGG(nome, ', ') AS funcionarios
FROM tb_funcionario
GROUP BY codigo_departamento;

-- MySQL
SELECT 
    codigo_departamento,
    GROUP_CONCAT(nome SEPARATOR ', ') AS funcionarios
FROM tb_funcionario
GROUP BY codigo_departamento;
```

---

## 3. GROUP BY e HAVING

### 3.1 GROUP BY
Agrupa linhas que têm o mesmo valor em colunas especificadas.

```sql
SELECT 
    codigo_departamento,
    COUNT(*) AS total_funcionarios,
    AVG(salario) AS salario_medio
FROM tb_funcionario
GROUP BY codigo_departamento;
```

### 3.2 HAVING
Filtra grupos criados por GROUP BY (similar a WHERE, mas para agregações).

```sql
SELECT 
    codigo_departamento,
    COUNT(*) AS total_funcionarios,
    AVG(salario) AS salario_medio
FROM tb_funcionario
GROUP BY codigo_departamento
HAVING COUNT(*) > 3 AND AVG(salario) > 4000;
```

**Diferença entre WHERE e HAVING:**

| WHERE | HAVING |
|-------|--------|
| Filtra **antes** da agregação | Filtra **depois** da agregação |
| Funciona em linhas individuais | Funciona em grupos |
| Não pode usar funções de agregação | Pode usar funções de agregação |

---

## 4. Subconsultas

### 4.1 Subconsultas no SELECT
```sql
SELECT 
    nome,
    salario,
    (SELECT AVG(salario) FROM tb_funcionario) AS salario_medio,
    CASE 
        WHEN salario > (SELECT AVG(salario) FROM tb_funcionario) THEN 'Acima da média'
        ELSE 'Abaixo da média'
    END AS categoria
FROM tb_funcionario;
```

### 4.2 Subconsultas no FROM
```sql
SELECT 
    departamento,
    total_funcionarios,
    salario_medio
FROM (
    SELECT 
        codigo_departamento AS departamento,
        COUNT(*) AS total_funcionarios,
        AVG(salario) AS salario_medio
    FROM tb_funcionario
    GROUP BY codigo_departamento
) AS resumo_departamentos
WHERE total_funcionarios > 5;
```

### 4.3 Subconsultas no WHERE
```sql
SELECT 
    nome,
    salario
FROM tb_funcionario
WHERE salario > (
    SELECT AVG(salario) 
    FROM tb_funcionario
)
ORDER BY salario DESC;
```

### 4.4 Subconsultas com IN
```sql
SELECT 
    f.nome,
    f.codigo_departamento
FROM tb_funcionario f
WHERE f.codigo_departamento IN (
    SELECT id 
    FROM tb_departamento 
    WHERE sigla IN ('RH', 'TI', 'ADM')
);
```

### 4.5 Subconsultas com EXISTS
```sql
SELECT 
    d.nome AS departamento
FROM tb_departamento d
WHERE EXISTS (
    SELECT 1 
    FROM tb_funcionario f 
    WHERE f.codigo_departamento = d.id 
    AND f.salario > 5000
);
```

---

## 5. UNION e UNION ALL

### 5.1 UNION
Combina resultados de múltiplas consultas, removendo duplicatas.

```sql
SELECT nome, 'Ativo' AS status
FROM tb_funcionario
WHERE data_demissao IS NULL

UNION

SELECT nome, 'Inativo' AS status
FROM tb_funcionario
WHERE data_demissao IS NOT NULL;
```

### 5.2 UNION ALL
Combina resultados mantendo duplicatas.

```sql
SELECT id, nome FROM tb_departamento
UNION ALL
SELECT id, nome FROM tb_cargo;
```

---

## 6. Window Functions

### 6.1 ROW_NUMBER
Numera as linhas sequencialmente dentro de uma partição.

```sql
SELECT 
    nome,
    salario,
    codigo_departamento,
    ROW_NUMBER() OVER (
        PARTITION BY codigo_departamento 
        ORDER BY salario DESC
    ) AS ranking_salario
FROM tb_funcionario;
```

### 6.2 RANK e DENSE_RANK
Ranqueia linhas com tratamento de empates.

```sql
SELECT 
    nome,
    salario,
    RANK() OVER (ORDER BY salario DESC) AS ranking,
    DENSE_RANK() OVER (ORDER BY salario DESC) AS dense_ranking
FROM tb_funcionario;
```

### 6.3 LAG e LEAD
Acessa dados de linhas anteriores ou posteriores.

```sql
SELECT 
    nome,
    salario,
    LAG(salario) OVER (ORDER BY nome) AS salario_anterior,
    LEAD(salario) OVER (ORDER BY nome) AS salario_proximo
FROM tb_funcionario;
```

### 6.4 SUM OVER (Window Aggregate)
Soma com partição de janela.

```sql
SELECT 
    nome,
    salario,
    codigo_departamento,
    SUM(salario) OVER (PARTITION BY codigo_departamento) AS folha_departamento,
    SUM(salario) OVER () AS folha_total
FROM tb_funcionario;
```

---

## 7. Common Table Expressions (CTE)

### 7.1 WITH (CTE Simples)
Define uma consulta temporária que pode ser reutilizada.

```sql
WITH resumo_departamentos AS (
    SELECT 
        codigo_departamento,
        COUNT(*) AS total_funcionarios,
        AVG(salario) AS salario_medio,
        MAX(salario) AS maior_salario
    FROM tb_funcionario
    GROUP BY codigo_departamento
)
SELECT 
    d.nome AS departamento,
    rd.total_funcionarios,
    rd.salario_medio,
    rd.maior_salario
FROM resumo_departamentos rd
JOIN tb_departamento d ON rd.codigo_departamento = d.id
WHERE rd.total_funcionarios > 5;
```

### 7.2 CTE Recursiva
Define um padrão recursivo para hierarquias.

```sql
WITH RECURSIVE hierarquia AS (
    -- Caso base: funcionários sem supervisor
    SELECT 
        id,
        nome,
        codigo_supervisor,
        1 AS nivel
    FROM tb_funcionario
    WHERE codigo_supervisor IS NULL
    
    UNION ALL
    
    -- Caso recursivo: funcionários com supervisor
    SELECT 
        f.id,
        f.nome,
        f.codigo_supervisor,
        h.nivel + 1
    FROM tb_funcionario f
    JOIN hierarquia h ON f.codigo_supervisor = h.id
)
SELECT * FROM hierarquia ORDER BY nivel, nome;
```

---

## 8. Operadores Especiais

### 8.1 CASE
Implementa lógica condicional.

```sql
SELECT 
    nome,
    salario,
    CASE 
        WHEN salario < 2000 THEN 'Baixo'
        WHEN salario < 4000 THEN 'Médio'
        WHEN salario < 6000 THEN 'Alto'
        ELSE 'Muito Alto'
    END AS faixa_salarial
FROM tb_funcionario;
```

### 8.2 BETWEEN
Verifica se um valor está dentro de um intervalo.

```sql
SELECT 
    nome,
    salario
FROM tb_funcionario
WHERE salario BETWEEN 3000 AND 5000;
```

### 8.3 LIKE e Pattern Matching
Busca por padrões em texto.

```sql
SELECT 
    nome
FROM tb_funcionario
WHERE nome LIKE 'J%'      -- Começa com J
   OR nome LIKE '%Silva'  -- Termina com Silva
   OR nome LIKE '%da%';   -- Contém 'da'
```

### 8.4 IN e NOT IN
Verifica pertencimento a conjunto.

```sql
SELECT *
FROM tb_funcionario
WHERE codigo_cargo IN (1, 3, 5)
  AND codigo_departamento NOT IN (2, 4);
```

### 8.5 IS NULL e IS NOT NULL
Verifica valores nulos.

```sql
SELECT 
    nome,
    data_demissao
FROM tb_funcionario
WHERE data_demissao IS NULL;  -- Funcionários ativos
```

---

## 9. Funções de String

```sql
-- LENGTH - Comprimento da string
SELECT nome, LENGTH(nome) FROM tb_funcionario;

-- UPPER/LOWER - Converter maiúsculas/minúsculas
SELECT UPPER(nome), LOWER(nome) FROM tb_funcionario;

-- SUBSTRING - Extrair parte da string
SELECT SUBSTRING(cpf, 1, 3) FROM tb_funcionario;

-- TRIM - Remover espaços
SELECT TRIM(nome) FROM tb_funcionario;

-- REPLACE - Substituir texto
SELECT REPLACE(nome, 'Silva', 'Santos') FROM tb_funcionario;

-- CONCAT - Concatenar strings
SELECT CONCAT(nome, ' - ', cargo) FROM tb_funcionario;
```

---

## 10. Funções de Data

```sql
-- CURRENT_DATE/NOW - Data/hora atual
SELECT CURRENT_DATE, NOW();

-- DATE_PART - Extrair parte da data
SELECT DATE_PART('year', data_admissao) FROM tb_funcionario;

-- DATE_ADD/DATE_SUB - Adicionar/subtrair datas
SELECT DATE_ADD(data_admissao, INTERVAL 1 YEAR) FROM tb_funcionario;

-- DATEDIFF - Diferença entre datas
SELECT DATEDIFF(NOW(), data_admissao) AS dias_trabalhados FROM tb_funcionario;

-- DATE_FORMAT - Formatar data
SELECT DATE_FORMAT(data_admissao, '%d/%m/%Y') FROM tb_funcionario;
```

---

## 11. Índices

### 11.1 Criar Índice
```sql
-- Índice simples
CREATE INDEX idx_funcionario_departamento 
ON tb_funcionario(codigo_departamento);

-- Índice composto
CREATE INDEX idx_funcionario_depto_cargo 
ON tb_funcionario(codigo_departamento, codigo_cargo);

-- Índice único
CREATE UNIQUE INDEX uk_funcionario_email 
ON tb_funcionario(email);
```

### 11.2 Dropar Índice
```sql
DROP INDEX idx_funcionario_departamento;
```

---

## 12. Transações

### 12.1 ACID Properties
- **Atomicidade** - Tudo ou nada
- **Consistência** - Integridade dos dados
- **Isolamento** - Transações independentes
- **Durabilidade** - Dados persistem

### 12.2 BEGIN, COMMIT, ROLLBACK
```sql
BEGIN;  -- Inicia transação

UPDATE tb_funcionario 
SET salario = salario * 1.10 
WHERE codigo_departamento = 1;

-- Se houver erro:
ROLLBACK;  -- Desfaz alterações

-- Se tudo OK:
COMMIT;    -- Confirma alterações
```

### 12.3 SAVEPOINT
```sql
BEGIN;

INSERT INTO tb_funcionario VALUES (...);
SAVEPOINT sp1;

INSERT INTO tb_funcionario VALUES (...);
SAVEPOINT sp2;

-- Se segundo insert falhar:
ROLLBACK TO sp1;  -- Desfaz até sp1

COMMIT;  -- Confirma sp1
```

---

## 13. Procedures e Funções

### 13.1 Criar Função
```sql
CREATE FUNCTION calcular_idade(data_nasc DATE) RETURNS INT AS $$
BEGIN
    RETURN EXTRACT(YEAR FROM AGE(data_nasc));
END;
$$ LANGUAGE plpgsql;

SELECT nome, calcular_idade(data_nascimento) FROM tb_funcionario;
```

### 13.2 Criar Procedure
```sql
CREATE PROCEDURE aumentar_salario(p_departamento INT, p_percentual FLOAT)
AS $$
BEGIN
    UPDATE tb_funcionario
    SET salario = salario * (1 + p_percentual/100)
    WHERE codigo_departamento = p_departamento;
    
    COMMIT;
END;
$$ LANGUAGE plpgsql;

CALL aumentar_salario(1, 10);  -- Aumenta 10% no departamento 1
```

---

## 14. Triggers

### 14.1 Trigger para Auditoria
```sql
CREATE TABLE tb_auditoria (
    id SERIAL PRIMARY KEY,
    tabela VARCHAR(50),
    operacao VARCHAR(10),
    usuario VARCHAR(50),
    data_hora TIMESTAMP,
    dados_antigos TEXT,
    dados_novos TEXT
);

CREATE TRIGGER tr_audit_funcionario
AFTER INSERT OR UPDATE OR DELETE ON tb_funcionario
FOR EACH ROW
EXECUTE FUNCTION registrar_auditoria();
```

---

## 15. Views

### 15.1 Criar View
```sql
CREATE VIEW vw_funcionarios_por_departamento AS
SELECT 
    d.nome AS departamento,
    COUNT(f.id) AS total_funcionarios,
    AVG(f.salario) AS salario_medio,
    MAX(f.salario) AS maior_salario,
    MIN(f.salario) AS menor_salario
FROM tb_funcionario f
JOIN tb_departamento d ON f.codigo_departamento = d.id
GROUP BY d.id, d.nome;

-- Usar a view
SELECT * FROM vw_funcionarios_por_departamento;
```

### 15.2 Atualizar View
```sql
CREATE OR REPLACE VIEW vw_funcionarios_por_departamento AS
-- Nova definição
```

---

## 16. Normalização

### 16.1 Primeira Forma Normal (1NF)
- Eliminar grupos repetitivos
- Todos os atributos são atômicos

### 16.2 Segunda Forma Normal (2NF)
- Cumprir 1NF
- Remover dependências parciais
- Todos os atributos não-chave dependem da chave completa

### 16.3 Terceira Forma Normal (3NF)
- Cumprir 2NF
- Remover dependências transitivas
- Atributos não-chave não dependem uns dos outros

---

## 17. Otimização de Consultas

### 17.1 EXPLAIN
Mostra o plano de execução da consulta.

```sql
EXPLAIN
SELECT 
    f.nome,
    d.nome
FROM tb_funcionario f
JOIN tb_departamento d ON f.codigo_departamento = d.id
WHERE f.salario > 5000;
```

### 17.2 Boas Práticas
- Use índices em colunas frequentemente filtradas
- Evite SELECT * quando possível
- Use JOINs ao invés de subconsultas quando apropriado
- Evite funções em colunas de WHERE
- Use LIMIT quando buscando apenas alguns registros

---

## 18. Repositório - Estrutura e Conteúdo

Este repositório contém exemplos práticos de todos esses conceitos:

### Pastas Principais:
1. **1 - Modelo Conceitual** - Diagramas ER (Entity-Relationship)
2. **2 - Modelo Lógico Relacional** - Conversão para modelo relacional
3. **3 - Normalização** - Aplicação de formas normais
4. **4 - SQL DDL e DML** - Criação e manipulação de dados
5. **5 - Consultas SQL** - Exemplos de DQL avançadas

---

## 19. Próximos Passos

- Estudar otimização de performance
- Aprender sobre replicação e backup
- Explorar diferentes SGBD (PostgreSQL, MySQL, SQL Server)
- Implementar aplicações com ORM (Entity Framework, SQLAlchemy)
- Estudar data warehousing e analytics

