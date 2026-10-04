# 產品手冊結構與檔名

寫一整套軟體手冊或文件網站時參考。

## 目錄結構

| 部分 | 英文名 | 必備 | 形式 | 內容 |
|---|---|---|---|---|
| 簡介 | Introduction | 是 | 檔案 | 產品和文件的總體說明 |
| 快速上手 | Getting Started | 否 | 檔案 | 最快用起來的辦法 |
| 入門篇 | Basics | 是 | 目錄 | 初級使用教學 |
| ├ 環境準備 | Prerequisite | 是 | 檔案 | 使用前要滿足的條件 |
| ├ 安裝 | Installation | 否 | 檔案 | 安裝方法 |
| └ 設定 | Configuration | 是 | 檔案 | 設定說明 |
| 進階篇 | Advanced | 否 | 目錄 | 中高級開發教學 |
| API | Reference | 否 | 目錄或檔案 | 逐個介紹 API |
| FAQ | FAQ | 否 | 檔案 | 常見問題 |
| 附錄 | Appendix | 否 | 目錄 | 名詞解釋（Glossary）、最佳實務（Recipes）、故障排除（Troubleshooting）、版本說明（ChangeLog）、回饋方式（Feedback） |

參考範例：[Redux 文件](https://redux.js.org/introduction/getting-started)。

## 檔名

- 只用半形字元，不用中文，不含空格。
- 用小寫字母。`README`、`LICENSE` 這類檔案可以大寫。
- 多個單字用 `-` 連接。

```
差：名詞解釋.md    好：glossary.md
差：TroubleShooting.md    好：troubleshooting.md
差：advanced_usage.md    好：advanced-usage.md
```
