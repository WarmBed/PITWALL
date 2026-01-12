
## What is this?

PitWall is an  **F1 data analysis** and telemetry visualization tool.  
It allows  data fans to analyze lap times, throttle usage, speed traces, and driver comparisons using real Formula 1 telemetry.


A professional Formula 1 telemetry analysis workstation providing comprehensive race data analysis capabilities.

![PITWALL](/images/Page01.png)


---

## 1. 歷史靜態分析 (Historical Analysis)

此群組包含針對賽後數據進行的深度分析工具，涵蓋策略、輪胎、事故與賽道環境等面向。
(/images/Page02.png)
### 1.1 賽事溫度環境 (Temperature Analysis)
    本模組專門用於可視化賽事週末的環境數據變化。它不僅顯示賽道溫度 (Track Temp) 和空氣溫度 (Air Temp)，還整合了濕度 (Humidity)、氣壓 (Pressure) 以及降雨量 (Rainfall) 的即時數據流。透過時間軸的對齊，使用者可以精確分析環境變因如何影響特定圈數的圈速表現或輪胎衰退情況。底層數據支援動態切換年份與賽式，並具備自動縮放的時間軸圖表功能。

### 1.2 賽道與彎道分析 (Track Analysis)
    此模組負責繪製高精度的賽道地圖，並標註官方定義的所有彎道編號與 DRS 檢測/啟動區域。它利用 API 獲取的向量數據來渲染賽道幾何形狀，並支援疊加顯示車手的行駛軌跡或遙測數據（如速度熱圖）。程式碼中內建了座標轉換邏輯，能將 GPS 座標轉換為螢幕上的 XY 繪圖座標，是分析車手走線與賽道特性的基礎工具。

### 1.3 進站策略分析 (Pitstop Analysis)
    本模組提供詳盡的進站數據分析，分為「車隊匯總」與「詳細日誌」兩個視圖。它能計算每位車手的進站次數、平均停站時間 (Stationary Time) 以及進出的總損失時間 (Total Pit Loss)。系統內建了智能過濾器，能區分正常進站與通過維修區 (Drive-through)，並顯示每次換胎前後的輪胎配方變化。若 API 連線失敗，模組具備自動切換至本地 `pit_stops.json` 檔案的後備機制 (Fallback Mechanism)。

### 1.4 事故與旗號分析 (Accident Analysis)
    此工具專注於統計與視覺化賽事中的中斷事件，包括黃旗 (Yellow Flag)、紅旗 (Red Flag)、虛擬安全車 (VSC) 與實體安全車 (SC)。它會以時間軸甘特圖 (Gantt Chart style) 的形式展示這些事件的持續時間與發生當下的圈數。這對於分析比賽節奏的改變、車隊策略的應變點以及計算比賽有效圈數至關重要，並且能關聯到具體的退賽 (DNF) 原因分析。

### 1.5 輪胎策略歷程 (Tire Strategy Analysis)
    這是分析車手輪胎使用策略的核心模組，採用直觀的橫向條形圖展示每位車手的輪胎使用歷程 (Stints)。每一段條形圖代表一套輪胎，顏色對應輪胎配方 (紅/黃/白/綠/藍)，長度對應使用圈數。模組內部演算法會計算每個 Stint 的平均圈速與衰退趨勢，並標註出是全新胎 (New) 還是使用過的舊胎 (Used)。這讓使用者能一目了然地對比不同車隊的一停 (1-stop) 或多停策略差異。

### 1.6 車手位置追蹤 (Driver Run Position)
    本模組繪製整場比賽的車手排名變化折線圖 (Position Chart)，橫軸為圈數，縱軸為排名。它特別處理了退賽 (DNF) 車手的顯示邏輯，確保留在賽道上的車排名計算正確。程式碼中包含互動式圖例 (Legend)，允許使用者快速篩選特定車手進行對比，例如只觀察前三名之爭或中游集團的激烈纏鬥。數據源直接來自官方計時系統的分圈排名數據。

### 1.7 賽道交通分析 (Traffic Analysis)
    此進階模組用於量化車手在比賽中遇到的交通狀況 (Traffic)。它通過計算車手與前後車輛的時間差 (Gap)，來判定車手是處於乾淨空氣 (Clean Air) 還是受前車亂流影響的髒空氣 (Dirty Air) 中。分析結果通常以熱圖或區間圖呈現，顯示車手在多少比例的比賽里程中受到阻擋，這對於評估車手真實配速 (True Pace) 與進站窗口選擇 (Pit Window) 非常關鍵。

---

## 2. 遙測數據分析 (Telemetry Analysis)

