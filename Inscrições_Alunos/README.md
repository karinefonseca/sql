# Inscrições de Alunos para Universidades

Neste projeto faço diversas consultas à seguinte base de dados utilizando os principais comandos do SQL: SELECT, DELETE, DROP, INSERT, UPDATE, RIGHT JOIN, LEFT JOIN e INNER JOIN. Bem como os comandos: GROUP BY, ORDER BY, COUNT, MIN, MAX e tratamento de campos NULL.

![Inscrições de Alunos em Universidades (EDX-Stanford) - Diagrama ER de banco de dados (pé de galinha)](https://user-images.githubusercontent.com/98848529/184547164-6c997c11-1d80-431f-a49a-68dcf93e655c.jpeg)

Antes de irmos para a análise dos dados presentes na tabela, vamos entender a estrutura dessa base de dados. 

## Análise dos Dados

Vamos observar, a seguir, alguns dados presentes nas tabelas para nos familiarizarmos com as consultas que serão realizadas. Lembrando que as imagens mostram **apenas parte do banco**. 

### Tabela Student

Na tabela Student temos o ID do estudante (sID), o nome (sName), o GPA (Grade Point Average) que é a média geral que o aluno obtém ao longo do high school (equivalente ao ensino médio) e esse valor é utilizado para o ingresso nas faculdades americanas e sizeHS que é o tamanho da escola (sizeHS) onde o aluno fez o ensino médio (tamanho em número de estudantes dessa escola). 

![image](https://user-images.githubusercontent.com/98848529/184548122-1cd5cb39-b83f-4d59-b622-bab43b1563b5.png)


### Tabela College
Na tabela College temos o nome do College (universidade), o state (estado aonde essa universidade está) e o enrollment que se trata do número de inscrições.

![image](https://user-images.githubusercontent.com/98848529/184548220-e3ea8169-4020-45e6-965a-052ed2091515.png)


### Tabela Apply
Na tabela Aplly temos a relação dos estudantes com as universidades. Temos o ID do estudante (sID), o nome da Universidade (cName), o nome do curso superior (major) e a decisão (decision) onde definimos se um estudante foi ou não aceito (Y para sim e N para não).

![image](https://user-images.githubusercontent.com/98848529/184548476-0daf463d-4d9e-458b-a299-72542c6b8f2c.png)

# Consultas (Queries)

## SELECT

 **Todos os IDs e nomes dos alunos com GPA > 3.6**

  - **SELECT** sID, sName **FROM** Student **WHERE** GPA > 3.6;

**Nomes dos estudantes e dos cursos para os quais eles se inscreveram**

  - **SELECT** sName, major **FROM** Student, Apply **WHERE** Student.sID = Apply.sID;

**Nomes e GPAs dos studantes em escolas menores que 1000 (menos de 1000 alunos) que se inscreveram para o curso de Ciência da COmputação (CS) na faculdade de Staford e a decisão.**

- **SELECT** sName, GPA, decision **FROM** Student, Apply **WHERE** Student.sID = Apply.sID and sizeHS < 1000 and major = 'CS' and cname = 'Stanford';
  
 **Alunos que se inscreveram em cursos superiores na área de bio** 

- **SELECT** sID, major **FROM** Apply **WHERE** major like '%bio%';

**Adicionando uma escala para o CPA baseado no sizeHS**
- **SELECT** sID, sName, GPA, sizeHS, GPA*(sizeHS/1000.0) as scaledGPA **FROM** Student;


## Subqueries no WHERE

**Nomes dos alunos que se inscreveram para CS (Computer Science)**
- **SELECT** sName **FROM** Student **WHERE** sID in (**SELECT** sID **FROM** Apply **WHERE** major = 'CS');


**Alunos que não são da menor escola (menor sizeHS)**

**select** sID, sName, sizeHS **FROM** Student S1 **WHERE** exists (**SELECT** * **FROM** Student S2 **WHERE** S2.sizeHS < S1.sizeHS);

## 














