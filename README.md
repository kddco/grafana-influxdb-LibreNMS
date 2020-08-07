# docker-compose
- docker-compose -f docker-compose-bridge.yml up -d

- 文章參照 https://www.cnblogs.com/python-gm/p/12843653.html

# influxdb時序性資料庫
- 連接libreNMS的主機資訊，並透過influxdb來媒介，最後呈現到grafana上面
## 建立influxdb的Container
- docker run -d -p 8083:8083 -p 8086:8086 --name influxsrv -e INFLUXDB_ADMIN_USER=librenms -e INFLUXDB_ADMIN_PASSWORD=password tutum/influxdb
## 到LibreNMS開啟外部整合
### 全域設定
![](https://i.imgur.com/hLRu9HQ.png)
### 輪詢器
![](https://i.imgur.com/F9GhKCP.png)
### InfluxDB 
 ![](https://i.imgur.com/LqI5EYR.png)
### 設定連接API
![](https://i.imgur.com/Qk4v5LH.png)
### 在influxdb上建立librenms資料庫
- 先到influxdb網頁管理頁面 http://localhost:8083
- 點擊右邊,選擇Create database
![](https://i.imgur.com/bWPAfT9.png)
- 輸入語法並按下**enter**
![](https://i.imgur.com/qhPxBTj.png)
### 完成
- 輸入SHOW MEASUREMENTS
- 看到欄位內的有資料
- ![](https://i.imgur.com/9BXrIOF.png)




