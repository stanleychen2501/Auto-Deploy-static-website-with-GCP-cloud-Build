# 透過 Google Cloud Build 在Google Cloud Storage自動部署靜態網站
### 開始之前您需要
1. 擁有對外服務的域名
2. 註冊GCP帳號，並且擁有專案
3. 擁有Github Repositry

---
## 建立Storage Bucket

將您的網站內容作為文件上傳到 Cloud Storage，您可以透過Bucket託管您的靜態網站。首先，您需要創建一個Bucket。前往 Cloud Console 的存儲部分並輸入您的域名，例如 (www.example.com)
並創建Bucket：
輸入bucket名稱與選擇區域
![](https://i.imgur.com/5Wuamrw.png)
選擇儲存類型與ACL方式(預設即可)
![](https://i.imgur.com/R2Q1M23.png)
進到Bucket後選擇Permission並將Allusers作為Storage object viewer加入
![](https://i.imgur.com/TSS3UIN.png)
編輯網站設定，輸入主畫面檔案後保存
![](https://i.imgur.com/zkZXagP.png)

---

![](https://i.imgur.com/cvoqyQZ.png)
## 建立Cloud Build Trigger
進到Cloud Build Trigger頁面後選擇Create trigger
![](https://i.imgur.com/t4x60lz.png)
輸入名稱並選擇觸發方式，如果您Fork本範例專案，請選擇“Push to a branch”
![](https://i.imgur.com/teMXo6E.png)
連結github repositry
![](https://i.imgur.com/MTSYSQH.png)

輸入Branch:^main$

---

## 建立自動化部屬文件
在Github repositry中建立檔案：
```
steps:
  - name: gcr.io/cloud-builders/gsutil
    args: ["-m", "rsync", "-r", "-c", "-d", "[Your-Path]", "gs://[Your-Bucket-Name]"]
```
請置換路徑與bucket名稱，路徑請依照您的repositry目錄路徑

之後點擊create 建立，接著嘗試修改Index.html 檔案內容，即可看到修改的變化。
