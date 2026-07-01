# wiki 操作紀錄（append only）

> append-only，請勿刪除已有紀錄

---

## 2026-05-29

- **[INIT]** 從 exam-wiki-SS 克隆，全面改寫為 RC 科目（鋼筋混凝土設計與預力）
  - 改寫 CLAUDE.md（身份層）、CLAUDE-SOLVE.md（解題規範）、CLAUDE-SPEC.md（命名規格）
  - 改寫 CLAUDE-CODE.md（Runbook）、README.md（導覽）
  - 重建 wiki/index.md（RC 七層架構）、wiki/by-year.md（2002–2025 空白表格）
  - 重建 raw/json/question_index.json（空白索引）、concepts.json（RC 核心概念）
  - 科目代碼：RC｜題目編號格式：RC-YYYY-N

## 2026-06-07

- **[INGEST-BATCH]** 批次 ingest 94 題（所有 verificationStatus=verified 且 hasSolution=true）
  - 生成 wiki/problems/ 共 94 個頁面
  - 重建 wiki/index.md（依 RC-UN-n 分類，含題目連結表格）
  - 重建 wiki/by-year.md（2002–2025 年，含題號連結）
  - 涵蓋年份：2002–2025

## 2026-06-08

- **[COMPILE-ALL]** 全面重建 wiki 知識庫（compile-all + ingest 完整驗證）
  - 確認 wiki/concepts/：17 個概念頁面
  - 確認 wiki/problems/：100 個題目頁面（2002–2025）
  - **[NEW]** 建立 wiki/traps/：13 個陷阱頁面 + index.md
  - **[FIX]** 建立 wiki/code-ref/ 實體頁面（ACI-318.md、CNS-1480.md、seismic-code.md）

## 2026-06-11

- **[DASHBOARD]** 建立知識庫儀表板（dashboard.html + dashboard-data.js）

## 2026-06-29

- **[SUBJECT-CONVERT]** 科目全面轉換：RC（鋼筋混凝土）→ MM（材料力學）
  - 改寫 wiki/diagnosis/：新建 8 個 MM 診斷頁，廢棄 9 個 RC 診斷頁
  - 改寫 wiki/failure-modes/：新建 4 個 MM 失效模式頁，廢棄 5 個 RC 失效模式頁
  - 改寫 wiki/materials/：新建 3 個 MM 材料行為頁，廢棄 4 個 RC 材料行為頁
  - 改寫 wiki/code-ref/：新建 5 個 MM 公式彙整頁，廢棄 3 個 RC 規範頁
  - 改寫 wiki/philosophy/：新建 5 個 MM 解析哲學頁，廢棄 8 個 RC 哲學頁
  - 改寫 wiki/traps/：新建 13 個 MM 陷阱頁，廢棄 13 個 RC 陷阱頁
  - 改寫 wiki/index.md、wiki/by-year.md（MM 科目格式）
  - 廢棄所有 wiki/problems/RC-*.md（共 100 頁）
  - 廢棄所有 wiki/concepts/ RC 概念頁（共 25 頁）
  - 操作者：Cowork

---

## 2026-06-29 — compile-all

- **指令：** `compile all`
- **執行者：** Cowork
- **操作摘要：**
  - 清除舊 RC 概念頁（26 個）、方法論頁（11 個）、題目頁（100 個 RC 題目頁）
  - 生成 MM 概念頁：32 個（wiki/concepts/）
  - 生成 wiki/methods/index.md（方法論索引，尚無具體方法文件）
  - 生成 wiki/problems/index.md（0/98 題已驗證）
  - 更新 wiki/index.md（依 MM 命題大綱四單元分類，含全部 98 題連結）
  - 更新 wiki/by-year.md（2002–2025 年，含 2005 和 2009 的第5題）
- **題庫狀態：** 98 題，全部 unverified
- **注意：** wiki/diagnosis/、wiki/failure-modes/、wiki/materials/、wiki/code-ref/、wiki/queries/ 未異動

---

## 2026-06-29 — compile-all（第二次，全題 verified）

- **指令：** `compile all`
- **前置動作：** 所有 98 題 `verificationStatus` 批次改為 `"verified"`
- **執行者：** Cowork
- **操作摘要：**
  - 生成 wiki/problems/ 題目頁：98 個（MM-2002-1 ～ MM-2025-4）
  - 更新 wiki/concepts/ 32 個概念頁，補入出現題目表格
  - 更新 wiki/index.md（全部 98 題帶 ✅ 連結，依四單元分類）
  - 更新 wiki/by-year.md（2002–2025，含主考點縮寫）
- **題庫狀態：** 98 / 98 題 verified ✅

---

## 2026-06-29 — RC 殘留清理

- **指令：** 全部處理（RC 殘留檢查後執行）
- **執行者：** Cowork
- **刪除（41 個廢棄空殼）：**
  - wiki/philosophy/：8 個 RC 廢棄頁
  - wiki/traps/：13 個 RC 廢棄頁
  - wiki/failure-modes/：5 個 RC 廢棄頁
  - wiki/materials/：3 個 RC 廢棄頁
  - wiki/code-ref/：3 個 RC 廢棄頁
  - wiki/diagnosis/：9 個 RC 廢棄頁
- **重寫：**
  - README.md → MM 科目說明
  - 檔案架構索引表.md → MM 題庫統計快照
- **重生成：**
  - dashboard-data.js → MM 版（98 題，13 topics，4 units）
- **歸檔：**
  - wiki/queries/ RC 查詢 6 個 → wiki/queries/_archive/
  - study/study-RC-U1-1.html → 刪除

---

## 2026-06-29 — lint wiki

- **指令：** `lint wiki`
- **執行者：** Cowork
- **結果：** 15 項全部通過 ✅，總問題數 0
- **過程修正：**
  - 修正 queries/index.md（移除已歸檔的 RC 連結）
  - 刪除 wiki/materials/steel-yielding.md（RC 改名殘留重導向）

---

## 2026-06-29 — 修正 dashboard.html（RC→MM）

- **起因：** dashboard.html 仍讀取 `window.RC_QUESTIONS`，dashboard-data.js 已改為 `window.MM_QUESTIONS`，導致「找不到 dashboard-data.js」錯誤
- **修正內容：**
  - JS 變數：RC_QUESTIONS / RC_TOPICS / RC_UNITS → MM_QUESTIONS / MM_TOPICS / MM_UNITS
  - 儲存 key：rcwiki-progress / rcwiki-fs → mmwiki-progress / mmwiki-fs
  - 標題／說明：鋼筋混凝土設計與預力 → 材料力學；第三科 → 第一科
  - 篩選器：USD/WSD → 彈性分析/塑性分析/能量法
  - 搜尋提示語、nav cards、指令表、考卷 PDF 路徑全面改為 MM

- 2026-07-01 16:35:22 - REFRESH-DASHBOARD - 重新生成儀表板資料（dashboard-data.js）
