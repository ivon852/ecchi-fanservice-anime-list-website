# Ecchi Fanservice Anime List Website

[繁體中文說明](README.zh-tw.md)

This repository is a Hugo starter website for publishing structured "Ecchi Anime Fanservice List" from JSON data files.

Example website: [https://htxacg.cc/posts/uncensored-ecchi-anime-list/](https://htxacg.cc/posts/uncensored-ecchi-anime-list/)

## Getting Started

1. Fetch data from [ecchi-fanservice-anime-list-data](https://github.com/ivon852/ecchi-fanservice-anime-list-data/). Place them in `/data`

2. Clone the repository with submodules:
```bash
git clone --recurse-submodules <repo-url>

cd ecchi-fanservice-anime-list-website
```

3. If you already cloned it without submodules, initialize them manually:
```bash
git submodule update --init --recursive
```

4. Run the local Hugo server:
```bash
hugo server
```

5. Build the static site:

```bash
hugo --gc --minify
```


## JSON List Data

The main custom shortcode is:
```go-html-template
{{< add-list "ecchi-fanservice-anime-list" "zh-TW" "enable-caption" "/posts/images/" >}}
```

The first argument maps to a JSON file in the `data/` directory:
```text
data/ecchi-fanservice-anime-list.json
```

For a flat JSON array, the shortcode renders the whole list. For a combined
dataset, you may pass a fifth argument to select a year range:
```go-html-template
{{< add-list "uncensored-ecchi-anime-list" "zh-TW" "enable-caption" "/posts/images/" "2020-2029" >}}
```

Expected item shape:
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

Dates should use the `YYYY-MM-DD` format.


## Customization

Most site-specific behavior should be customized outside the Blowfish submodule:
- Edit `config/_default/` for Hugo and Blowfish settings.
- Edit `assets/css/custom.css` for visual overrides.
- Edit `layouts/shortcodes/add-list.html` to change JSON rendering behavior.
- Put reusable placeholder files in `static/`.
- Keep large production datasets and screenshots in separate repositories when possible.


## Updating Blowfish

```bash
git submodule update --remote themes/blowfish

git add themes/blowfish

git commit -m "Update Blowfish theme"
```


## Built On

This website is based on:
- [Hugo](https://gohugo.io/), the static site generator.
- [Blowfish](https://github.com/nunocoracao/blowfish), a Hugo theme licensed under the MIT License.
- Custom Hugo shortcodes and layout overrides for rendering JSON-backed anime list tables.


## License

Recommended license for this repository: **MIT License**.

MIT is a good fit for a Hugo starter/theme repository because it is permissive,
simple, and compatible with Blowfish, which is also MIT licensed.

Content datasets, screenshots, article text, and third-party media may need
their own license or usage policy. If this repository later includes production
data or media, consider documenting those assets separately from the website
template code.

Blowfish remains licensed under its original MIT License:
```text
Copyright (c) 2022 Nuno Coração
```
