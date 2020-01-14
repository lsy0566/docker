# Swarm 설정

- docker-compose up
- docker ps (registry, manager, worker01, worker02, worker03)
- docker exec -it manager
  - (m)$ docker swarm init (-> join token 생성 됨)
- docker exec -it worker01 sh (worker02, 03에서도 실행)
  - (w1)$ docker swarm join (with join token)
- docker exec -it manager sh
  - (m)$ docker node ls (worker01~03, manager 확인)
  - (m)$ docker network create --driver=overlay --attachable todoapp
  - (m)$ docker stack deploy -c /stack/visualizer.yml visualizer
  - (m)$ docker stack deploy -c /stack/todo-mysql.yml todo_mysql
- docker exec -t worker01 (or worker02, worker03) sh -> MASTER DB 접속
  - ex, w1) docker exec -it [MASTER DB Container] bash
  - ex, w1, MASTER Container) $ init-data.sh
  - ex, w1, MASTER Container) $ mysql -uroot -p tododb
  - ex, w1, MASTER Container) mysql> select *from todo;
- docker push localhost:5000/ch04/todoapi:latest