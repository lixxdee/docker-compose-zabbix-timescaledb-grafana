<code>git clone https://github.com/lixxdee/docker-compose-zabbix-timescaledb-grafana.git</code> - download project.

<code>cd docker-compose-zabbix-timescaledb-grafana</code> - go to directory with docker-compose.yml file.

<code>docker-compose up -d</code> - build containers.

<code>docker ps -a</code> - make sure all containers are is running.

<code>docker inspect zabbix-agent | grep "IPAddress\\": "</code> - received ip address you need change in web interface Zabbix server instead of '127.0.0.1', or just insert <code>zabbix-agent</code> in DNS name.

<code>docker restart zabbix-agent</code> - restart zabbix-agent container.

Grafana will be available by http://YourIP:3000/, default login:admin, password:admin.

Enjoy! :)

Example other option config grafana with SSL and local installed grafana-zabbix-app-plugin:

    container_name: grafana
    image: grafana/grafana
    networks:
      - network-zabbix
    restart: always
    ports:
      - '3000:3000'
    environment:
      - GF_INSTALL_PLUGINS=alexanderzobnin-zabbix-app // default method app install;  You need choice one option!!!
      - GF_INSTALL_PLUGINS=/home/username/alexanderzobnin-zabbix-app-4.2.4.zip;alexanderzobnin-zabbix-app //local method app install; You need choice one option!!!
      - GF_SERVER_PROTOCOL=https
      - GF_SERVER_CERT_FILE=/etc/ssl/nginx/ssl.crt
      - GF_SERVER_CERT_KEY=/etc/ssl/nginx/ssl.key
    volumes:
      - /etc/ssl/nginx:/etc/ssl/nginx:ro
      - /home/username:/home/username
    links:
      - zabbix-web
    depends_on:
      - zabbix-web
For Zabbix SSL you just need copy DHPARAM.PEM, SSL.CRT and SSL.KEY into to <code> /etc/ssl/nginx</code> and make chmod 644.
