# Grafana InfluxDB整合步驟文件
## 前置所需軟體
- docker engine
## clone專案
- `git clone https://github.com/kddco/grafana-influxdb.git`
## Grafana安裝
## 安裝Grafana在Docker裡面
- `docker-compose -f docker-compose-bridge.yml up -d`
## 嘗試網頁登入
- http://127.0.0.1:3000
- ![](https://i.imgur.com/noE2vhK.png)

- 帳號密碼都是admin
- 如有錯誤
  - 嘗試登入上層router分配給機器的ip(192.168.70.101)
  - docker logs查看
- 文章參照 https://www.cnblogs.com/python-gm/p/12843653.html

# influxdb時序性資料庫安裝
- 連接libreNMS的主機資訊，並透過influxdb來媒介，最後呈現到grafana上面
## 建立influxdb的Container
- `docker run -d -p 8083:8083 -p 8086:8086 -e PRE_CREATE_DB="librenms" -e INFLUXDB_ADMIN_USER=librenms -e INFLUXDB_ADMIN_PASSWORD=password tutum/influxdb:latest`


- 已在docker run環境參數中設定admin帳號密碼 **librenms/password**
- port 8083是網頁管理頁面
- port 8086是HTTP API通道
# 到LibreNMS開啟外部整合
## 全域設定
![](https://i.imgur.com/hLRu9HQ.png)
## 輪詢器
![](https://i.imgur.com/F9GhKCP.png)
## InfluxDB 
 ![](https://i.imgur.com/LqI5EYR.png)
## 設定連接API
![](https://i.imgur.com/Qk4v5LH.png)
## influxdb上建立librenms資料庫
- 先到influxdb網頁管理頁面 http://localhost:8083
- 點擊右邊,選擇Create database
![](https://i.imgur.com/bWPAfT9.png)
- 輸入語法並按下**enter**
![](https://i.imgur.com/qhPxBTj.png)
## libreNMs成功把資料給influxdb
- 輸入SHOW MEASUREMENTS
- 看到欄位內的有資料
- ![](https://i.imgur.com/9BXrIOF.png)
- **如輸入Query沒有得到途中資料則是有誤**
## 回到Grafana設定資料來源
- 點齒輪，點Data Sources
![](https://i.imgur.com/EeeAFSp.png)
## Add data source -> Data Sources / InfluxDB
![](https://i.imgur.com/VIHAjee.png)
![](https://i.imgur.com/727GFYs.png)
## 到terminal查看influxdb的ip
`docker inspect influxsrv | grep IPAddress`
![](https://i.imgur.com/4AN7Pll.png)
## 在grafana上面設定influxdb連線
![](https://i.imgur.com/qW1jGFz.png)
![](https://i.imgur.com/vWfkyrC.png)
- 連線目標db名稱：libreNMS
- 帳號密碼：librenms/password
    - 參照influxdb生成使用的環境參數
![](https://i.imgur.com/8P1jdYt.png)
- 按下save&test出現綠色字則成功
- 如錯誤請參考grafana 或是 influxdb的docker logs
## import現成的dashboard
![](https://i.imgur.com/uHtCpaM.png)
- 輸入InfluxDB結合libreNMS現成Dashboards編號
- [套用更多現成版型連結-點我](https://grafana.com/grafana/dashboards) 
![](https://i.imgur.com/FsvPvme.png)
- 按下load
![](https://i.imgur.com/GRz58WZ.png)
- 選取InfluxDB並按下import
## 查看套版的Dashboard
### 儀表板管理
![](https://i.imgur.com/3MpF1pG.png)
### 最終成品
- 部分數值為空是主機本身無提供，屬正常現象
![](https://i.imgur.com/Wun6S18.png)






