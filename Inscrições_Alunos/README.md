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







