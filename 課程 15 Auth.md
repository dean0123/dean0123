做一個最簡單的前後端 AD Server 的 帳號密碼登入測試
前端是一個fastapi的靜態html檔案, 第一列先放四個輸入框在同一列: 帳號, AD密碼, AD IP或主機名 (預設10.1.220.1), AD Domain/網域名(預設compeq.com.tw)
第二列輸入個下方是「BIND TEST」按鈕, 按下後就與 AD server 做 BIND 測試, BIND 成功後按鈕右方 顯示 BIND 成功, 失敗就顯示原因
BIND 成功後下方顯示 此登入帳號資訊: 如的帳號(sAMAccount), email, First Name, Last Name, 電話, 與頭像, manager, 部屬, 公司, 組織, department 及一般常用的 AD 欄位訊息
主管, 同部門成員, 部屬人員作為連結可同頁顯示帳號資訊. 



## 學習目標

我要做一個 auth serviec 透過 oauth2 oidc jwt 等技術，讓組織內其他跨不同server 的前後端網頁應用app 及 api 可以很快的做安全的身分認證。 

其中 client_id 先統一用 ”

1. index.html 前端做一個fastapi 靜態網頁，包含四個輸入框 帳號密碼 AD Server IP/hostname，Domain。 登入 並 顯示 AD user info

2. oidc.js 與認證相關的功能都包裝在 所有與auth 相關的功能，包裝在一個 oauth2.js 的 jsvascript 檔案內，用一行 script src url 方式引入前端靜態網頁。 並套入 user info 讓前端網頁可以很方便的用來顯示，或處理。 讓這個 oidc.js 可以套用在其他應用網頁， 直接登入認證取得登入的 userinfo。  

3. 後端 user 認證功能，IDP 是 AD Server， NTLM bind 成功就是登入成功， Bind 失敗就是登入失敗。 

4. 前資料交換， client_id 先統一用 “compeq”， callback-uri 自動從 origin 取得跳回原來的前端網頁。 
後端做一個
2. 取得自己 AD User Info，姓名， 部門，電話，主管，photo， 同儕，部署
3. 以上述主管，同部門，部署人連結取得其 AD User Info， 格式相同
4. 做一OIDC Service 提供



client_id, callback_url, auth_server, show_login, auto_login 