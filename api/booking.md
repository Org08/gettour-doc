
# Booking

訂房相關功能.

由於各家 API 在部分功能差異很大, 為了降低前端開發與第三方整合難度, 預定用前端元件轉換. 不管是一般的搜尋條件, 或是那種規定修改資料要把整包回傳的, 都由元件內部處理, 開發者只需要指定本系統對應的 ID, 以及要動的資料即可.

不過由於整合工作尚未全部完成, 所以以下範例會有很多是針對特定供應商的寫法.

## Functions

---

### staticSearch

搜尋靜態資料.

用前端工具取得 `座標`, 配合 `星級` `設施` 等靜態條件搜尋. 目標是取得本系統內符合條件`飯店`, 對應每家供應商的 `HotelID`. 這些 `HotelID` 是用來向各家查詢即時資料時, 限制搜尋範圍用的.

這個搜尋所取得的資料可以用來顯示飯店的基本資訊.

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

搜尋即時資料.

用來自 [staticSearch](https://github.com/Org08/gettour-doc/blob/master/api/booking.md#staticsearch) 取得的 `HotelID`, 配合 `入住退房日期` `大人小孩人數` 等訂房資訊, 實際向各家供應商查詢即時空房.

也就是用地圖工具劃出範圍以後, 用範圍內的飯店做即時空房查詢.

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

### prebook

有些廠商(如WebBeds)強制要在 book 前先發出 prebook, 把從 prebook 取得的資料更新到前端介面, 讓使用者再次確認(有可能價格跟一開始查的不同了).

有些廠商(如HotelBeds)沒有強制, 但是會根據不同的房來決定需不需要這個前置的確認.

因此在我們的系統一律必須先送 prebook.

當該廠商或房間需要這麼做, 就送出查詢. 反之則直接回應給前端.

對前端來說, 兩者都一樣是跳出再次顯示訂房資訊的確認視窗.

##### 範例

```javascript
Gettour.booking(supplier).prebook({
    rateKey: "20191201|20191204|W|102|60819|DBL.DX|CG-TODOS1|BB||1~1~0||N@03~~23e2d8~945529463~N~548A85CCE4E84A0157395802663200AATW0000001000000000522f289"
});
```

- `supplier: String` 供應商名稱. 對於不同供應商, 會有不同資訊需要傳送.

- `rateKey: String` 能夠代表此訂房的 key. 不同供應商會有不同定義.

> 目前的範例為 HotelBeds

> 預定要把這段包在前端 API 元件裡, 讓第三方開發者不需要處理各家不同的情況.

---

### book

執行過 prebook 步驟後, 用原資料(或是同意更新後的資料)送出.

##### 範例

```javascript
Gettour.booking(supplier).book({
    holder: {
        name: "IntegrationTestFirstName",
        surname: "IntegrationTestLastName"
    },
    rooms: [{
        rateKey: "20191201|20191204|W|102|60819|DBL.DX|CG-TODOS1|BB||1~1~0||N@03~~23e2d8~945529463~N~548A85CCE4E84A0157395802663200AATW0000001000000000522f289",
        paxes: [{
            roomId: "1",
            type: "AD",
            name: "First Adult Name",
            surname: "Surname"
        }, {
            roomId: "1",
            type: "CH",
            name: "First Child Name",
            surname: "Surname"
        }]
    }]
});
```

- `supplier: String` 供應商名稱. 對於不同供應商, 會有不同資訊需要傳送.

- `holder: Object` 訂房者.
    - `name: String` 訂房者名.
    - `surname: String` 訂房者姓.

- `rooms: [Object]` 預定的房間資料.
    - `rateKey: String` 能夠代表此訂房的 key. 不同供應商會有不同定義.
    - `paxes: [Object]` 房客資料.
        - `roomId: String` 房間 ID. 當同一房有多個房客時, 是用此值來分辨誰在同一房.
        - `type: String` AD: 成人. CH: 兒童.
        - `name: String` 房客名.
        - `surname: String` 房客姓.

> 目前的範例為 HotelBeds

> 預定要把這段包在前端 API 元件裡, 讓第三方開發者不需要處理各家不同的情況.

---

### list

列出訂房紀錄.

這裡取得的是本地資料庫所存的紀錄.

##### 範例

```javascript
Gettour.booking().list({
    supplier: "HotelBeds",
    start: "2019-12-01",
    end: "2019-12-10",
    from: 1,
    to: 20,
});
```

- `supplier: String` 供應商名稱.

- `start: String` 入住日期.

- `end: String` 退房日期.

- `from: Number` 從第幾筆資料開始回傳.

- `to: Number` 回傳到第幾筆資料.

---

### detail

從列出的訂房紀錄裡, 進一步調閱細節資料.

這會向該紀錄所屬的供應商取得即時資料.

##### 範例

```javascript
Gettour.booking(supplier).detail({
    id: "102-10544416",
});
```

- `supplier: String` 供應商名稱. 對於不同供應商, 會有不同資訊需要傳送.

- `id: String` 訂房 ID.

> 目前的範例為 HotelBeds

> 預定要把這段包在前端 API 元件裡, 讓第三方開發者不需要處理各家不同的情況.

---

### update

修改訂房.

##### 範例

```javascript
Gettour.booking(supplier).update({
    id: "102-10544416",
    booking: {
        "reference": "102-10544416",
        "clientReference": "INTEGRATIONAGENCY-XDDD",
        "creationDate": "2019-10-28",
        "status": "CONFIRMED",
        "modificationPolicies": {
            "cancellation": true,
            "modification": false
        },
        "creationUser": "z9p5xex7p8jfvzpknkukpw6x",
        "holder": {
            "name": "INTEGRATIONTESTFIRSTNAME",
            "surname": "INTEGRATIONTESTLASTNAME"
        },
        "hotel": {
            "checkOut": "2019-10-31",
            "checkIn": "2019-10-30",
            "code": 69,
            "name": "TRYP Barcelona Apolo Hotel",
            "categoryCode": "4EST",
            "categoryName": "4 STARS",
            "destinationCode": "BCN",
            "destinationName": "Barcelona",
            "zoneCode": 44,
            "zoneName": "Parallel",
            "latitude": "41.37446",
            "longitude": "2.170625",
            "rooms": [
                {
                    "status": "CONFIRMED",
                    "id": 1,
                    "code": "SGL.ST",
                    "name": "SINGLE STANDARD",
                    "supplierReference": "TS1572266134059",
                    "paxes": [
                        {
                            "roomId": 1,
                            "type": "AD",
                            "name": "First Adult Name",
                            "surname": "Surname"
                        }
                    ],
                    "rates": [
                        {
                            "rateClass": "NOR",
                            "net": "132.20",
                            "rateComments": "Car park YES (with additional debit notes) 22.00 EUR Per unit/night. Key Collection 15:00 - . Check-in hour 15:00 - . Deposit on arrival. Identification card at arrival.",
                            "paymentType": "AT_WEB",
                            "packaging": false,
                            "boardCode": "RO",
                            "boardName": "ROOM ONLY",
                            "cancellationPolicies": [
                                {
                                    "amount": "55.48",
                                    "from": "2019-10-22T23:59:00+02:00"
                                },
                                {
                                    "amount": "132.20",
                                    "from": "2019-10-27T23:59:00+01:00"
                                }
                            ],
                            "rooms": 1,
                            "adults": 1,
                            "children": 0
                        }
                    ]
                }
            ],
            "totalNet": "132.20",
            "currency": "USD",
            "supplier": {
                "name": "MIKI Travel Limited",
                "vatNumber": "ESB38877676"
            }
        },
        "remark": "Booking remarks are to be written here.",
        "invoiceCompany": {
            "code": "SG1",
            "company": "HOTELBEDS PTE. LTD",
            "registrationNumber": "M2-0084578-1"
        },
        "totalNet": 132.2,
        "pendingAmount": 132.2,
        "currency": "USD"
    }
});
```

- `supplier: String` 供應商名稱. 對於不同供應商, 會有不同資訊需要傳送.

- `id: String` 訂房 ID.

> 目前的範例為 HotelBeds

> 暫時省略詳細資料說明, 因為實在太雜了. 這裡怎樣都應該包在元件內部做掉.

> 預定要把這段包在前端 API 元件裡, 讓第三方開發者不需要處理各家不同的情況.

---

### cancel

取消訂房.

##### 範例

```javascript
Gettour.booking(supplier).cancel({
    id: "102-10544416",
    cancellationFlag: "SIMULATION",  // 這不是每家都有的參數
});
```

- `supplier: String` 供應商名稱. 對於不同供應商, 會有不同資訊需要傳送.

- `id: String` 訂房 ID.

> 目前的範例為 HotelBeds

> 預定要把這段包在前端 API 元件裡, 讓第三方開發者不需要處理各家不同的情況.

---


---

---

[回目錄](https://github.com/Org08/gettour-doc/blob/master/README.md)


