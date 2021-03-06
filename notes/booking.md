
---

## 前提

先從各家供應商的系統, 把各飯店的`靜態資料`匯入本系統.

主要是需要`座標`, 用來讓前端可以用地圖工具搜尋.

> 儲存在本地的飯店資料, 會有對應供應商的`HotelID`. 對供應商搜尋時, 用`HotelID`當條件可以節省效能.

> 各家命名不同, 在此統稱 `HotelID`.

---

## 流程

### 靜態搜尋

前端地圖工具透過`拖曳`或`輸入地址`或`名稱搜尋`等, 取得欲搜尋的飯店`座標`及搜尋`範圍`.

> 必須控制範圍, 以及顯示飯店的總量, 以避免效能問題.

> 當範圍內飯店數量超過可顯示的總數時, 先顯示靠近中心的飯店.

> 除了座標以外, 星級和設施等靜態條件, 皆可一起在此步驟加入.

### 動態條件

例如`入住與退房日期`或`大人小孩人數`, 這類資訊會即時變動, 所以不會除存在本地系統.

`動態條件`配合`靜態搜尋`取得的`HotelID`, 發給供應商查詢即時房間.

### 供應商篩選

上述兩種查詢, 預設都是對所有供應商搜尋.

但這同樣也可以是搜尋條件, 留給前端控制.

---

## 情境說明

使用者拉好靜態條件, 也設好動態條件(對使用者來說沒什麼區別, 都是搜尋條件).

本系統後端先在內部抓出符合靜態條件的飯店.

後端根據搜尋出的飯店, 配合動態條件, 向各供應商查詢.

每個供應商查詢都獨立跑, 先收到回應的, 就先丟給前端.

前後端用 websocket(換別的也行) 溝通, 前端收到後端推來的查詢結果, 就顯示出這組供應商的房間資訊.

---

## 後續訂房步驟

在使用者選擇了某間房以後, 接下來的`訂房`或`修改`或`取消`, 就都是針對此`供應商`的此`房間`操作.

本系統會儲存關鍵資訊, 像是 `rateKey`(功能等同此訂房的 id) 或是總金額等等. 方便在本系統快速查詢或統計.

> 各家命名不同, 在此統稱 `rateKey`.

當需要做`修改`或`取消`等操作時, 就是先在本系統查詢出 `rateKey`, 並用這個來對供應商系統執行對應動作.

---
