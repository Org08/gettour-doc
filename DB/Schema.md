
# Hotel

## HotelSchema

```javascript
{
    sup_id: { type: IDSchema },
    name: { type: NameSchema },
    address: { type: AddressSchema },
    location: { type: GeoSchema },

    status: { type: Number, default: 1 },
    updated: { type: Date, default: Date.now }
}
```

底下是子項目的細節

原則上子項目裡儲存著針對不同供應商的同義欄位

### IDSchema

飯店在供應商系統裡的 ID

```javascript
{
    hotelbeds: { type: String, index: true },
    webbeds: { type: String, index: true },
}
```

### NameSchema

飯店在供應商系統裡的名稱

```javascript
{
    hotelbeds: { type: String, index: true },
    webbeds: { type: String, index: true },
}
```

### AddressSchema

飯店在供應商系統裡的地址

```javascript
{
    hotelbeds: { type: String, index: true },
    webbeds: { type: String, index: true },
}
```

### GeoSchema

飯店在供應商系統裡的座標

此架構是為了在 mongodb 裡用座標和距離做為搜尋條件

```javascript
{
    type: {
        type: String,
        default: "Point"
    },
    coordinates: {
        type: [Number],
        default: [0, 0]  // lng, lat
    }
}
```

此外, GeoSchema 需要用以下方式設定 index

```javascript
HotelSchema.index({ location: "2dsphere" });
```







