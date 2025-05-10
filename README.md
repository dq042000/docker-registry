# Docker Registry 私有映像檔伺服器

本專案用於快速建構一個支援 htpasswd 認證的私有 Docker Registry，適合團隊或個人於內部網路部署自有映像檔倉庫。

---

## 目錄結構

- `docker-compose.yml`：啟用 htpasswd 認證的預設建構設定檔。
- `docker-compose.yml.dist`：不啟用認證的建構範本，可依需求調整。
- `auth/htpasswd`：存放 htpasswd 認證資訊檔案。
- `registry-data/`：映像檔儲存資料夾。

---

## 快速開始

### 1. 建立認證資訊 (如需啟用認證)

```bash
docker run --rm --entrypoint htpasswd httpd:2 -Bbn <使用者名稱> <密碼> > auth/htpasswd
```

### 2. 啟動 Registry

```bash
docker-compose up -d
```

### 3. 推送映像檔到私有 Registry

```bash
docker tag <本地映像>:<tag> localhost:5000/<映像名稱>:<tag>
docker push localhost:5000/<映像名稱>:<tag>
```

---

## 切換是否啟用認證

- **啟用認證**：使用 `docker-compose.yml`，並確保 `auth/htpasswd` 存在。
- **停用認證**：改用 `docker-compose.yml.dist`，並註解或移除 `auth` 相關設定。

---

## 常用指令

- 啟動服務：
  ```bash
  docker-compose up -d
  ```
- 停止服務：
  ```bash
  docker-compose down
  ```
- 查看日誌：
  ```bash
  docker-compose logs -f
  ```

---

## 注意事項

- 請勿將此 Registry 暴露於公網，建議僅於內部網路使用。
- 若需多用戶認證，可重複執行 htpasswd 指令新增帳號。
