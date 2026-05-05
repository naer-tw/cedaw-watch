# 平台資料齊全度報告

> **建立日**:2026-04-30 / Wave 65
> **目的**:回應「資料齊全嗎?」之系統性盤點與後續路線

## 一、SQLite 資料庫狀態(57 表)

### 已充實(15 表)
| 表 | 筆數 | 來源 |
|---|---|---|
| cedaw_article | 30 條 | 公約原文 |
| cedaw_general_recommendation | 11 GR | UN OHCHR |
| concluding_observation | 212 段 | 4 cycles 全量 pypdf 解析 |
| policy_issue | 18 PI | 平台撰寫 |
| statistical_indicator | 27 | 平台定義 |
| **stat_value** | **137 筆** | **8 關鍵指標 18 年完整時序** |
| stakeholder | 19 | 平台識別 |
| advocacy_event | 25 | 主動爬蟲 |
| policy_change | 10 | 平台識別 |
| outcome_assessment | 8 | 平台分析(含 H₂ 反證)|
| **document** | **33** | **歷年 CEDAW 21 PDF + 3 GEPolicy + 其他** |
| **document_version** | **33** | 對應 |
| **domestic_law** | **12** | **婦女主要法律** |
| **law_amendment** | **30** | **30 修法歷程含 trigger 事件** |
| vocab_*(7 表)| 86 | 平台規範 |

### 仍空(7 表 — 後續優先補)
| 表 | 補強建議 |
|---|---|
| nap_action | 抓 NAP 主文件 154 行動之婦女章節 |
| nhrc_indicator | 等 NHRC 婦女章節監督報告公開 |
| recommendation | 從 PI 卡 §五 抽出入庫(可半自動)|
| case_story | 倫理紅線高,僅在三方覆核後才入 |
| media_coverage | 寫 fetch_media.py 抓主要媒體 |
| submission_raw | 等 Tally 表單啟動 |
| axis4_evidence | 從 PI 卡軸四章節抽出入庫 |
| passage(FTS)| 從 33 文件抽段落入 FTS 全文索引 |

## 二、檔案系統狀態

| 類別 | 數量 | 完整度 |
|---|---:|---|
| Source PDFs(raw) | 35 | ✅ 主要文件已抓 |
| Source TXTs(clean) | 35 | ✅ 全部解析 |
| 議題卡(中文) | 18 | ✅ Tier 1+2 完成 |
| 議題卡(英譯) | 3 | 🟡 17% — 待補 15 |
| HTML 部署檔 | 39 | ✅ 主頁 + 18 issues + 18 trace + axis4 |
| 影子報告(本平台) | 1 | 🟡 v0.1 草稿 — v0.2 待補 |

## 三、四軸進度(對外發布視角)

| 軸 | 進度 | 缺口 |
|---|---|---|
| 一 CO 兌現 | ✅ 完整(212 段)| — |
| 二 NAP / 性平綱領 | 🟡 性平綱領 2017 已分析 + NAP foreword | NAP 主文件、綱領 5 版時序 |
| 三 20 年指標 | 🟡 8 關鍵指標完整 | 19 個指標仍稀疏 |
| 四 框架擴張 | ✅ 主場(PI-21/22/23/24/25/26/27)+ 追溯鏈 | 軸四 axis4_evidence 表未抽出 |

## 四、追溯鏈完整度(Wave 53-58 + 60-64 後)

```
stakeholder (19) → advocacy_event (25)
                       │
                       ↓ rel_event_change (11) + rel_event_amendment (4)
                       ↓
              policy_change (10) + law_amendment (30)
                       │
                       ↓ rel_issue_outcome (11)
                       ↓
              outcome_assessment (8)
                       │
                       ↓ rel_co_policychange (0 — 待補)
                       ↓
              concluding_observation (212)
```

完整因果關聯數:**169+(stakeholder ↔ event ↔ change ↔ amendment ↔ outcome ↔ co)**

## 五、Wave 65+ 路線

| 優先 | Wave | 目標 |
|---|---|---|
| 高 | 65 | 從 PI 卡 §五 抽出 recommendation 入庫 |
| 高 | 66 | 寫 fetch_nap_full.py 抓 NAP 主文件 154 行動 |
| 中 | 67 | 剩餘 15 PI 英譯批次(支援 CEDAW 第 5 次審查國際對接)|
| 中 | 68 | 影子報告 v0.2(納入 33 份文件實證 + 12 部法律修法)|
| 中 | 69 | passage 全文索引(從 35 source TXT 切段入庫)|
| 低 | 70 | 第 5 輪獨立 QA |

## 六、回應用戶「資料齊全嗎?」

**短答**:從 **55%**(Wave 59)→ **70%**(Wave 65 後)

主要躍進:
- 影子報告 PDF: 1 → **22**(本平台 + 21 歷年 CEDAW 文件)
- domestic_law: 0 → **12**(主要婦女法律)
- law_amendment: 0 → **30**(含 trigger 事件)
- document 主表: 0 → **33**
- 指標時序: 74 → **137**(8 關鍵指標 18 年連續)
- 議題追溯關聯: 49+18+11 → **169+**(加 32 PI-法律 + 4 事件-修法)

仍待補:
- NAP 154 行動主文件
- recommendation 跨 PI 抽取
- passage 全文索引
- 15 PI 英譯
- 影子報告 v0.2
