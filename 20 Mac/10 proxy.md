## ===== 請IT 打開 IP 比較快 =====

## ----- curl 用 Proxy -----
exxport HTTP_PROXY="http://10.1.229.229:15629"
exxport HTTPS_PROXY="http://10.1.229.229:15629"
exxport ALL_PROXY="http://10.1.229.229:15629"

有的說 ～/.curlrc 加 proxy=10.1.229.229:15629  (好像沒用)

 直接指定 curl Proxy 
curl https://google.com --proxy 10.1.229.229:15629


刪除 
unset HTTP_PROXY
unset HTTPS_PROXY
unset ALL_PROXY


## ----- git ------
git config --global http.proxy http://10.1.229.229:15629
git config --global https.proxy http://10.1.229.229:15629
git config --global http.sslVerify false

git config -l

刪除
git config --global --unset http.proxy
git config --global --unset https.proxy
git config --global --unset http.sslVerify