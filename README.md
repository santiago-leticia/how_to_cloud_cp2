# how_to_cloud_cp2

- Feito por: Leticia Santiago e Silva
- RM: 565799

<h2>Tecnologia: </h2>

- Java
- Docker
- Mave
- MySQL 8

<h2>Primeiro passo abaixar o git dentro de sua vm</h2>

- SQL
git clone https://github.com/santiago-leticia/sqlMusica.git

- java
 git clone https://github.com/santiago-leticia/projeto_musica_sql.git
 
<h2>Segundo passo Docker containers</h2>

<h3>Primeira parte - sql</h3>
docker network create redeCp2

<h4>Mysql: </h4>
docker pull mysql:8.0

<h4>Volume: </h4>
docker volume create mysql-dimdim-data

<h4>container</h4>

docker run --name rm565799_sqlMusica -d \
--network redeCp2 \
-e MYSQL_ROOT_PASSWORD=1234 \
-e MYSQL_DATABASE=db_dimdim \
-e MYSQL_USER=leticia \
-e MYSQL_PASSWORD=2345 \
-p 3306:3306 \
-v mysql-dimdim-data:/var/lib/mysql \
mysql:8.0

<h3>Segunda parte - java ou Maven</h3>

<h4>Entrar na pasta</h4>

cd projeto_musica_sql

<h4>Criar imagem</h4>
docker build -t projeto_musica_sql.

<h4>container</h4>

docker run --name rm565799_projeto_musica -d \
-v $(pwd):/app \
-w /app \
--network redeCp2 \
-p 8080:8080 \
-e SPRING_DATASOURCE_URL=jdbc:mysql://sqlMusica:3306/db_dimdim \
-e SPRING_DATASOURCE_USERNAME=leticia \
-e SPRING_DATASOURCE_PASSWORD=2345 \
maven:3.9-eclipse-temurin-17 \
bash -c "mvn clean package -DskipTests && java -jar target/*.jar"


# Na aplicação:

<h2>Dica doque voce pode fazer na aplicação </h2>

<h3>SQL</h3>
- Para entrar na sql
Exemplo:

docker exec -it sqlMusica mysql-u leticia -p
apos disso adicionar a sua senha: 
exemplo 2345

<h3>Exemplos de comandos</h3>
SELECT * FROM musica;

UPDATE musica SET titulo='Tempo Pedido' WHERE id=1;

INSERT INTO musica (fk_artista,titulo,data_lancamento,duracao,genero) VALUES(1,'Bad Romance','2009-10-19,'Pop');


<h3>Java</h3>

- No postman

buscar por id: 
http://localhost:8080/musicas/5

Paginação:
http://localhost:8080/musicas/paginadas?page=0&size=2

delete:
http://localhost:8080/musicas/5