此群組提供基於採樣 (Hz) 的車輛物理數據分析，用於精細對比駕駛風格與車輛性能。
![PITWALL](/images/Page03.png)
### 2.1 主遙測視窗 (Main Telemetry Analysis)
    這是系統中最強大的遙測分析工具，支援同步顯示速度 (Speed)、轉速 (RPM)、檔位 (Gear)、油門 (Throttle)、煞車 (Brake) 與 DRS 狀態等多個數據通道。它採用高效能繪圖引擎，支援多車手數據疊加 (Overlay) 對比，並具備游標同步功能 (Cursor Synchronization)，當使用者在某個圖表移動滑鼠時，所有相關圖表會同步顯示該時間點的數值。此模組依賴 `fastf1` 核心進行數據對齊與重採樣。

### 2.2 各通道詳細分析 (Channel-Specific Analysis)
以下模組是主遙測功能的拆分優化版，針對特定物理量進行深入分析：

*   **速度分析 (Speed Analysis)**
    *   **說明**: 專注於速度曲線的細節，提供更精細的 Y 軸刻度與平滑化處理，方便觀察彎中最低速 (Minimum Corner Speed) 與直線尾速 (Top Speed)。

*   **煞車分析 (Brake Analysis)**
    *   **說明**: 分析煞車踏板的輸入壓力與持續時間，幫助判斷車手的煞車點 (Braking Point) 深淺與 Trail-braking 技巧的運用。

*   **油門分析 (Throttle Analysis)**
    *   **說明**: 檢視油門開度的線性變化，特別用於分析出彎加速時的牽引力控制 (Traction) 與車手對油門的細膩操作。

*   **檔位與轉速 (Gear & RPM)**
    *   **說明**: 這兩個模組通常結合使用，用於分析車手的換檔時機 (Shift Points) 與變速箱齒比策略，以及引擎在不同轉速區間的輸出特性。

*   **加速度分析 (Acceleration Generic)**
    *   **說明**: 計算縱向加速度 (Longitudinal G) 與橫向加速度 (Lateral G)，生成 G-G 圖 (G-G Diagram)，用於評估輪胎抓地力極限與車輛綜合過彎性能。

### 2.3 差異分析 (Delta Analysis)
    *   直接計算兩車在賽道同一位置的速度差值，直觀顯示哪輛車在彎道或直線更快。
    *   積分速度差來計算兩車在空間上的距離變化，用於分析追擊戰中距離是如何被拉近或拉開的。
    *   這是最傳統的 "Delta" 曲線，顯示車手在單圈過程中相對於參考圈的時間得失，幫助車手識別哪個彎角損失了時間。

---

## 3. 圈速性能分析 (Lap Performance)

此群組關注於單圈時間的統計特性、穩定性以及長距離測試表現。
![PITWALL](/images/Page04.png)
### 3.1 詳細圈速數據表 (Detailed Lap Data)
    提供一個功能豐富的數據表格，列出選定車手每一圈的詳細資訊。欄位包含圈數、單圈時間、S1/S2/S3 分段時間、通過測速點的尾速 (Speed Trap)、輪胎配方與壽命。模組還會透過演算法標記出異常圈 (如黃旗影響、Box 出場圈)，並用顏色區分個人最快 (Green) 與全場最快 (Purple) 成績，是工程師檢查數據完整性的首選工具。

### 3.2 圈速分佈箱型圖 (Lap Time Box Plot)
    利用統計學箱型圖 (Box-and-Whisker Plot) 來可視化車手的圈速分佈。圖表顯示中位數 (Median)、四分位距 (IQR) 以及極端值 (Outliers)。這能有效過濾掉進站圈或慢車阻擋圈的干擾，真實反映車手在正賽中的平均配速能力 (Pace) 與單圈穩定性 (Consistency)。箱體越窄，代表車手表現越穩定。

### 3.3 彎道油門控制統計 (Throttle Corner Analysis)
    這組模組將油門數據與賽道彎道結合。它統計車手在通過特定彎道時的平均油門開度或全油門比例，並以箱型圖或折線圖呈現。這有助於分析車手在不同彎角的信心程度、輪胎抓地力狀況，以及出彎時提早補油的能力，是評估車手 "彎道極限" 的重要指標。

### 3.4 踏板行為分析 (Pedal Behavior Analysis)
![PITWALL](/images/Page16.png)
    本模組以疊加棒狀圖 (Stacked Bar Chart) 呈現每位車手的踏板使用狀態分佈。系統將踏板行為分類為四種狀態：
    *   **Throttle Only (全油門)**: 僅踩下油門踏板，通常出現在直線加速或出彎全開時。
    *   **Brake Only (全煞車)**: 僅踩下煞車踏板，對應進彎前的重煞車區。
    *   **Trail Braking (拖煞)**: 油門與煞車同時操作，這是高階駕駛技巧，用於入彎時維持車身平衡並最大化過彎速度。
    *   **Coasting (滑行)**: 兩個踏板皆未踩下，代表車手在進行慣性滑行或 Lift and Coast 省油操作。

