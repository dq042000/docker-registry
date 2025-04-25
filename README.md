## 建立認證檔案

```bash
docker run --rm --entrypoint htpasswd httpd:2 -Bbn 使用者名稱 密碼 > auth/htpasswd
```