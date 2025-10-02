做一個最簡單的前後端 AD Server 的 帳號密碼登入測試
前端是一個fastapi的靜態html檔案, 第一列先放四個輸入框在同一列: 帳號, AD密碼, AD IP或主機名 (預設10.1.220.1), AD Domain/網域名(預設compeq.com.tw)
第二列輸入個下方是「BIND TEST」按鈕, 按下後就與 AD server 做 BIND 測試, BIND 成功後按鈕右方 顯示 BIND 成功, 失敗就顯示原因
BIND 成功後下方顯示 此登入帳號資訊: 如的帳號(sAMAccount), email, First Name, Last Name, 電話, 與頭像, manager, 部屬, 公司, 組織, department 及一般常用的 AD 欄位訊息
主管, 同部門成員, 部屬人員作為連結可同頁顯示帳號資訊. 

