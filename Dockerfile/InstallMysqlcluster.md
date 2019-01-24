# Mysql cluster
## Create network
docker network create cluster --subnet=192.169.0.0/16
docker network create -d overlay nginx-net-2
docker network create -d overlay mysqlcluster

"Subnet": "10.0.13.0/24"
"Gateway": "10.0.13.1"
docker run -d --net=cluster --name=management1 --ip=192.168.0.2 mysql/mysql-cluster ndb_mgmd
docker run -d --net=cluster --name=management1 --ip=192.169.0.2 mysql/mysql-cluster:7.6 ndb_mgmd



docker run -d --net=cluster --name=ndb1 --ip=192.169.0.3 mysql/mysql-cluster:7.6 ndbd
docker run -d --net=cluster --name=ndb2 --ip=192.169.0.4 mysql/mysql-cluster:7.6 ndbd


docker run -d --net=cluster --name=mysql1 --ip=192.169.0.10 -e MYSQL_RANDOM_ROOT_PASSWORD=true mysql/mysql-cluster:7.6 mysqld













docker service create -d --network=mysqlcluster --name=management1 -p 30000:3306 mysql/mysql-cluster ndb_mgmd

docker service create -d --network=mysqlcluster --name=ndb1 -p 30000:3306 mysql/mysql-cluster ndbd
docker service create -d --network=mysqlcluster --name=ndb2 -p 30000:3306 mysql/mysql-cluster ndbd

docker service create -d --network=mysqlcluster --name=mysql -p 30000:3306 -e  MYSQL_RANDOM_ROOT_PASSWORD=true mysql/mysql-cluster mysqld

docker logs mysql1 2>&1 | grep PASSWORD

docker exec -it mysql1 mysql -uroot -p

ALTER USER 'root'@'localhost' IDENTIFIED BY 'MyNewPass';

docker run -it --net=cluster mysql/mysql-cluster ndb_mgm

Starting ndb_mgm
-- NDB Cluster -- Management Client --
ndb_mgm> show
