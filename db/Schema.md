
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

---

# Booking

## BookingSchema

```javascript
{
    supplier: { type: String, index: true, trim: true, required: [true, "supplier"] },  // 供應商名稱
    id: { type: String, index: true, trim: true, required: [true, "no id"] },           // 在各家供應商辨識此 booking 的 id, 例如 HotelBeds 的 "reference"

    holder: { type: HolderSchema },
    checkIn: { type: Date, index: true },
    checkOut: { type: Date, index: true },
    hotelName: { type: String, index: true, trim: true },

    pendingAmount: { type: Number },
    totalNet: { type: Number },
    remark: { type: String, default: "" },

    agentID: { type: String, index: true, trim: true },                                 // 本系統裡的 agent

    status: { type: Number, default: 0 },                                               // 0: CANCELLED, 1: CONFIRMED
    updated: { type: Date, default: Date.now }
}
```

底下是子項目的細節

### HolderSchema

holder 姓名

```javascript
{
    name: { type: String, index: true },
    surname: { type: String, index: true },
}
```

---

# User

## UserSchema

```javascript
{
    username: { type: String, index: true, trim: true, unique: true, required: [true, "no username"] },
    nickname: { type: String, index: true, trim: true, default: "----" },

    password: { type: String, trim: true }, // after bcrypt

    group: { type: String, default: "client" },                       // client, staff, admin
    status: { type: Number, default: 0 },                             // -1:停用, 0:未啟用, 1:啟用
    updated: { type: Date, default: Date.now }
}
```

---

---

| [回目錄](https://github.com/Org08/gettour-doc/blob/master/README.md) |
[回DB](https://github.com/Org08/gettour-doc/blob/master/db/README.md) |

---

