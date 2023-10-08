# docker-postgres
docker-postgresql














# 
    mkdir -p /data/postgresql/data
    mkdir -p /data/postgresql/pgadmin


# docker-compose.yml

    version: '3.6'
    
    services:
      postgres:
        container_name: postgres
        image: postgres:10
        restart: unless-stopped
        environment:
          - POSTGRES_PASSWORD='비밀번호'
          - TZ=Asia/Seoul
        volumes:
          - /data/postgresql/data:/var/lib/postgresql/data
        ports:
          - "5432:5432"
    
      pgadmin:
        container_name: pgadmin
        image: dpage/pgadmin4
        restart: unless-stopped
        ports:
          - "5555:80"
        volumes:
          - /data/postgresql/pgadmin:/var/lib/pgadmin
        environment:
          - PGADMIN_DEFAULT_EMAIL=ducj@pgadmin.com
          - PGADMIN_DEFAULT_PASSWORD=비밀번호
          - TZ=Asia/Seoul
        depends_on:
          - postgres