### 3.5 長距離模擬與衰退 (Long Run Analysis)
    本模組專為分析自由練習賽 (FP2) 的長距離模擬數據而設計。它內建了 **Stint Detection 演算法**，能自動識別出連續的高載油計時圈。核心功能包括 **燃油修正 (Fuel Correction)**，即根據每一圈消耗的燃油重量來反推修正後的圈速，從而計算出剔除車重影響後的純粹輪胎物理衰退率 (Degradation Rate)，是制定正賽停站策略的關鍵依據。

---

## 4. 理想圈與分段分析 (Ideal Lap & Sectors)

此群組透過重組最佳分段數據，探索車手與車輛的理論極限性能。
![PITWALL](/images/Page05.png)
### 4.1 理想圈排名表 (Ideal Lap Ranking)
    模組會計算每位車手的「理論最佳圈速」(Theoretical Best)，即將該車手在整場比賽中跑出的最佳 S1、S2 與 S3 時間相加。表格將此理論時間與實際桿位時間進行對比，計算出 "Potential Gap"。這能揭示車手是否因為失誤而未能跑出應有的成績，或者車輛在特定分段是否具有隱藏的性能優勢。

---

## 5. 速度表現與車輛動態 (Speed & Corner Analysis)


### 5.1 極速與直線性能 (Straight Line Speed)
![PITWALL](/images/Page06.png)
    統計並比較所有車手在賽道主要直線底端的最高速度 (Top Speed/Trap Speed)。這能反映車輛的空氣阻力設定 (Drag Level) 以及引擎馬力輸出強弱。模組通常會過濾掉使用 DRS 或尾流 (Tow) 的異常數據，以評估車輛在純淨空氣下的本質直線性能，幫助判斷下壓力設定是否過大。

### 5.2 煞車與加減速性能 (Brake & Acceleration Performance)
    透過散佈圖 (Scatter Plot) ，分析各車隊在重煞車區域的減速度 。同時比較出彎加速階段的縱向 G 值累積。這些數據直接關聯到車輛的機械抓地力 (Mechanical Grip) 與煞車系統效能，能清楚區分出哪些車輛擅長 "Stop-and-Go" 佈局的賽道，哪些則在流暢彎道更有優勢。
![PITWALL](/images/Page08.png)

### 5.3 彎速性能分級 (Corner Performance)
    本模組將賽道彎道依據通過速度分類為：低速彎 (Low Speed)、中速彎 (Medium Speed) 與高速彎 (High Speed)。它會計算車手在各類彎道的平均最低彎速 (Minimum Apax Speed)。揭示車輛在不同空力負載下的平衡性 (Balance)，例如某車隊可能在依賴空力的高速彎極快，但在依賴機械抓地力的低速彎掙扎。
![PITWALL](/images/Page07.png)
---

## 6. AI 預測模型 (Prediction Models)
![PITWALL](/images/Page09.png)
*   **FP3/FP2 → 排位預測**: 
    收集自由練習賽的圈速、輪胎配方與燃油載重假設，透過回歸模型預測車手在排位賽的潛在最快單圈。
*   **Q → 正賽預測**: 
    基於排位賽成績與歷史賽道的超車難易度係數，模擬正賽的最終排名分佈，為策略組提供期望值參考。

---

## 7. 多賽季分析 (Multi-Season Analysis)

### 7.1 歷年賽道旗幟統計 (Historical Track Map)
![PITWALL](/images/Page010.png)
    此模組整合了賽道地圖、高程剖面圖 (Elevation Chart) 與年度旗幟統計表格。它利用 API 獲取歷年的事故位置 (X, Y 座標) 與類型，並將其標註在賽道圖上。系統還會分析賽道的高程變化 (Elevation Change)，幫助識別事故熱點是否位於盲彎或起伏路段。右側面板統計了近四年 (2022-2025) 的黃旗、紅旗與安全車次數，提供宏觀的賽道安全特性評估。

### 7.2 年度起跑反應分析 (Season Start Reaction)
![PITWALL](/images/Page11.png)
    專注於分析車手在整個賽季中的起跑表現，具體指標為 0-50km/h 加速時間分佈。模組使用箱型圖 (Box Plot) 來展示每位車手的反應時間中位數與穩定性範圍 (IQR)。這能有效過濾掉雨戰或起步事故的極端值，真實反映車手的平均起步水準。支援車隊配色顯示，方便橫向對比隊友間的起步能力差異。

---

