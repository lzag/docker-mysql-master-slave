Docker MySQL master-slave replication 
========================

MySQL 8 master-slave replication with Docker. 

## Run

To run this examples you will need to start containers with "docker compose up". The replication is set up automagically when the containers are started. 

#### Make changes to master

```bash
docker compose exec mysql_source sh -c 'mysql -p${MYSQL_ROOT_PASSWORD} db -e "INSERT INTO code VALUES (100), (200)"'
```

#### Read changes from replica

```bash
docker compose exec mysql_replica sh -c 'mysql -p${MYSQL_ROOT_PASSWORD} db -e "select * from code \G"'
```

## Troubleshooting

#### Check Logs

```bash
docker compose logs
```

#### Check master status

```bash
docker compose exec mysql_source sh -c 'mysql -p${MYSQL_ROOT_PASSWORD} -e "SHOW BINARY LOG STATUS \G"'
```

#### Check replica status

```bash
docker compose exec mysql_replica sh -c 'mysql -p${MYSQL_ROOT_PASSWORD} -e "SHOW REPLICA STATUS \G"'
```