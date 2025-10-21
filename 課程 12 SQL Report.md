
1. FastAPI 做一個靜態網頁，6個輸入框 「IP/Host」「DB SID」「帳號」「密碼」「DB type 預設Oracle/SQL Server/Postgres」 「Port」 一個按鈕「測試連連」按下後， =顯示測試連線結果成功或失敗訊息

2. 上述靜態網頁，加一個可調整大小的輸入框 可輸入SQL Statement. 一個【查詢】按鈕
   按鈕按下後，會連線到後端 程式連線到 DB， 並以 json 格式傳回前端， 直接以文字方式顯示在畫面上

3. 加一個按鈕 「Row Set」 把JSON 格式轉換為 Row Set， 以文字模式顯示

4. 加一個按鈕「HTML Table」結果顯示為 HTML 輸出， 再加一個按鈕可以將最左邊三個欄位上下值如果重複，自動做 rowspan

5. 加一個按鈕「Excport CSV」把結果輸出為 CSV 檔案

6. 加一個按鈕「datatables」引入 datatables.js CDN，並套用結果，以datatables 顯示具有排列，查詢，分頁的功能

7. 加一個「transpose」將 (3)row set X軸與 Y軸互換，文字方式顯示

8. 加一個 按鈕「Pivot」 處理只有三個columnes 的輸出的，將第二個 Column 值 轉為 Row 的 欄位標題 Head。 以文字 dataset 方式顯示

9. 加一個按鈕「echart」引入 「echarts.js」CDN，自動處理前三個columns 畫成 chart

第一個 Column 值 為 x-axis type=category，
      column name 設為 x-axis 的名稱，「或保留不使用」
第二個 column 值 為 series name，
      column name 「可做為 Legend Name」
第三個 column 值為 y-axis type=value data 值，
畫出 line chart (multiple/stacked)， bar chart(stacked/group)，pie chart
      column name 為這個 Chart 的 Chart Name

10. 將上述全部的 java script 功能收入一個 dataresult.js 裡面，前端頁面只要引入這個 dataformat.js，做最小的處理就可以很容易輸出轉換輸出不同的格式。 以後其他前端的到的 DB Query Reuslt，只要引入這個 dataformat.js， 也都能很快套用這些輸出的格式，不用再重寫輸出格式轉換。  
