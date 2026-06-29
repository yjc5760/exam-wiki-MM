# 結構工程技師考試知識庫 — 材料力學（MM）

> 科目代碼：MM｜資料夾：`exam-wiki-MM`｜其他科目另建獨立資料庫

## 專案說明

本資料庫專門收錄「專門職業及技術人員高等考試結構工程技師」**第一科：材料力學**的考古題解析知識庫。

- **科目代碼：** MM（Mechanics of Materials）
- **題目編號格式：** MM-YYYY-N（如 MM-2016-1）
- **其他科目：** 各自建立獨立資料庫（exam-wiki-SS、exam-wiki-RC 等）

**核心工作流程：**
```
在 Cowork 開啟 exam-wiki-MM/ 資料夾（Project）
    ↓
說：「解析 XXXX 年考卷」
Cowork 讀取 CLAUDE.md + 考卷 PDF + question_index.json
  → 建立所有尚無解析的題目資料夾（已有解析者跳過）
  → 提醒你將各題附圖截圖存入對應資料夾
  → 等待你通知「截圖完成，請開始解題」
    ↓
【你做】依提醒截圖存檔，完成後告知 Cowork
    ↓
【重要】Cowork 一次只解一題，解完存檔後再繼續下一題
    ↓
你加入補充截圖（chart/eqn/hand）
請 Cowork 更新 question_index.json（tags、verified）
    ↓
說：「ingest MM-XXXX-N」→ Cowork 直接執行，wiki 自動更新
```

---

## 兩個環境分工

| 環境 | 負責什麼 |
|------|---------|
| **你（使用者）** | PDF 題目附圖截圖（fig-N.png）、chart/eqn/hand 補充截圖、人工驗算後通知 Cowork 更新 verificationStatus |
| **Cowork** | 解題（SOLVE，**一次一題**）、存檔（.md + viz.html）、更新 question_index.json、**所有 wiki 操作指令**（ingest / compile-all / lint / status / reindex / add-concept / add-method / refresh-dashboard / frequency / analyze / predict / study / find / related / unverified / query，共 16 個，詳見 CLAUDE-CODE.md）、直接維護 wiki/diagnosis/ · wiki/failure-modes/ · wiki/materials/ · wiki/code-ref/ · wiki/queries/ · study/（study 指令輸出） |

---

## 單向資料流

```
raw/solutions/MM-XXXX-N/MM-XXXX-N.md  ──→  wiki/problems/      （Cowork: ingest）
raw/json/concepts.json                 ──→  wiki/concepts/      （Cowork: compile-all）
raw/solutions/methods/                 ──→  wiki/methods/       （Cowork: compile-all）
Cowork 查詢結果                        ──→  wiki/queries/       （Cowork 直接存入）
Cowork study 指令輸出                  ──→  study/              （Cowork 直接存入）
Cowork 跨層知識工具                    ──→  wiki/diagnosis/     （Cowork 直接存入）
                                       ──→  wiki/failure-modes/ （Cowork 直接存入）
                                       ──→  wiki/materials/     （Cowork 直接存入）
                                       ──→  wiki/code-ref/      （Cowork 直接存入）

解題內容唯一來源：raw/solutions/ 下的 .md 檔案
索引資訊唯一來源：raw/json/question_index.json
wiki/queries/、study/（study 輸出）及四個跨層知識目錄：由 Cowork 直接寫入，不走 ingest 流程
```

---

## 資料夾結構

```
exam-wiki-MM/
├── README.md                        ← 冷啟動快速導覽
├── CLAUDE.md                        ← 本檔（身份層：分工、資料流、重要規則）
├── CLAUDE-SOLVE.md                  ← Cowork 解題 Skill
├── CLAUDE-CODE.md                   ← Claude Code 操作指令（Runbook）
├── CLAUDE-SPEC.md                   ← 規格驗證層（格式、命名、完成標準）
│
├── study/                           ← 讀書筆記、講義、study 指令 HTML 輸出（study-MM-UN.html / study-MM-UN-n.html）
│
├── raw/                             ← 所有原始資料（唯讀，絕對不可修改）
│   ├── exams/                       ← 原始考卷 PDF（命名：MM-YYYY_材料力學.pdf）
│   ├── json/
│   │   ├── concepts.json            ← 概念定義（供 compile-all）
│   │   └── question_index.json      ← ⭐ 題目總索引（唯一需要人工維護的 JSON）
│   └── solutions/                   ← AI 解析 + 補充截圖（每題一個資料夾）
│       ├── MM-YYYY-N/
│       │   ├── MM-YYYY-N.md
│       │   ├── MM-YYYY-N-fig-1.png
│       │   └── MM-YYYY-N-[內容碼]-viz.html
│       └── methods/                 ← 解題方法論
│
└── wiki/                            ← 知識庫輸出
    ├── index.md                     ← 主導航（七層架構）
    ├── by-year.md                   ← 依考年分類
    ├── log.md                       ← 操作紀錄（append only）
    ├── concepts/                    ← 概念頁         ← Cowork (compile-all)
    ├── methods/                     ← 方法論頁       ← Cowork (compile-all)
    ├── traps/                       ← 陷阱頁         ← Cowork (compile-all)（補充目錄，非七層架構核心）
    ├── problems/                    ← 題目頁         ← Cowork (ingest)
    ├── philosophy/                  ← 解析哲學頁     ← Cowork (compile-all)
    ├── queries/                     ← 查詢結果頁     ← Cowork (直接存入)
    ├── diagnosis/                   ← 題型診斷層     ← Cowork (直接存入)
    ├── failure-modes/               ← 失敗模式層     ← Cowork (直接存入)
    ├── materials/                   ← 材料行為層     ← Cowork (直接存入)
    └── code-ref/                    ← 規範條文對應層 ← Cowork (直接存入)
```

