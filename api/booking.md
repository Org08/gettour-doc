
# Booking

訂房

## Functions

### staticSearch

主要以座標與半徑(km)搜尋, 配合預先匯入在本系統的其他靜態資料(如星級)進一步篩選.

##### 範例

```javascript
Gettour.booking.staticSearch({
    coordinates: [2.170625, 41.37446],
    distance: 0.5,
    star: { min: 3, max: 4 }
});
```

- `coordinates: [Number]` [longitude, latitude], 經度與緯度.

- `distance: Number` 距離指定地點幾公里.

- `star: Object` 

> 待擴充其他靜態條件

---
