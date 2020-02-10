
# 訂房系統

底下會列出所有功能, 而實際使用時, 會根據權限開放不同功能.

## 登入

- 基本登入功能.

- 錯誤訊息提示.

- 保持登入狀態.

## 主功能頁

- 開啟個子功能的主選單.

- 視需要可以開啟顯示數量用的數字泡泡, 例如新訂單的提示.

## 訂房

這是後來設計的, 以地圖範圍搜尋優先, 接著才根據這些飯店撈符合條件的即時空房. 目的是為了提升效率.

由於舊版的也還沒廢除, 所以另外拉出來一個章節. 未來會視情況取代或並存.

### 地圖

- 以選擇的位置為圓心, 標示出所設定的範圍.

- 根據[篩選面板](https://github.com/Org08/gettour-doc/blob/master/front/booking.md#%E7%AF%A9%E9%81%B8%E9%9D%A2%E6%9D%BF), 在範圍內顯示出飯店.

- 可拖曳外圈來調整範圍. 調整完會刷新符合條件的飯店.

- 可拖曳圓心來調整中心位置. 調整完會刷新符合條件的飯店.

- 點選飯店標示, 會顯示出簡略的飯店資訊. 並同時選取在飯店列表裡的該飯店. 

- 當飯店列表裡的飯店被點選, 會同時選取地圖上的飯店標示並移動到畫面裡, 並在飯店標示上顯示出簡略的飯店資訊.

### 篩選面板

- 分為搜尋靜態資料的部分, 和查詢即時空房資訊的部分. 這只對系統有差別, 對使用者則沒有影響.

- 位置欄位可以輸入地址或關鍵字, 所查詢到的地點會即時反應在[地圖](https://github.com/Org08/gettour-doc/blob/master/front/booking.md#%E5%9C%B0%E5%9C%96)上. 反之若從[地圖](https://github.com/Org08/gettour-doc/blob/master/front/booking.md#%E5%9C%B0%E5%9C%96)上移動中心點, 新的地址也會顯示在位置欄位.

- 範圍欄位也會即時影響地圖上的範圍圓圈. 反之若從[地圖](https://github.com/Org08/gettour-doc/blob/master/front/booking.md#%E5%9C%B0%E5%9C%96)上調整範圍, 新的範圍也會顯示在範圍欄位.

- 星級可以用大於小於和等於來更進一步控制條件.

- 可以設定不同的排序, 改變飯店列表的顯示. 例如依據距離或是價錢, 高到低或低到高.

### 飯店列表

- 根據[篩選面板](https://github.com/Org08/gettour-doc/blob/master/front/booking.md#%E7%AF%A9%E9%81%B8%E9%9D%A2%E6%9D%BF)與[地圖](https://github.com/Org08/gettour-doc/blob/master/front/booking.md#%E5%9C%B0%E5%9C%96)的設定, 顯示出符合條件的飯店.

- 點選飯店會同時在[地圖](https://github.com/Org08/gettour-doc/blob/master/front/booking.md#%E5%9C%B0%E5%9C%96)上選取該飯店的標示, 並顯示出簡易的飯店資訊.

- 當在[地圖](https://github.com/Org08/gettour-doc/blob/master/front/booking.md#%E5%9C%B0%E5%9C%96)上點選飯店標示, 會同時選取在飯店列表裡的該飯店. 

- 可以開啟此飯店的房間列表.

### 房間列表

- 列出符合[篩選面板](https://github.com/Org08/gettour-doc/blob/master/front/booking.md#%E7%AF%A9%E9%81%B8%E9%9D%A2%E6%9D%BF)的特定飯店房間.

- 可以開啟房間詳細資料, 並設定訂房資料和送出訂房.


## 訂房紀錄

### 篩選面板

- 篩選要顯示的紀錄

### 訂單列表

- 根據[篩選面板](https://github.com/Org08/gettour-doc/blob/master/front/booking.md#%E7%AF%A9%E9%81%B8%E9%9D%A2%E6%9D%BF)顯示出符合條件的訂單.

## 帳務

## 供應商

## 旅行社

## 帳號

## 系統


---

| [回目錄](https://github.com/Org08/gettour-doc/blob/master/README.md) |
[回前端介面](https://github.com/Org08/gettour-doc/blob/master/README.md) |

---
