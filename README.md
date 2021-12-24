git clone https://github.com/lixxdee/docker-compose-zabbix-timescaledb-grafana.git

cd docker-compose-zabbix-timescaledb-grafana

docker-compose up -d

docker ps -a

docker inspect zabbix-agent | grep "IPAddress\\": " /// this is ip address you need change in web interface zabbix server.

docker stop/start

docker-compose up -d // build or rebuild docker-compose.yml
