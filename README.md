1.可爬完所有分類看板

2.可指定貼文發布日期的區間爬取(目前只爬一個看板，可修正)

3.儲存格式部分已設計完成(MySQL)

4.可將爬完資料逐筆存入MySQL(但存入後會有些小問題，待修正)


待完成部分:

 1 須考慮機器如因不可預期狀況停機，後續如何追朔未擷取之資料。
 
  : 將設定的時間區間以及爬過的網址或文章編號寫入log，再比對log看那些抓過。

 2. 須考慮爬蟲會被部署在多台機器架構下的狀況。
 
 :可使用docker 搭配spark 自動分配

 3. 須考量如何監控爬蟲狀態及相關異常通知。
 
 :使用line bot 將錯誤訊息推送，或是google api傳送email

 4. 須考量如何避免因過度快速擷取⾴⾯⽽造成的網路資安問題。
 
 :可用多個ip循環跑，可用許多header，可用隨機等待時間模擬手動操作

 5.  請以 docker 建置及安裝各類外部服務。
 
 : 安裝步驟
 
(1)  docker pull jupyter/base-notebook:latest

(2)  docker pull mysql:8.0.19

(3)  docker run --name mysql -e MYSQL_ROOT_PASSWORD=123456 -v $(pwd)/sqldb:/var/lib/mysql -d -p 3360:3360 mysql:8.0.19

(4)  docker run --link mysql --name jupyter -d -p 8888:8888 -p 5000:5000 -v $PWD/app/:/home/jovyan/work/data jupyter/base-notebook start-notebook.sh --NotebookApp.token= ""

(5)將附件ptt_crawler.ipynb 放進app資料夾中

(6)開啟jupyter網頁執行
