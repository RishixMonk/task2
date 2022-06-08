1.Intially we were using sqlite3 databas,here i used postgres database by using its image from dockerhub.

2.We have two containers,one from our first task and now postgres container and dockerhub provides a network where 2 containers can talk to each other. But in first container had to do some changes like: i)add 'pg' gem to gem file and running bundle install

3.I used a docker-compose file but it can be even done by i)create a docker network ii)run two containers by specifying port numbers and required environment variables.

4.In database.yml file changing development mode to url: <%= ENV['DATABASE_URL'] %> which will run on mentioned database url but since here we are using postgre container and url will be 'DATABASE_URL=postgres://postgres:postgres@db:5432' which we mention in docker-compose file.

5.Now for port numbers,postgres by default is 5432,but for webapp to listen on localhost at 8080 we have to mention in docker-compose file under app service ports:"8080:3000" which will do the work.

6.Then we run docker-compose build and run docker-compose up which will work and can be seen by going to localhost:8080 on browser.
