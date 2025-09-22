
- https://wiki.freeradius.org/guide/Getting%20Started
- https://www.lijyyh.com/2013/07/radius-configuring-radius-server.html


## 0. Install RADIUS
apt install

freeradius
freeradius-utils




加使用者： `testing`， 
明碼密碼： `password`   
共用密碼 為 `testing123`  (在clients.conf 有設，可改)
```
testing Cleartext-Password := "password"
```

測試 驗證指令 
```
$ radtest testing password 127.0.0.1 0 testing123
```


## 2. 
vi 




service


netcat-xxxx

ssd
adcli
sssd-kbr5
krb5-user 

---- ???----

krb5-otp
krb5-config



# === 2 RADIUS LDAP AD =======

- https://www.freeradius.org/documentation/freeradius-server/4.0.0/howto/modules/ldap/base_configuration/index.html

- https://www.freeradius.org/documentation/freeradius-server/3.2.8/concepts/modules/ldap/authentication.html

- https://www.freeradius.org/documentation/freeradius-server/4.0~alpha1/raddb/mods-available/ldap.html
- https://www.freeradius.org/documentation/freeradius-server/4.0~alpha1/howto/modules/ldap/authentication.html
-   https://github.com/irasnyd/freeradius-ldap
- 
freeradius-ldap
freeradius-krb5


## 1. radius.conf -> 2. clients.conf -> 3. 加 users

## 1. Clients.conf 允許誰來用RADIUS

```
apt install freeradius-ldap freeradius-krb5

ln -s /etc/freeradius/3.0/mods-available/ldap /etc/freeradius/3.0/mods-enabled

```

改
/etc/freeradius/3.0/mods-available/ldap
```
server = '10.1.220.1' (AD Server)
base_dn = 
filter = "(mail=%{%{User-Name}:-%{Stripped-User-Name}})"
或
filter = "(sAMAccountName=%{%{Stripped-User-Name}:-%{User-Name}})"

 identity = deanliu@compeq.com.tw
password = Dean@

```
改
/etc/freeradius/3.0/sites-available/default
```
ldap  (- 減號 去掉)
  if ((ok || updated) && User-Password && !control:Auth-Type) {
                update control {
                        &Auth-Type := ldap
                }

。。。。。。。

 Auth-Type LDAP {
               ldap
       }


```

測試
```
freeradius -X
# 測試 
radtest deanliu@compeq.com.tw Dean@0005 localhost 0 testing123

```




## 工具 去掉 # 的行
```
sed '/^[[:blank:]]*(#)/d;s/#.*//;/^\s*$/d' file > out
```






# === 3 Radiud PAM ======


https://github.com/beatgammit/simple-pam

`apt install rsyslog`

```

# 1 clients (all)
/etc/freeradius/3.0/clients.conf

# 2 sites (default)
/etc/freeradius/3.0/sites-enabled/default
 
# 3 mods (pam) 
/etc/freeradius/3.0/mods-enabled/pam
pam {
        pam_auth = pam_radius   (/etc/pam.d/pam_radius) 
}

4 pam.d (radius) 
/etc/pam.d/pam_redius


/etc/freeradius/3.0/mods-enabled/ldap

```



## 1 install pam dev library
```
apt install libpam0g-dev

```
Check library header path `/usr/include/security`

## 2 pam code
vi pam_hello.c
```
#include <security/pam_modules.h>
#include <security/pam_ext.h>

PAM_EXTERN int pam_sm_authenticate(pam_handle_t *pamh, int flags, int argc, const char **argv) {
        pam_syslog(pamh, 1 , "pam_hello.c : authentication called");
        return PAM_SUCCESS;
}

PAM_EXTERN int pam_setcred(pam_handle_t **pamh, int flags, int argc, const char **argv) {
        return PAM_SUCCESS;
}

```
## 3 Build code
```
gcc -fPIC -fno-stack-protector -c pam_hello.c
ld -x --shared -o pam_hello.so pam_hello.o
cp pam_hello.so /lib/security/
```
## 4 /etc/freeradius/3.0/mods-enalbe/pam

## 5 sites-enabled/default



Notes
```



```






