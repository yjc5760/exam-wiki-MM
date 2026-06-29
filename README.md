# exam-wiki-MM — 材料力學考古題知識庫

**科目：** 專門職業及技術人員高等考試結構工程技師 — 第一科：材料力學  
**科目代碼：** MM（Mechanics of Materials）  
**收錄範圍：** 2002–2025 年（民國 91–114 年）  
**題目編號：** MM-YYYY-N（如 MM-2018-1 = 2018 年第 1 題）  
**總題數：** 98 題（2005、2009 年各有第 5 題）

---

## 快速導覽

| 我要… | 去這裡 |
|-------|--------|
| 看所有題目（依單元） | [wiki/index.md](wiki/index.md) |
| 看所有題目（依年份） | [wiki/by-year.md](wiki/by-year.md) |
| 查某個概念 | [wiki/concepts/](wiki/concepts/) |
| 查解題方法論 | [wiki/methods/](wiki/methods/) |
| 開啟互動儀表板 | [dashboard.html](dashboard.html) |
| 查操作指令 | [CLAUDE-CODE.md](CLAUDE-CODE.md) |
| 查解題規範 | [CLAUDE-SOLVE.md](CLAUDE-SOLVE.md) |

---

## 命題大綱四單元

| 單元 | 名稱 | 子項數 | 歷年題數 |
|------|------|--------|---------|
| MM-U1 | 斷面與材料性質 | 3 | 約 20 題 |
| MM-U2 | 斷面應力分析 | 3 | 約 28 題 |
| MM-U3 | 變位與內力分析 | 5 | 約 35 題 |
| MM-U4 | 塑性分析 | 2 | 約 15 題 |

---

## 核心工作流程

```
解析 XXXX 年考卷
  → 建立 raw/solutions/MM-XXXX-N/MM-XXXX-N.md
  → 驗算確認後：將 verificationStatus 改為 verified
  → ingest MM-XXXX-N  →  wiki/problems/ 自動更新
```

**常用指令：** `status` · `ingest MM-XXXX-N` · `compile all` · `frequency` · `predict` · `study MM-UN`

---

*建庫日期：2026-06-29｜其他科目：exam-wiki-SS（鋼結構）、exam-wiki-RC（鋼筋混凝土）*
