本專案為一個完整的 心率變異性 (HRV) 機器學習分析流程，
資料來源為研究專案：

《診斷與自律神經標誌數據 (VNS 研究，2025-08-13)》

此流程結合資料前處理、特徵工程、PCA/UMAP 降維視覺化與多模型比較，
用以探索 HRV 指標與心理疾病（SSD、MDD、Panic、GAD）之間的關聯性。

⚙️ 分析流程特色

1. 資料清理

   將所有 HRV 與基本欄位轉為數值型

   移除極端離群值（IQR，3 倍範圍）

   自動處理 LFHF<0 的無效值

2. 特徵工程

   新增多種交互與比率特徵：

   LF_HF_ratio = LF / HF

   LF_plus_HF = LF + HF

   Age_BMI_interaction = Age × BMI

   SDNN_SC_ratio = SDNN / SC

   支援 log1p 對數轉換 改善偏態分布

   使用 RobustScaler / QuantileTransformer 提升穩定性

3. 缺失值處理

   類別型：使用眾數 (SimpleImputer)

   數值型：使用鄰近值補全 (KNNImputer)

   自動生成缺失報告

4. 降維分析

   PCA：主成分解釋變異量與累積曲線

   UMAP：非線性投影可視化標籤群集

   特徵重要性分析

   mutual_info_classif

   RandomForest feature_importances_

   生成整合式權重排名表與圖表

5. 分類模型建構

   Logistic Regression

   Random Forest

   Gradient Boosting

   Support Vector Machine

   以 5-Fold Stratified CV 評估，並計算：

   ROC-AUC、AP、F1

   SMOTE 平衡過取樣
