# Redash

### How to build other version?
* 可以到 https://version.redash.io/ 查看目前有釋出的版本
* 這裡 https://version.redash.io/API/releases 可以下載 release 的內容

找到你要的版本後，依據 "download_url" 下載 tar.gz 檔
建立一個資料夾後，將其解壓縮
> tar -zxf redash.7.0.0.b17535.tar.gz -C <path>

接著修改 docker-compose.yml，我們要將自行 build image 的方式改為指定成在 docker hub 上的 image
```yaml
build: .
```
改成
```yaml
image: "redash/redash:7.0.0.b18042"
```

如果你想要自己 build image 的話也可以，但是我嘗試自編時遇到很多問題，其中一個是 memory 問題。所以我這邊直接用 docker hub 上編好的。
直接用 docker hub 上的 image 可能會遇到 import 對象找不到的問題，遇到的話可以參考[這裡的image](https://github.com/LiuLiujeng/docker-redash)。

接下來要先建立 database
```bash
$ docker-compose run --rm server create_db
```

沒有錯誤訊息的話，即可執行
```bash
$ docker-compose up
```

訪問 http://0.0.0.0:5000

### 其他問題
#### Invalid parameter: "static_path"
* 這是因為版本的問題，請將 `static_path` 改為 `static_url_path`