---

## 知識分類骨架（七層）

Wiki 導航依七層知識架構組織（前三層由 Cowork 透過 compile-all/ingest 生成，後四層由 Cowork 直接維護）：

| 層 | 目錄 | 維護者 | 內容 |
|----|------|:------:|------|
| Layer 1 | `concepts/` + `problems/` | Cowork (ingest/compile) | 核心概念（斷面性質/應力應變/撓度/挫屈/塑性） |
| Layer 2 | `philosophy/` | Cowork (compile-all) | 解析哲學（彈性法/塑性法/疊加法/能量法） |
| Layer 3 | `methods/` | Cowork (compile-all) | 解題方法論（Mohr's circle/撓度積分/Euler 挫屈/塑性鉸） |
| Layer 4 | `diagnosis/` | Cowork (直接存入) | 題型診斷決策樹 |
| Layer 5 | `failure-modes/` | Cowork (直接存入) | 失敗模式（降伏/挫屈/斷裂/過大變形） |
| Layer 6 | `materials/` | Cowork (直接存入) | 材料行為（彈性-塑性/韌性/脆性/疲勞） |
| Layer 7 | `code-ref/` | Cowork (直接存入) | 參考公式對應（正向應力/剪應力/扭轉/撓度/挫屈） |

> **補充目錄 `wiki/traps/`：** 不屬於七層架構，由 compile-all 從題目解析萃取陷阱頁面，與 concepts/ 並列為輔助導航。

---

## 命題大綱分類（依官方命題大綱）

> topicId 格式：`MM-UN-n`，U = 單元號，n = 子項號。
> `primaryTopicId` 填最主要考點；跨子項時用 `secondaryTopicIds` 列出。

### 第一單元（MM-U1）：斷面與材料性質

| topicId | 命題大綱子項 |
|---------|------------|
| MM-U1-1 | 斷面性質計算 |
| MM-U1-2 | 虎克定律應用 |
| MM-U1-3 | 應力及應變分析原理與應用 |

### 第二單元（MM-U2）：斷面應力分析

| topicId | 命題大綱子項 |
|---------|------------|
| MM-U2-1 | 軸力桿件斷面應力計算 |
| MM-U2-2 | 梁桿件斷面應力計算 |
| MM-U2-3 | 扭力桿件斷面應力計算 |

### 第三單元（MM-U3）：變位與內力分析

| topicId | 命題大綱子項 |
|---------|------------|
| MM-U3-1 | 軸力桿件變位及內力分析 |
| MM-U3-2 | 梁桿件變位及內力分析 |
| MM-U3-3 | 扭力桿件變位及內力分析 |
| MM-U3-4 | 柱之挫屈載重分析 |
| MM-U3-5 | 動態變位分析 |

### 第四單元（MM-U4）：塑性分析

| topicId | 命題大綱子項 |
|---------|------------|
| MM-U4-1 | 軸力桿件、扭力桿件與梁之塑性分析 |
| MM-U4-2 | 殘留應力與應變 |

---

## 重要規則

1. **`raw/` 目錄下所有檔案絕對不可修改**（`question_index.json` 除外）
2. **`verifiedSolution` 是最終答案，不可質疑或重新計算**
3. **`wiki/log.md` 只可 append，不可刪除已有紀錄**
4. **wiki/ 大多數目錄是 compile 輸出，不可手動修改**；例外：diagnosis/ · failure-modes/ · materials/ · code-ref/ · queries/ 由 Cowork 直接維護
5. **ingest 前必須確認 verificationStatus = "verified"**
6. 概念連結使用 `[[concept_id]]`（Obsidian 相容）
7. 每次 ingest 同時更新 index.md 和 by-year.md
8. **格式與命名規範見 CLAUDE-SPEC.md；操作指令（ingest/compile/lint/status）見 CLAUDE-CODE.md，全部由 Cowork 執行**

---

## CHANGELOG

| 日期 | 變更 | 原因 |
|------|------|------|
| 2026-05-29 | 從 exam-wiki-SS 克隆 RC 版本 | RC 科目建庫 |
| 2026-06-04 | 三層架構改為兩層（User/Cowork） | 知識庫全程在 Cowork 運行 |
| 2026-06-11 | 新增 dashboard；指令擴充至 16 個 | 建立視覺化入口 |
| 2026-06-26 | study 指令輸出目錄改為 study/ | 講義集中管理 |
| 2026-06-29 | 全面改寫為 MM（材料力學）科目 | 從 exam-wiki-RC 克隆後轉換科目 |
