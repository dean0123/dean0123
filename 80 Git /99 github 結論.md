
如果有Proxy 就用 https

- windows 就用 https ok (有 credential-manager)
```
git remote set-url origin https://github.com/username/repository.git

```
- docker linux 就用 https URL 加入 Token
就醬子
```
git remote set-url origin https://<TOKEN>@github.com/username/repository.git
```

如果 沒有 proxy 就用 ssh


