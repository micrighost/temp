# 一星一陽突破策略

## 簡介
一星一陽突破策略主要依賴於一星二陽的K線形態，當出現一星一陽時進行進場操作，期待價格能夠突破並持續上漲或下跌。

## 版本
- **版本**: 1.00

## 安裝步驟
1. 將 `一星一陽突破策略.mq5` 文件放入 MetaTrader 5 的 `Experts` 目錄中。
2. 打開 MetaTrader 5，並在導航欄中找到「專家顧問」。
3. 右鍵點擊「專家顧問」，選擇「重新加載」以加載新的策略。
4. 將策略拖放到圖表上，並根據需要進行設置。

## 使用說明
- **參數設置**:
  - **Lot**: 交易手數，默認為 `0.01`。
  - **CrossBodyThreshold**: 十字K最大實體比例（1%）。
  - **ThresholdMagnification**: 第二根K棒漲跌幅需達第一根實體的10倍。
  - **UpperLowerShadowThreshold**: 第二根K棒上下引線最大佔比要小於總漲幅的1%。
  - **MinShadowRatio**: 十字K棒上下引線最少要是實體的三倍。

- **策略邏輯**:
  - 當出現一星二陽的形態時，若出現一星一陽，則進場卡位。
  - 十字K（星）的實體需小於1%（漲跌幅），且上下引線需是實體的3倍(防止停損過小)。
  - 長紅K（陽）的實體需是十字K實體的10倍，且上下引線佔的總漲跌幅小於1%。
  - 星最高點要高於陽才能開多單。
  - 當前兩根K棒的條件滿足，且現價突破十字K的高點，則開多單，停損設在十字星K棒的底部，盈虧比為1:2。
  - 空單的條件與多單相反。

## 函式說明
- `OnInit()`: 初始化函式，EA啟動時執行，設置指標和參數。
- `OnDeinit(int reason)`: 程式結束函式，EA停用時執行。
- `OnTick()`: 主執行函式，每次收到新Tick觸發計算，檢查價格行為並執行交易。
- `GetBarPrice(int index, double &open, double &high, double &low, double &close)`: 獲取指定K棒的開盤價、高價、低價和收盤價。
- `HasPosition()`: 檢查是否已有持倉。
- `IsNewBar()`:判斷是否新K棒生成 (用時間判斷)。
- `BodyPercent(double open, double close)`: 計算K棒實體長度百分比（收盤與開盤的絕對差 / 開盤）。
- `UpperShadowPercent(double open, double close, double high)`: 計算K棒上影線百分比（最高價 - 實體上緣）/ 開盤。
- `LowerShadowPercent(double open, double close, double low)`: 計算K棒下影線百分比（實體底部 - 最低價）/ 開盤。
- `RisePercent(double open, double close)`: 計算漲幅百分比（收盤與開盤的絕對差）/ 開盤。

