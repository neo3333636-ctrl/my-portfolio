# OG 分享縮圖原始檔

社群分享（LINE / Facebook / Threads / X）連結時顯示的縮圖來源。

| 檔案 | 產出 | 用途 |
|---|---|---|
| `og-dark.html` | `../og-cover.jpg` | 主要 OG 縮圖（深色版） |
| `og-light.html` | `../og-cover-light.jpg` | 備用（淺色版，可用於提案 PDF／簡報封面） |

## 重新產生（數據更新時）

改完 HTML 裡的數字後，在專案根目錄執行：

```sh
CHROME="/Applications/Google Chrome.app/Contents/MacOS/Google Chrome"

"$CHROME" --headless=new --disable-gpu --hide-scrollbars \
  --force-device-scale-factor=2 --window-size=1200,630 \
  --screenshot=/tmp/og@2x.png "file://$PWD/og-source/og-dark.html"
sips -z 630 1200 /tmp/og@2x.png --out /tmp/og.png
sips -s format jpeg -s formatOptions 90 /tmp/og.png --out og-cover.jpg
```

淺色版把 `og-dark.html` 換成 `og-light.html`、`og-cover.jpg` 換成 `og-cover-light.jpg`。

## 注意

- 尺寸固定 **1200 × 630**，是 Open Graph 標準比例（1.91:1），不要改。
- `index.html` 的 `og:image` 必須寫**絕對網址**，相對路徑會讓 LINE / Facebook 抓不到圖。
- 換圖後平台會有快取，用 [Facebook 分享偵錯工具](https://developers.facebook.com/tools/debug/) 重新抓取，或在網址後面加 `?v=2` 強制更新。
