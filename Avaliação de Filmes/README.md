# Avaliação de Filmes

O presente projeto faz parte da lista de exercícios do curso Databases: Relational Databases and SQL da Universidade de Stanford. Aqui temos a seguinte base de dados (o gráfico de entidade relacionamento foi elaborado por mim no software LucidChart) e temos que responder 8 questões. A análise da base de dados, as perguntas e as respostas (queries) estão descritas a seguir.

![image](https://user-images.githubusercontent.com/98848529/184564830-9110a0cb-ea35-4337-ac34-9835e0e288d6.png)

## Análise dos Dados

Vamos observar, a seguir, as tabelas presentes no banco de dados.

### Tabela Movie

Na tabela Movie temos o ID do filme (mID), o título (title), o ano de lançamento (year) e o nome do diretor (director).

![image](https://user-images.githubusercontent.com/98848529/184565104-a3c475c6-00d9-4698-9ab8-19dcd0bdea4c.png)


### Tabela Reviewer
Na tabela Reviewer temos o ID do avaliador (rID) e o nome do avaliador (name) 

![image](https://user-images.githubusercontent.com/98848529/184565323-737770a1-a163-4bbe-b788-2fd55812d925.png)


### Tabela Rating
Na tabela Rating temos a relação dos avaliadores com os filmes avaliados. Temos o ID do avaliador (rID), o ID do filme (mID), número de estrelas dada ao filme (stars) e a data da avaliação (ratingDate)

![image](https://user-images.githubusercontent.com/98848529/184565291-dddc3148-d5d6-45ab-b031-292ec7ff47e2.png)

## Consultas (Queries)

Ao todo temos que responder 8 questões. As respostas são as queries que tive que elaborar para retornar os dados desejados.

**1. Ache os títulos de filmes dirigidos por Steven Spielberg**
- SELECT title FROM Movie WHERE director = "Steven Spielberg"

**2. Ache todos os anos que um filme recebeu um rating de 4 ou 5 estrelas, e os ordene em ordem crescente**
- SELECT distinct year FROM Movie inner join Rating using (mID) WHERE stars > 3 order by year

**3. Ache os títulos de todos os filmes que não tiveram avaliações**
- SELECT distinct title FROM Movie, Rating WHERE Movie.mID not in (SELECT mID FROM Rating intersect SELECT mID FROM Movie)

**4. Alguns avaliadores não forneceram uma data com sua classificação. Encontre os nomes de todos os revisores que têm avaliações com valor NULL para a data.**
- SELECT distinct name FROM Reviewer inner join Rating using (rID) WHERE ratingDate is null

**5. Escreva uma consulta para retornar os dados de classificação em um formato mais legível: nome do revisor, título do filme, estrelas e data de classificação. Além disso, classifique os dados, primeiro pelo nome do revisor, depois pelo título do filme e, por último, pelo número de estrelas.**
- SELECT name, title, stars, ratingDate FROM Reviewer, Movie, Rating WHERE Movie.mID = Rating.mID and Reviewer.rID = Rating.rID order by name,title,stars

**6. Para todos os casos em que o mesmo revisor avaliou o mesmo filme duas vezes e deu uma classificação mais alta na segunda vez, retorne o nome do revisor e o título do filme.**
- SELECT name, title FROM Movie, Reviewer, Rating as R2, Rating as R1 WHERE R1.rID = R2.rID and R1.mID = R2.mID and R1.stars < R2.stars and R1.ratingDate < R2.ratingDate and R1.rID = Reviewer.rID and R1.mID = Movie.mID

**7. Para cada filme que tenha pelo menos uma classificação, encontre o maior número de estrelas que o filme recebeu. Retorna o título do filme e o número de estrelas. Classificar por título do filme.**
- SELECT title, max(stars) from Rating, Movie Where Rating.mID = Movie.mID group by Rating.mID order by (title)

**8. Para cada filme, retorne o título e o 'rating spread', ou seja, a diferença entre as classificações mais altas e mais baixas atribuídas a esse filme. Classifique por classificação espalhada do maior para o menor e, em seguida, pelo título do filme.**
- SELECT title, (max(stars) - min(stars)) as spread FROM Rating, Movie WHERE  Rating.mID = Movie.mID GROUP BY Rating.mID ORDER BY spread DESC, title


