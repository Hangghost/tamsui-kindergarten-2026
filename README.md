# 淡水分區幼兒園抽籤小幫手

React + Vite 靜態網站，整理新北市淡水分區（淡水區、石門區、三芝區）公立與非營利幼兒園缺額、地圖、距離與新手爸媽挑選重點。

> Fork 自 [bluetch/ntpc-kindergarten-2026](https://github.com/bluetch/ntpc-kindergarten-2026)（中永和版本），移除了 AI 評分功能，改成純資訊比較。

## 本機開發

```bash
npm install
npm run dev
```

## 部署到 GitHub Pages

1. 在 GitHub 建立一個新 repo，例如 `tamsui-kindergarten-picker`。
2. 將本專案 push 到 `main` 分支。
3. 到 repo 的 `Settings` -> `Pages`，Source 選 `GitHub Actions`。
4. 每次 push 到 `main` 會自動 build 並部署。

## 資料來源

- 缺額：`https://kid123.ntpc.edu.tw/`（2026-04-29 公告）
- 經緯度 / 地址：Google Maps 自動爬取
- 抓取流程在 `infra/adhoc_jobs/tamsui_kindergarten_scrape/`（位於 Exocortex-personal repo）

## 更新資料

幼兒園清單在 `src/data/kindergartens.js`。

- `lat` / `lng`：距離為直線粗估，實際接送時間請用 Google Maps 路線確認。
- `vacancies`：缺額以 2026-04-29 新北市 115 學年度公告為基準，若官方更動請直接更新。
- `homes.homeA` / `homes.homeB`：Joey 的預設接送地址（透過 `?home=joey` 啟用）。其他訪客看到的是空地址、需自填。

## 重新抓取資料

```bash
# 在 Exocortex-personal repo 內
uv run --group tamsui-scrape python infra/adhoc_jobs/tamsui_kindergarten_scrape/scrape_kid123.py
uv run --group tamsui-scrape python infra/adhoc_jobs/tamsui_kindergarten_scrape/enrich_with_gmaps.py
uv run --group tamsui-scrape python infra/adhoc_jobs/tamsui_kindergarten_scrape/retry_addresses.py
uv run --group tamsui-scrape python infra/adhoc_jobs/tamsui_kindergarten_scrape/generate_kindergartens_js.py
```
