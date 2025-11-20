# DevSuperior Banco de Dados SQL

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
![SQL](https://img.shields.io/badge/SQL-✓-blue.svg)
![Database Design](https://img.shields.io/badge/Database%20Design-✓-green.svg)

Repositório completo com materiais de aprendizado sobre banco de dados e SQL, desenvolvido durante o curso **Fundação de Programação** da **DevSuperior**.

---

## 📚 Sobre Este Repositório

Este repositório contém uma documentação abrangente e exemplos práticos sobre:

- **Modelagem de Dados** - Conceitual, Lógico e Relacional
- **Normalização de Banco de Dados** - 1NF, 2NF, 3NF
- **SQL DDL** - Criação e alteração de estruturas
- **SQL DML** - Inserção, atualização e deleção de dados
- **SQL DQL** - Consultas e análises complexas
- **Projetos Práticos** - Casos de uso reais

## 🎯 Conteúdo Principal

### 📁 Estrutura do Repositório

```
DevSuperiorBancoDeDadosSQL/
│
├── FUNDAMENTOS_SQL.md                    # Conceitos básicos de SQL
├── CONCEITOS_SQL_AVANCADO.md             # Tópicos avançados
├── README.md                              # Este arquivo
├── TABLEcurso.sql                        # Exemplo inicial
│
├── 1 - Modelo Conceitual/
│   ├── 1 - Atividade/                    # Exercícios básicos de modelagem
│   │   ├── 1 - Albuns Musicais.asta
│   │   ├── 2 - Campeonato de Handebol.asta
│   │   ├── 3 - Redes Sociais.asta
│   │   ├── 4 - Evento Academico.asta
│   │   └── 5 - Turismo.asta
│   │
│   ├── 2 - Atividade/                    # Exercícios intermediários
│   │   ├── 1 - Locação.asta
│   │   ├── 2 - Academico.asta
│   │   └── 3 - Blibioteca.asta
│   │
│   └── 3 - Atividade/                    # Exercícios avançados
│       ├── 1 - Locadora de Auto.asta
│       ├── 2 - Sistema de Pedido.asta
│       └── 3 - Companhia Aera.asta
│
├── 2 - Modelo Logico Relacional/
│   ├── Diagrama Modelo Relacional.drawio
│   └── Exercicios/
│
├── 3 - Normalização/
│   └── Exercicios/
│
├── 4 - SQL DDL e DML/
│   └── Exercicio/
│       ├── SQL-DDL-Exercicio-Carros.sql
│       ├── SQL-DDL-Exercicio-ESCOLA.sql
│       ├── SQL-DDL-Exercicio-Evento-Academico.sql
│       ├── SQL-DDL-Exercicio-Evento.sql
│       ├── SQL-DDL-Exercicio-Rede-Social.sql
│       ├── SQL-DDL.sql
│       ├── SQL-DML-Exercicio-Carros.sql
│       ├── SQL-DML-Exercicio-ESCOLA.sql
│       ├── SQL-DML-Exercicio-Evento-Academico-PostGre.sql
│       ├── SQL-DML-Exercicio-Evento-Academico.sql
│       ├── SQL-DML-Exercicio-Evento-PostGre.sql
│       ├── SQL-DML-Exercicio-Evento.sql
│       ├── SQL-DML-Exercicio-Rede-Social.sql
│       └── SQL-DML.sql
│
└── 5 - Consultas SQL/
    └── Exercicios/
        └── DevSuperior-Consultas-em-SQL/
            ├── Exercicio-DDL-Exemplo-Empregados.sql
            ├── Exercicio-DML-Exemplo-Empregados.sql
            ├── Exercicio-DQL-Exemplo.sql
            ├── Exercicios.sql
            ├── README.md
            └── Script dos Exercicios/
                ├── 2602.sql
                ├── 2603.sql
                ├── ... (scripts até 3001.sql)
                └── 3001.sql
```

---

## 🚀 Como Usar Este Repositório

### Pré-requisitos

- Um SGBD instalado (PostgreSQL, MySQL, SQL Server ou semelhante)
- Um editor de texto ou IDE com suporte a SQL
- Conhecimento básico de conceitos de banco de dados

### Passos Recomendados

#### 1️⃣ **Comece Pelos Fundamentos**
Leia o arquivo `FUNDAMENTOS_SQL.md` para entender:
- Conceitos básicos de SQL
- Tipos de dados
- DDL, DML e DQL
- Restrições e relacionamentos

#### 2️⃣ **Estude Modelagem de Dados**
Explore a pasta **1 - Modelo Conceitual** para:
- Entender diagramas Entidade-Relacionamento (ER)
- Ver exemplos práticos de diferentes domínios
- Aprender a estruturar bancos de dados

#### 3️⃣ **Aprenda Normalização**
Acesse a pasta **3 - Normalização** para:
- Compreender Formas Normais (1NF, 2NF, 3NF)
- Evitar redundância de dados
- Otimizar estrutura das tabelas

#### 4️⃣ **Pratique com DDL e DML**
Estude a pasta **4 - SQL DDL e DML** para:
- Criar tabelas com `CREATE TABLE`
- Inserir dados com `INSERT`
- Atualizar dados com `UPDATE`
- Remover dados com `DELETE`

#### 5️⃣ **Domine Consultas SQL**
Trabalhe com a pasta **5 - Consultas SQL** para:
- Fazer consultas básicas com `SELECT`
- Aprender JOINs e subconsultas
- Usar funções de agregação
- Resolver problemas complexos

#### 6️⃣ **Aprofunde em Conceitos Avançados**
Leia `CONCEITOS_SQL_AVANCADO.md` para:
- Window Functions
- Common Table Expressions (CTEs)
- Triggers e Procedures
- Otimização de queries

---

## 📖 Documentação Incluída

### FUNDAMENTOS_SQL.md
Documento que cobre:
- O que é SQL
- Conceitos básicos (tabelas, colunas, linhas)
- Tipos de dados
- DDL, DML e DQL
- Restrições (PRIMARY KEY, FOREIGN KEY, NOT NULL, etc.)
- Operações CRUD
- Estrutura de SELECT
- Relacionamentos entre tabelas
- Boas práticas

### CONCEITOS_SQL_AVANCADO.md
Documento que abrange:
- JOINs (INNER, LEFT, RIGHT, FULL OUTER, CROSS, SELF)
- Funções de agregação
- GROUP BY e HAVING
- Subconsultas
- UNION e UNION ALL
- Window Functions
- Common Table Expressions (CTEs)
- Operadores especiais
- Funções de string e data
- Índices
- Transações
- Procedures e Funções
- Triggers
- Views
- Normalização
- Otimização de consultas

---

## 🎓 Tópicos Abordados

### Modelo Conceitual
Desenvolvimento de diagramas entidade-relacionamento para diferentes domínios:
- **Álbuns Musicais** - Armazenamento de coleções musicais
- **Campeonato de Handebol** - Gestão de competições esportivas
- **Redes Sociais** - Conexões entre usuários
- **Evento Acadêmico** - Organização de eventos educacionais
- **Turismo** - Gestão de destinos e reservas
- **Locação** - Sistemas de aluguel
- **Biblioteca** - Gestão de acervos e empréstimos
- **Locadora de Auto** - Gerenciamento de frotas
- **Sistema de Pedido** - E-commerce
- **Companhia Aérea** - Reservas e voos

### Modelo Lógico Relacional
Conversão de modelos conceituais para o modelo relacional com relacionamentos 1:1, 1:N e N:N.

### Normalização
Aplicação de Formas Normais para otimizar estruturas de dados e eliminar anomalias.

### SQL DDL (Data Definition Language)
Exemplos de:
- `CREATE TABLE`
- `ALTER TABLE`
- `DROP TABLE`
- Definição de constraints

### SQL DML (Data Manipulation Language)
Exemplos de:
- `INSERT INTO`
- `UPDATE`
- `DELETE`
- Operações em múltiplas tabelas

### SQL DQL (Data Query Language)
Exemplos de:
- `SELECT` simples e complexas
- `WHERE`, `ORDER BY`, `GROUP BY`
- `JOINs` e subconsultas
- Funções de agregação
- Filtros e condições avançadas

---

## 📊 Exemplo de Exercício

### Criar uma tabela de Cursos
```sql
CREATE TABLE tbCurso (
    id SERIAL PRIMARY KEY,
    nome VARCHAR(20) NOT NULL,
    cargaHoraria INT,
    valor FLOAT,
    notaPrevista FLOAT,
    notaMinima FLOAT
);
```

### Inserir dados
```sql
INSERT INTO tbCurso (nome, cargaHoraria, valor, notaPrevista, notaMinima)
VALUES ('SQL Avançado', 40, 500.00, 7.0, 5.0);
```

### Consultar dados
```sql
SELECT 
    nome,
    cargaHoraria,
    valor
FROM tbCurso
WHERE cargaHoraria > 30
ORDER BY valor DESC;
```

---

## 🔧 Ferramentas Recomendadas

### Modelagem
- **StarUML** - Para criar diagramas ER (arquivos .asta)
- **Draw.io** - Para diagramas relacionais (arquivos .drawio)
- **DBeaver** - Visualização de esquemas

### Execução de SQL
- **PostgreSQL** - Recomendado para exercícios (alguns usam sintaxe PostgreSQL)
- **MySQL** - Alternativa com sintaxe similar
- **SQLite** - Leve, ideal para práticas
- **DBeaver** - IDE visual
- **pgAdmin** - Gerenciador PostgreSQL
- **MySQL Workbench** - Gerenciador MySQL

### Editores de Código
- **VS Code** - Com extensões SQL
- **DataGrip** - IDE profissional
- **Sublime Text** - Editor leve

---

## 📝 Scripts Inclusos

### DDL (Data Definition Language)
- `SQL-DDL.sql` - Exemplo básico de DDL
- `SQL-DDL-Exercicio-*.sql` - Exercícios para diferentes domínios

### DML (Data Manipulation Language)
- `SQL-DML.sql` - Exemplo básico de DML
- `SQL-DML-Exercicio-*.sql` - Exercícios com diferentes datasets
- `SQL-DML-Exercicio-*-PostGre.sql` - Variações para PostgreSQL

### DQL (Data Query Language)
- `Exercicio-DQL-Exemplo.sql` - Exemplos de consultas
- `2602.sql` até `3001.sql` - 40+ exercícios de consultas

---

## 💡 Dicas de Aprendizado

### Para Iniciantes
1. Comece com exemplos simples de CREATE TABLE
2. Pratique INSERT, UPDATE e DELETE com dados pequenos
3. Faça consultas SELECT básicas
4. Aos poucos, adicione WHERE, ORDER BY, GROUP BY
5. Estude JOINs e relacionamentos

### Para Intermediários
1. Explore subconsultas
2. Estude funções de agregação
3. Aprenda sobre índices
4. Pratique otimização de queries
5. Explore diferentes tipos de JOINs

### Para Avançados
1. Implemente CTEs recursivas
2. Use Window Functions
3. Crie Triggers e Procedures
4. Estude transações ACID
5. Otimize queries grandes

---

## 🎯 Casos de Uso

Este repositório contém exemplos de modelagem para:

- **E-commerce** - Sistema de pedidos
- **Gestão de RH** - Funcionários e departamentos
- **Educação** - Alunos, turmas e cursos
- **Bibliotecas** - Livros e empréstimos
- **Transportes** - Companhias aéreas e voos
- **Diversão** - Redes sociais e coleções musicais
- **Negócios** - Vendas e clientes

---

## 📚 Progressão de Aprendizado

```
┌─────────────────────────────────────────────────────────┐
│  Iniciante                                              │
│  • Fundamentos de SQL                                   │
│  • Tipos de dados                                       │
│  • Operações CRUD básicas                               │
└────────────────┬────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────┐
│  Intermediário                                          │
│  • Normalização                                         │
│  • JOINs múltiplos                                      │
│  • Agregações e GROUP BY                                │
│  • Subconsultas                                         │
└────────────────┬────────────────────────────────────────┘
                 │
┌────────────────▼────────────────────────────────────────┐
│  Avançado                                               │
│  • Window Functions                                     │
│  • CTEs recursivas                                      │
│  • Triggers e Procedures                                │
│  • Otimização de performance                            │
│  • Transações complexas                                 │
└─────────────────────────────────────────────────────────┘
```

---

## 🤝 Contribuindo

Este repositório foi criado como material de aprendizado. Se você tem sugestões de melhorias ou correções:

1. Identifique a área de melhoria
2. Documente-a claramente
3. Sugira alterações ou correções

---

## 📄 Licença

Este projeto está sob a licença MIT. Veja o arquivo LICENSE para mais detalhes.

---

## 👨‍💼 Autor

**Gabriel Sales David**
- Estudante de Fundação de Programação - DevSuperior
- Foco em Banco de Dados e SQL

---

## 📞 Contato & Suporte

Para dúvidas sobre SQL ou banco de dados:

1. Consulte a documentação incluída (`FUNDAMENTOS_SQL.md`, `CONCEITOS_SQL_AVANCADO.md`)
2. Execute os exemplos do repositório
3. Pratique com os exercícios propostos

---

## 🔗 Recursos Externos

### Documentação Official
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [MySQL Reference Manual](https://dev.mysql.com/doc/)
- [SQL Server Documentation](https://docs.microsoft.com/en-us/sql/)

### Aprendizado
- [DevSuperior](https://devsuperior.com.br/) - Plataforma do curso
- [W3Schools SQL Tutorial](https://www.w3schools.com/sql/)
- [Modo SQL Online](https://www.sqlline.com/)

### Ferramentas
- [DBeaver Community](https://dbeaver.io/)
- [pgAdmin 4](https://www.pgadmin.org/)
- [Draw.io](https://www.draw.io/)

---

## ✨ Destaques

✅ **Cobertura Completa** - Do básico ao avançado
✅ **Exemplos Práticos** - Casos de uso reais
✅ **Documentação Detalhada** - Guias de aprendizado
✅ **Exercícios** - 40+ scripts de exercícios
✅ **Múltiplos Domínios** - Diferentes casos de negócio
✅ **Bem Organizado** - Estrutura lógica e clara

---

## 🎓 Objetivo de Aprendizado

Ao completar este repositório, você será capaz de:

- ✅ Projetar banco de dados relacionais eficientes
- ✅ Criar e gerenciar tabelas com SQL DDL
- ✅ Inserir e modificar dados com SQL DML
- ✅ Escrever consultas complexas com SQL DQL
- ✅ Aplicar normalização de dados
- ✅ Otimizar queries para performance
- ✅ Usar funções avançadas de SQL
- ✅ Resolver problemas de negócio com dados

---

**Última Atualização:** Novembro de 2025

*Desenvolvido como parte do curso Fundação de Programação - DevSuperior*