## 8. Live Timing (實時賽況)
![PITWALL](/images/Page12.png)
### 8.1 核心監控組件 (Core Monitoring)
*   **Ranking Tower**:
    高度優化的即時排行榜，顯示排名、車手代號、輪胎資訊、區段時間 (S1/S2/S3) 與目前狀態 (Pitting/Out)。支援動態排序動畫與車隊顏色顯示。
*   **Track Map**:
    實時顯示所有車輛在賽道上的位置。不同於靜態分析圖，它主要關注車輛間的相對位置與追擊動態，並用不同顏色標記領先集團。
*   **Circle Map**:
    將賽道抽象化為一個圓環，直觀展示車手之間的秒數差距 (Gap)。這是判斷 "Safety Car Window" 或 "Pit Window" 是否安全的最佳工具。
*   **Track & Weather**:
    頂部資訊列，即時顯示賽事名稱、比賽時間、圈數進度與 Track Status (綠/黃/紅旗/SC/VSC)。第二行提供詳細天氣數據：空氣溫度、賽道溫度、濕度、氣壓、風速與風向。

### 8.2 策略與預測 (Strategy & Prescription)
![PITWALL](/images/Page15.png)
*   **Driver Strategy**:
    顯示預測圈速曲線 (Predicted) 與實際圈速 (Actual) 的對比圖。包含預測區間 (Prediction Range)、SC 區域與進站標記，幫助策略師判斷車手表現是否符合預期模型。
*   **Battle Insight**:
    針對特定纏鬥組合 (Battle Pair) 進行深入分析，實時計算兩車的速度差、DRS 可用性與預計超車圈數。
*   **Chase Strategy**:
    追擊策略計算器，根據當前兩車圈速差與剩餘圈數，預測追擊者是否能在比賽結束前進入 DRS 攻擊範圍。
*   **Pit Window**:
    即時計算並在地圖上標記出車手進站後的預計回到賽道位置 (Rejoin Position)，考慮了維修區通過時間與賽道交通狀況。
*   **Tyre Strategy**:
    監控全場車手的輪胎使用圈數 (Age) 與預測剩餘壽命。結合 Pirelli 的輪胎衰退曲線，預警車手何時可能出現性能懸崖 (Cliff)。

### 8.3 遙測與性能分析 (Telemetry & Performance)
![PITWALL](/images/Page13.png)
*   **Real-time Telemetry Traces**:
    提供各類物理量的實時波形圖，支援多車對比：
    *   `speed_trace`: 速度曲線。
    *   `throttle_trace`: 油門開度。
    *   `brake_trace`: 煞車壓力。
    *   `rpm_trace`: 引擎轉速。
    *   `gear_trace`: 檔位變化。
    *   `drs_trace`: DRS 啟用狀態。
*   **Sector Comparison**:
    專門比較兩位車手在特定分段 (S1/S2/S3) 的時間差。採用類似 Speed Trace 的雙線圖設計，明確標示出在哪個彎角拉開了差距。
*   **SF% History**:
    Stint Fuel Saving Percentage 歷史圖表。計算車手每一圈的省油程度 (Lift and Coast)，正值代表強力推進，負值代表在進行省油管理，並以顏色深淺 (亮綠/暗綠) 區分強度。
*   **Top Speed History**:
    表格形式列出每位車手每一圈的尾速 (Top Speed)。紫色字體自動標記出該車手的個人最高速，是監控引擎模式與尾流效應的重要依據。

### 8.4 歷史數據與統計 (History & Stats)
![PITWALL](/images/Page14.png)
*   **Lap History Tables**:
    包含四個獨立表格模組：`Lap Time`, `S1`, `S2`, `S3`。以熱圖表格顯示全場車手每一圈的成績，自動標記全場最快 (紫色) 與個人最快 (綠色)。
*   **Lap Time Distribution**:
    視覺化全場車手的圈速分佈。以最快圈為基準，將所有車手與領先者的差距 (Gap) 繪製在垂直軸上，右側顯示輪胎配方，能一眼看出集團分佈與掉隊車手。
*   **Live Traffic Timeline**:
    熱圖形式的交通狀況時間線。顯示每位車手每一圈是處於 "Clean Air" (綠色) 還是 "Traffic" (橘色) 狀態，判斷依據為與前車的距離。
*   **Traffic Distance**:
    統計表格，量化每位車手在比賽中受到前車阻擋的比例 (Traffic Ratio) 與圈數，僅在 API-Only 模式下讀取 JSON 數據。

### 8.5 其他 (Others)
*   **Race Control**:
    即時串流賽會控制中心的訊息，包括旗號變更 (Flag Changes)、調查通知 (Investigation) 與判罰結果 (Penalties)，並支援關鍵字過濾。
