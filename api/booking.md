
# Booking

訂房

## Functions

### staticSearch

用前端工具取得 `座標`, 配合 `星級` `設施` 等靜態條件搜尋.

目標是取得本系統內符合條件`飯店`, 對應每家供應商的 `HotelID`.

這些 `HotelID` 是用來向各家查詢即時資料時, 限制搜尋範圍用的.

##### 範例

```javascript
Gettour.booking().staticSearch({
    coordinates: [2.170625, 41.37446],
    distance: 0.5,
    star: { min: 3, max: 4 }
});
```

- `coordinates: [Number]` [longitude, latitude], 經度與緯度.

- `distance: Number` 距離指定地點幾公里.

- `star: Object` 
    - `min: Number` 最小星級.
    - `max: Number` 最大星級.

> 待擴充其他靜態條件

---

### search

用來自 [staticSearch](https://github.com/Org08/gettour-doc/blob/master/api/booking.md#staticsearch) 取得的 `HotelID`, 配合 `入住退房日期` `大人小孩人數` 等訂房資訊, 實際向各家供應商查詢即時空房.

##### 範例

```javascript
Gettour.booking(supplier).search({
    stay: { checkIn: "2010-03-01", checkOut: "2020-03-10", },
    occupancies: [{ rooms: 1, adults: 1, children: 0, }],
    hotels: [69, 57, 395063, 388537, 229135, 49396],
    from: 1,
    to: 10
});
```

- `supplier: String` 供應商名稱. 可以搜尋特定供應商.

- `stay: Object` 停留時間資料.
    - `checkIn: String` 入住日期.
    - `checkOut: String` 退房日期.

- `occupancies: [Object]` 房客資料.
    - `room: Number` 房間編號. 部分廠商需要前端自己用編號區分.
    - `adults: Number` 成人人數.
    - `children: Number` 兒童人數.

- `hotels: [String]` 來自 [staticSearch](https://github.com/Org08/gettour-doc/blob/master/api/booking.md#staticsearch) 的 `HotelID`, 限制只對各廠商搜尋這些飯店.

- `from: Number` 從第幾筆資料開始回傳.

- `to: Number` 回傳到第幾筆資料.


---
