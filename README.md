# ESG-Rating-Statistical-Analysis
Statistical analysis of the CMoney Taiwan ESG Rating TOP100 dataset. Explores the relationship and predictive power of E, S, and G components on overall ESG ratings using Chi-squared tests and Multinomial Logistic Regression.

# Relationship Between ESG and Its Components (E, S, G)
## 台灣企業 ESG 總評分與各分項（環境、社會、公司治理）之關聯性與預測模型分析

**作者：** 潘皓心（統計所碩一）  
**課程：** 統計方法（Statistical Methods）期末專案  

---

## 📋 專案簡介 (Project Overview)
隨著永續發展成為全球企業評估長期價值的重要指標，ESG（環境 Environmental、社會 Social、公司治理 Governance）評級備受關注。本專案基於 **CMoney 台灣 ESG 評級 TOP100（CMoney Taiwan ESG Rating TOP100）** 資料集，運用統計檢定與多分類預測模型，探討 E、S、G 三大構面對整體 ESG 評級的影響力與預測能力。

本研究比較了兩種不同顆粒度的評級分類方式（10 級數值評分 vs. 高中低三分類），驗證類別合併在處理小樣本資料集時對模型穩健性與預測準確率的提升效果。

---

## 📂 資料集與變數設計 (Dataset & Categorization)
* **資料來源**：CMoney Taiwan ESG Rating TOP100（共 100 筆觀察值，10 個變數）。
* **核心變數**：整體 ESG 評級（依變項）、環境評分（E）、社會評分（S）、公司治理評分（G）（自變項）。
* **分類方法設計**：
  * **Method 1（原始數值等級）**：保留 1–10 的序數等級。
  * **Method 2（三分類序數等級）**：將評分重新劃分為 **Low (1–5)**、**Medium (6–7)** 與 **High (8–10)** 三個類別，以緩解極端值樣本過少的問題。

---

## 🔬 統計方法與分析流程 (Methodology)
本專案使用 **R / RStudio**（主要套件包含 `nnet` 與 `pROC` 等）進行以下分析：
1. **敘述性統計分析**：檢視整體 ESG 與 E、S、G 分項在兩種分類法下的次數分布（主要集中於 7–8 級或 Medium / High 區間）。
2. **卡方獨立性檢定 (Chi-Squared Test)**：採用蒙地卡羅模擬 p 值（1,000 次重複抽樣），檢驗整體 ESG 評級與 E、S、G 各分項之間是否存在顯著統計關聯。
3. **多元羅吉斯迴歸 (Multinomial Logistic Regression)**：建構 `multinom(esg ~ e + s + g)` 模型，評估 E、S、G 對整體 ESG 評級的多分類預測能力。
4. **模型表現評估**：透過 **Multi-class AUC**、**Accuracy（準確率）**、**Residual Deviance（殘差偏差）** 與 **AIC（赤池資訊準則）** 比較兩種分類方法的優劣。

---

## 📊 核心分析結果 (Key Results)

### 1. 卡方檢定結果 (Chi-Squared Test)
在 Method 1 與 Method 2 下，整體 ESG 評級與 E、S、G 三項指標皆呈現高度顯著關聯（$p = 0.001$），其中又以**公司治理（G）**的卡方統計量最高。

### 2. 多分類模型表現比較 (Model Performance)
| 評估指標 | Method 1 (1–10 級) | Method 2 (Low / Medium / High) |
| :--- | :---: | :---: |
| **Accuracy (準確率)** | 87.0% | **91.0%** |
| **Multi-class AUC** | **0.9777** | 0.9561 |
| **Residual Deviance** | 54.22 | **46.56** |
| **AIC** | 234.22 | **74.56** |

---

## 💡 研究結論與反思 (Conclusion & Discussion)
* **分類顆粒度的重要性**：在樣本數有限（$N = 100$）的情況下，Method 1 因類別過多且部分等級樣本數極少，導致模型參數估計變異較大（AIC 較高）；改採三分類的 **Method 2** 後，AIC 大幅下降且預測準確率提升至 **91%**，展現更佳的模型配適度與泛化表現。
* **資料不平衡限制**：無論採用哪種分類法，TOP100 企業的評分多集中於中高段（Medium 與 High）。未來研究可擴大納入全市場企業樣本，以提升模型在低評級區間的穩健性。

---
