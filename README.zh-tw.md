# Ecchi Fanservice Anime List Website

這個儲存庫是一個 Hugo 入門網站，用於從 JSON 資料檔發布結構化的「Ecchi Anime Fanservice List」。


## 開始使用

1. 從 [ecchi-fanservice-anime-list-data](https://github.com/ivon852/ecchi-fanservice-anime-list-data/) 取得資料，並放入 `/data`。

2. 連同子模組一起複製此儲存庫：
```bash
git clone --recurse-submodules <repo-url>

cd ecchi-fanservice-anime-list-website
```

3. 如果你已經複製儲存庫但沒有包含子模組，請手動初始化：
```bash
git submodule update --init --recursive
```

4. 啟動本機 Hugo 伺服器：
```bash
hugo server
```

5. 建置靜態網站：

```bash
hugo --gc --minify
```


## JSON 清單資料

主要的自訂 shortcode 是：
```go-html-template
{{< add-list "ecchi-fanservice-anime-list" "zh-TW" "enable-caption" "/posts/images/" >}}
```

第一個參數會對應到 `data/` 目錄中的 JSON 檔案：
```text
data/ecchi-fanservice-anime-list.json
```

若 JSON 是扁平陣列，shortcode 會渲染整份清單。若是合併資料集，你可以傳入第五個參數來選擇年份範圍：
```go-html-template
{{< add-list "uncensored-ecchi-anime-list" "zh-TW" "enable-caption" "/posts/images/" "2020-2029" >}}
```

預期的項目格式：
```json
{
  "name": {
    "zh-TW": "標題",
    "ja-JP": "タイトル",
    "en-US": "Title"
  },
  "date": "2026-04-11",
  "images": {
    "img1": {
      "zh-TW": "Caption",
      "ja-JP": "Caption",
      "en-US": "Caption",
      "imgsrc": "example.webp"
    }
  },
  "description": {
    "zh-TW": "Description",
    "ja-JP": "Description",
    "en-US": "Description"
  }
}
```

日期應使用 `YYYY-MM-DD` 格式。


## 客製化

大多數網站專屬行為都應在 Blowfish 子模組之外客製化：
- 編輯 `config/_default/` 以調整 Hugo 與 Blowfish 設定。
- 編輯 `assets/css/custom.css` 以覆寫視覺樣式。
- 編輯 `layouts/shortcodes/add-list.html` 以變更 JSON 渲染行為。
- 將可重複使用的佔位檔案放在 `static/`。
- 若情況允許，請將大型正式資料集與截圖保存在獨立的儲存庫中。


## 更新 Blowfish

```bash
git submodule update --remote themes/blowfish

git add themes/blowfish

git commit -m "Update Blowfish theme"
```


## 建構基礎

這個網站基於：
- [Hugo](https://gohugo.io/)，靜態網站產生器。
- [Blowfish](https://github.com/nunocoracao/blowfish)，採用 MIT License 授權的 Hugo 主題。
- 用於渲染 JSON anime 清單表格的自訂 Hugo shortcodes 與版面覆寫。


## 授權

此儲存庫建議使用的授權：**MIT License**。

MIT 很適合 Hugo 入門網站與主題儲存庫，因為它寬鬆、簡單，且相容於同樣採用 MIT 授權的 Blowfish。

內容資料集、截圖、文章文字與第三方媒體可能需要各自的授權或使用政策。若此儲存庫之後包含正式資料或媒體，建議將這些資產與網站範本程式碼分開記錄。

Blowfish 仍依其原始 MIT License 授權：
```text
Copyright (c) 2022 Nuno Coração
```
