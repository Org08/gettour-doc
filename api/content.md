
# Content

靜態資料同步與各家資料對應.

部分功能雖然有開放前端 API, 但平常只在自動同步系統資料時使用, 前端僅供開發測試.

## Functions

---

### syncHotel

同步飯店靜態資料.

會依序從已整合的廠商, 分別撈回資料, 並根據座標初步自動 mapping. 

很有機會需要人工調整. 人工調整的部分另有介面可用.

##### 範例

```javascript
Gettour.content().syncHotel();
```

---

### syncAccommodationType

同步 Accommodation 資料.

種類不多, 有的廠商甚至沒提供取的這個列表的 API, 而是在用到這欄位的說明裡寫死.

但仍然需要 mapping, 只是沒有複雜到需要額外介面處理.

##### 範例

```javascript
Gettour.content().syncAccommodationType();
```

---

### syncBoard

同步 Board 資料.

需要建立內部分類, 並把各家的定義 mapping.

##### 範例

```javascript
Gettour.content().syncBoard();
```

---

### syncCurrency

同步 Currency 資料.

有些廠商沒有提供支援的 Currency 列表, 只會在收到不支援的類型後回應錯誤.

因此在本地會對這類廠商, 手動建立支援列表.

##### 範例

```javascript
Gettour.content().syncCurrency();
```

---

### syncDestination

同步 Destination 資料.

雖然現在在地理位置方面的搜尋, 是像 google map 那樣直接入名稱或地址甚至隨便的字串來搜尋, 暫時用不到 Destination. 但這仍很有機會用來分類, 所以還是會載入.

##### 範例

```javascript
Gettour.content().syncDestination();
```

---

### syncFacility

同步 Facility 資料.

這項也需要 mapping 才能讓前端拿來當搜尋條件. 也需要決定前端要顯示的項目.

目前發現 WebBeds 沒有像 HotelBeds 那樣詳細到幾百項的 Facility, 倒是有只有 12 項的 Feature.

Feature 看起來基本上就是 Facility, 只是項目精簡很多, 或許可以參考他當前端顯示用的.

(WebBeds Features: Air Conditioning, Balcony, Bar, Elevator, Pool, Childrens Pool, Restaurant, Safe, Sea View, Telephone, TV, Wireless internet)

(所以所有需要 mapping 的項目, 都會提供像 Hotel 那樣的工具來設定. 這同時也會決定搜尋時會出現的選項.)

##### 範例

```javascript
Gettour.content().syncFacility();
```

---

### syncLanguage

同步 Language 資料.

各家語言支援不一, 當選了不支援的語言時, 或是來源資料缺了該語言, 預定會預設顯示英文.

##### 範例

```javascript
Gettour.content().syncLanguage();
```

---

### syncRoomType

同步 RoomType 資料.

需要建立內部分類, 並把各家的定義 mapping.

##### 範例

```javascript
Gettour.content().syncRoomType();
```

---


---

| [回目錄](https://github.com/Org08/gettour-doc/blob/master/README.md) |
[回API](https://github.com/Org08/gettour-doc/blob/master/api/README.md) |

---

