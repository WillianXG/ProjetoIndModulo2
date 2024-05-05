# Sistema RESILIADATA

Este projeto é um sistema para auxiliar na avaliação de quais tecnologias as empresas parceiras estão utilizando e quem são seus colaboradores. Este README descreve as entidades, campos, relacionamentos e exemplos de registros. O banco de dados é modelado para o PostgreSQL.

---

## Entidades e Campos

O sistema RESILIADATA contém as seguintes entidades:

### Empresa
- Campos:
  - `id`: `SERIAL`, chave primária, auto-incremento
  - `nome`: `VARCHAR(100)`, não nulo
  - `setor`: `VARCHAR(100)`, não nulo
- Descrição: Representa empresas parceiras.

### Tecnologia
- Campos:
  - `id`: `SERIAL`, chave primária, auto-incremento
  - `nome`: `VARCHAR(100)`
  - `area`: `VARCHAR(100)`
- Descrição: Representa diferentes tecnologias utilizadas pelas empresas parceiras.

### Colaborador
- Campos:
  - `id`: `SERIAL`, chave primária, auto-incremento
  - `nome`: `VARCHAR(100)`, não nulo
  - `cargo`: `VARCHAR(100)`
  - `id_empresa`: `INT`
- Chaves Estrangeiras:
  - `id_empresa` refere-se a `Empresa(id)`
- Descrição: Representa colaboradores das empresas parceiras.

### UsoTecnologia
- Campos:
  - `id`: `SERIAL`, chave primária, auto-incremento
  - `id_empresa`: `INT`
  - `id_tecnologia`: `INT`
- Chaves Estrangeiras:
  - `id_empresa` refere-se a `Empresa(id)`
  - `id_tecnologia` refere-se a `Tecnologia(id)`
- Descrição: Relaciona empresas com as tecnologias que utilizam.

---

## Relacionamentos

- A tabela **Empresa** tem um relacionamento de muitos-para-um com **Colaborador**.
- A tabela **UsoTecnologia** é uma tabela de relacionamento entre **Empresa** e **Tecnologia**, indicando quais tecnologias as empresas estão utilizando.

---

## Simulação de Dados

Exemplos de registros para cada entidade:

### Empresa
- Registro 1: `(1, "Tech Solutions Ltda", "Tecnologia")`
- Registro 2: `(2, "Innovatech Corp.", "Inovação")`

### Tecnologia
- Registro 1: `(1, "ReactJS", "Desenvolvimento Web")`
- Registro 2: `(2, "Python", "Análise de Dados")`

### Colaborador
- Registro 1: `(1, "João Silva", "Desenvolvedor", 1)`  // João trabalha na Tech Solutions
- Registro 2: `(2, "Maria Souza", "Analista de Dados", 2)`  // Maria trabalha na Innovatech

### UsoTecnologia
- Registro 1: `(1, 1, 1)`  // Tech Solutions usa ReactJS
- Registro 2: `(2, 2, 2)`  // Innovatech usa Python

---

## Instruções para Executar o SQL

Para criar as tabelas e definir as relações no PostgreSQL, use os seguintes comandos SQL:

```sql
CREATE TABLE Empresa 
( 
  id SERIAL PRIMARY KEY,  
  nome VARCHAR(100) NOT NULL,  
  setor VARCHAR(100) NOT NULL
);

CREATE TABLE Tecnologia 
( 
  id SERIAL PRIMARY KEY,  
  nome VARCHAR(100),  
  area VARCHAR(100)
);

CREATE TABLE Colaborador 
( 
  id SERIAL PRIMARY KEY,  
  nome VARCHAR(100) NOT NULL,  
  cargo VARCHAR(100),  
  id_empresa INT,
  FOREIGN KEY (id_empresa) REFERENCES Empresa(id)
);

CREATE TABLE UsoTecnologia 
( 
  id SERIAL PRIMARY KEY,  
  id_empresa INT,
  id_tecnologia INT,
  FOREIGN KEY (id_empresa) REFERENCES Empresa(id),
  FOREIGN KEY (id_tecnologia) REFERENCES Tecnologia(id)
);
