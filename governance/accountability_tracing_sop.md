# 議題追溯責任歸屬 SOP — 「誰倡議?誰執行?誰受益?誰受害?」

> **建立日**:2026-04-30 / Wave 57
> **目的**:讓任何議題可被追溯為「倡議者 → 政府回應 → 政策變化 → 結果指標 → 國際 CO 評估 → 反思誰受益/受害」
> **適用對象**:本平台 13 governance 文件之延伸,主編 + DPO + 律師覆核必讀
> **核心精神**:**假設驗證(hypothesis testing)**,而非預設結論

---

## 一、為何需要追溯鏈

過去政策監督多停留在「靜態議題卡」(這個議題是什麼)。但**負面結果出現時**,公民無法回答:

- **誰倡議造成的?**(who advocated)
- **誰執行的?**(which agency acted)
- **誰受益?**(who benefited)
- **誰受害?**(who paid the cost)
- **如果當時沒做,結果會如何?**(counterfactual)
- **下次怎麼改?**(reform direction)

本平台之**追溯鏈** schema(Wave 53)以 4 表 + 4 關聯表建構這個動態因果圖:

```
stakeholder(誰)
  ↓
advocacy_event(在何時發起什麼倡議)
  ↓ rel_event_change(因果強度:direct/contributory/context)
policy_change(政府如何回應)
  ↓
outcome_assessment(誰受益/誰受害)
  ↓ rel_co_policychange(國際 CEDAW 委員會事後評估)
concluding_observation
```

---

## 二、查詢實例(trace_issue.py)

```bash
# 對單一議題追溯全鏈
python3 scripts/trace_issue.py PI-21

# 只列「擴張派」倡議事件(假設他們是錯誤引導)
python3 scripts/trace_issue.py PI-21 --expand-only

# 全部擴張派 stakeholder 之時間軸(獨立分析)
python3 scripts/trace_issue.py --all-expand

# 特定議題之受益/受害群體分析
python3 scripts/trace_issue.py --who-benefits PI-22
```

**範例輸出(PI-21)**:
- 11 個倡議事件(2009 婦女新知 第 1 次影子報告 → 2026 護家護兒聯盟 第 5 次影子報告)
- 4 個政策變化(2017 性平綱領 v4 / 2019 同婚專法 / 2021 免術換證 / 2024 綱領 v6 待修)
- 1 個受益受害評估(2017 綱領擴張 → 婦女實質權益受害)
- 4 個國際 CO 段落

---

## 三、核心方法論:**假設驗證**(hypothesis testing)

⚠ **本 SOP 之倫理紅線**:平台主辦方(護家護兒聯盟)立場為「假設擴張派錯誤引導政策」,但**追溯鏈不可預設結論**,必須以實證驗證或反駁。

### 3.1 三種假設並列

對每個議題,平台應同時記錄三種假設:

| 假設 | 說明 |
|---|---|
| **H₁ 擴張派錯誤論** | 擴張派倡議導致婦女實質權益退步 |
| **H₀ 無關論**(虛無假設)| 擴張派倡議與婦女實質指標退步無因果 |
| **H₂ 反向論** | 擴張派倡議實質提升婦女與多元群體權益 |

### 3.2 證據等級

| 等級 | 證據 | 例 |
|---|---|---|
| 🟢 強(direct)| 政策文件直接引用倡議,且時間順序明確 | 2017 性平綱領 v4 引述婦女新知 2014 影子報告 |
| 🟡 中(contributory)| 時間順序合理,但無直接引用 | 2014 CEDAW CO §63 之擴張派 NGO 倡議 |
| 🔴 弱(context)| 僅時間相近,因果不明 | 同婚專法後 2 年 GPG 反向 |
| ❌ 反證 | 反向證據(指標反而進步)| 2023 性平三法修法後性騷擾申訴增 +900%(屬婦女實質進步)|

### 3.3 避免歸因謬誤

- **後此謬誤**(post hoc):X 之後 Y 發生,**不等於** X 導致 Y
- **共變謬誤**:X 與 Y 同時變化,**不等於** X 與 Y 因果
- **反事實思考**:**「若沒有這項倡議,結果會如何?」**(counterfactual,outcome_assessment.counterfactual 欄位)

---

## 四、責任歸屬(accountability)之 5 個層次

針對任何「結果」(outcome),問:

1. **倡議責任**:誰提出此議程?(advocacy_event.stakeholder)
2. **立法責任**:立法院 / 立委如何投票?
3. **執行責任**:行政機關如何執行?(policy_change.enacting_agency)
4. **監督責任**:NHRC / NGO / 媒體 是否有效監督?
5. **學術 / 司法責任**:學者 / 法官 / 司法院 如何詮釋?

