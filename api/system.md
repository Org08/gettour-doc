
# System

系統本身的基本功能

## Functions

---

### connect

連線

其他所有功能, 都會在連線成功後才載入

##### 範例

```javascript
Gettour.connect(url)
```

- `url: String` gettour-core server 的 ip 和 port 組成的字串.

---

### login

登入

成功的登入會被儲存, 下次 connect 後會自動登入, 直到主動呼叫 logout 才清除

##### 範例

```javascript
Gettour.login({
    username: username,
    password: password
})
```

- `username: String`

- `password: String`


---

### logout

登出

##### 範例

```javascript
Gettour.logout()
```

---


---

| [回目錄](https://github.com/Org08/gettour-doc/blob/master/README.md) |
[回API](https://github.com/Org08/gettour-doc/blob/master/api/README.md) |

---
