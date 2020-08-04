# docker-compose
- docker-compose -f docker-compose.yml up -d

- 文章參照 https://www.cnblogs.com/python-gm/p/12843653.html

# influxdb時序性資料庫
- 連接libreNMS的主機資訊，並透過influxdb來媒介，最後呈現到grafana上面
- docker run -d -p 8083:8083 -p 8086:8086 -p 8090:8090 -p 8099:8099 --name influxsrv -e INFLUXDB_ADMIN_USER=librenms -e INFLUXDB_ADMIN_PASSWORD=password tutum/influxdb
