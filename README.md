# zh-tech-writing

一個寫繁體中文（台灣）技術文件的 Agent Skill。用它寫 README、設計文件、介面說明和教學，讀起來像工程師寫的，沒有 AI 腔。

規則基於阮一峰的[《中文技術文檔的寫作規範》](https://github.com/ruanyf/document-style-guide)整理，另外補充了一份「AI 腔清單」。

適用於 Claude Code，以及其他支援 Agent Skills 的工具。

## 效果

下面是一段常見的 AI 寫法：

> 隨著微服務架構的不斷發展，設定管理已經成為一個不容忽視的問題。值得注意的是，ConfigHub 不僅提供了強大的設定管理能力，更實現了與現有系統的無縫整合——讓你輕鬆應對各種複雜情境！

用這個 skill 以後：

> ConfigHub 用來集中管理多個服務的設定。修改設定後，服務會在 5 秒內載入新值，不用重啟。串接時，在啟動命令裡加上 `--config-hub=<位址>` 即可。

改動有三處：
- 刪掉開場套話和驚嘆號。
- 去掉「不僅……更……」這種句式和破折號。
- 用具體事實替換「強大」「無縫」這類形容詞。

事實需要來自你的專案。skill 找不到事實時，會刪掉空話，或者直接問你。

## 安裝

用 [skills](https://github.com/vercel-labs/skills) 命令列工具安裝到全域：

```bash
npx skills add partment/zh-tech-writing -g
```

也可以手動安裝。把 `skills/zh-tech-writing` 目錄複製到 `~/.claude/skills/` 下面：

```bash
git clone https://github.com/partment/zh-tech-writing.git
cp -r zh-tech-writing/skills/zh-tech-writing ~/.claude/skills/
```

## 安裝 autocorrect（推薦）

[autocorrect](https://github.com/huacnlee/autocorrect) 是一個命令列工具。它會自動在中英文之間補空格，並把中文句子裡的半形標點改成全形。裝了它，AI 寫完文件後會按 skill 的要求執行一遍；沒裝就跳過這一步。

```bash
# macOS
brew install autocorrect

# Linux：從 Releases 頁面下載執行檔，放到 PATH 裡的任意目錄
# https://github.com/huacnlee/autocorrect/releases

# 已經裝了 Rust 工具鏈
cargo install autocorrect
```

裝好後執行 `autocorrect -V`，能看到版本號就說明裝好了。

## 使用

你讓 AI 寫或修改中文技術文件時，skill 通常會自動載入。比如：

```
幫我給這個專案寫一份 README
把 docs/deploy.md 改得更易讀一些
```

也可以手動呼叫：

```
/zh-tech-writing 改一下 docs/api.md
```

如果只想看修改意見，不想讓它直接改檔案，就說出來：

```
/zh-tech-writing 檢查 docs/api.md，只列問題，不要改
```

它會按「原句 → 改後 → 原因」的格式列出問題。

## 它做了什麼

skill 讓 AI 按下面的流程寫文件：

1. 先確定讀者是誰，讀完要能做成什麼事。
2. 按規則寫：句子、語氣、段落與結構、排版。
3. 用「AI 腔清單」逐條檢查全文，命中的地方全部改掉。
4. 執行 `autocorrect --fix`，修正空格和標點。
5. 手動檢查 autocorrect 不管的引號、刪節號和破折號。

主要規則：

- 句子：逗號隔開的每一截盡量在 20 字以內。多用肯定句和主動語態。直接用動詞，不套「進行」「做出」。
- 語氣：像給同事講清楚一件事。用數字、命令和錯誤訊息原文代替形容詞。
- 結構：每段第一句說重點。標題不跳級。少用四級標題。粗體和清單都不濫用。
- AI 腔清單：共 14 條，包括開場和結尾套話、「不是 A，而是 B」句式、硬湊三個排比、宣傳腔形容詞、行話、破折號和翻譯腔。

完整規則見 [SKILL.md](skills/zh-tech-writing/SKILL.md)。

## 目錄結構

```
skills/zh-tech-writing/
├── SKILL.md                     主檔案：流程、核心規則、AI 腔清單
└── references/
    ├── typography.md            數字、標點、英文縮寫的細則
    └── manual-structure.md      產品手冊的目錄結構和檔案命名
```

`references/` 下的檔案只在需要時讀取。比如，文件裡有數字範圍時才讀 `typography.md`。

## 來源與致謝

- 句子、段落、標題、標點和數字的規則，整理自阮一峰的[《中文技術文檔的寫作規範》](https://github.com/ruanyf/document-style-guide)。原專案放在公眾領域（public domain）。
  - 原規範裡有兩處符號寫錯了，這裡改成了標準寫法：破折號用 `——`，刪節號用 `……`。
  - 原規範說數字和中文之間加不加空格都可以。這裡統一定為加空格，這樣和 autocorrect 的結果一致。
  - 原規範要求「不使用非正式語言」。這裡放寬為：可以口語化，但不用網路流行語。
  - 原規範用中國用語，引號用 `“ ”`。這裡改成台灣用語，引號依教育部《重訂標點符號手冊》改用 `「」` 和 `『』`。
- 原規範本身參考了華為《產品手冊中文寫作規範》、LeanCloud《文檔風格指南》、[中文文案排版指北](https://github.com/sparanoid/chinese-copywriting-guidelines)、Google Developer Documentation Style Guide 和中國國家標準 GB/T 15835-2011。
- 「AI 腔清單」「用事實代替形容詞」和整套寫作流程，是這個專案新增的內容。
- 空格和標點的自動修正由 [autocorrect](https://github.com/huacnlee/autocorrect)（MIT 授權）完成。本專案只是執行這個工具，沒有包含它的程式碼。

## 授權

[MIT](LICENSE)