每一層皆有名字、職位、文件,可追究。

---

## 五、五種反思路徑(下次怎麼改?)

### 5.1 撤回擴張(rollback)
- 若假設 H₁ 成立,且**反證不足**:倡議撤回該政策
- 例:性平綱領 v6 章節體例回歸 CEDAW 16 條結構(對應 PI-22 主張)

### 5.2 加強限縮(narrow)
- 政策保留但加守備
- 例:免術換證後加強婦女空間 sex-based 分流(對應 PI-23/24/25)

### 5.3 平行框架(parallel)
- 不撤回擴張派議程,但另立獨立框架
- 例:LGBTQ 議題透過《性別認同法》草案處理,不擠壓 CEDAW

### 5.4 補償受害(compensation)
- 對因擴張政策受害之群體提供救濟
- 例:對受暴婦女庇護所空間擔憂,衛福部建立分流機制

### 5.5 學習機制(learn)
- 將個案納入下一輪 CEDAW 影子報告 + NAP 評估指標

---

## 六、優化方向(本 wave 之反思)

### 6.1 已做到

- ✅ schema 4 表 + 4 關聯表建構完整因果鏈
- ✅ 18 stakeholders / 15 倡議事件 / 7 政策變化 / 5 結果評估 入庫
- ✅ trace_issue.py 4 種查詢模式(全鏈 / 擴張派專項 / 受益受害 / 時間軸)
- ✅ position_axis4 標籤明確區隔擴張派 vs 反擴張派
- ✅ rel_event_change 因果強度三級(direct/contributory/context)避免過度歸因

### 6.2 仍需強化(Wave 58+ 路線)

| # | 缺口 | 補強建議 |
|---:|---|---|
| 1 | 倡議事件僅 15 筆,需擴充至 50+ | 用 WebFetch 抓 2009-2024 婦女新知/熱線/伴侶盟 之歷年新聞稿 + 影子報告 |
| 2 | 反證機制未啟動(全部假設 H₁ 走向)| Wave 58 補加 outcome_assessment 中之**反證紀錄**(如 2023 性平三法 → 婦女實質進步) |
| 3 | 立法院投票紀錄未入庫 | 寫 fetch_ly_vote.py 抓立法院公報投票記名 |
| 4 | 個別立委責任追蹤缺失 | 加 stakeholder type=legislator + 投票紀錄關聯 |
| 5 | counterfactual 多為文字,缺結構化 | Wave 58 加 counterfactual_assessment 表 |
| 6 | 視覺化(timeline / 知識圖譜)未實作 | Wave 56 timeline.html(D3.js)+ Wave 60 知識圖譜(Cytoscape)|
| 7 | 「擴張派」標籤本身可能不準確 | 部分團體立場隨時間變化,需 stakeholder_position_history 表記錄變遷 |

---

## 七、潛在的方法論風險與紅線

### 7.1 標籤化風險

`stakeholder.position_axis4 = 'expand'` 標籤雖有 governance §五紅線約束,但仍有:

1. **標籤過度簡化**:婦女新知近 10 年漸進擴張,但 1980-90 年代是純粹婦運;不能一概而論
2. **標籤政治化**:外界可能解讀為「敵我區分」
3. **預設結論**:即使標明「假設驗證」,實務上易滑入「擴張派 = 錯誤」

### 7.2 governance §五紅線必守

- 不使用攻擊性語言指稱擴張派 stakeholder
- 引用對立方論述必含 URL(advocacy_event.source_url)
- 反駁以證據(統計 / 法規 / 學術文獻)為主
- outcome_assessment.accountability_note 須中立敘述

### 7.3 資料缺口應公開承認

`outcome_assessment.indicator_changes` 若為 NULL,應改為 `(待 Wave N 補)`,**不可不寫**。

---

## 八、與既有 governance 之關聯

| 既有文件 | 本 SOP 之關聯 |
|---|---|
| `INDEX.md` §五 軸四紅線 | 本 SOP §七.2 直接套用 |
| `axis4_position_statement.md` | 平台立場聲明,本 SOP 為實證驗證 SOP |
| `content_sop.md` §六 軸四專屬 SOP | 本 SOP 補充「責任歸屬」面向 |
| `ai_use_policy.md` §四 | AI 不得讀 axis4_evidence 表;trace_issue.py 同樣 AI 限讀 |

---

## 九、修訂歷史

- v1.0 / 2026-04-30 / Wave 57 / 初版,因應用戶要求建立議題追溯責任歸屬機制
