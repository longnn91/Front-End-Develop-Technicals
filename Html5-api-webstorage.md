### HTML5 Web Storage
---
**Reference**: How to seting Notification with localStorage
- https://www.taniarascia.com/how-to-use-local-storage-with-javascript/
- https://www.smashingmagazine.com/2010/10/local-storage-and-how-to-use-it/
- https://medium.com/@mariusc23/using-local-storage-to-detect-content-changes-on-refresh-350523a9e313
- https://www.sitepoint.com/browser-notification-api/

> **1. Local Storage**

```javascripts
// Lưu dữ liệu vào local store hiện tại
localStorage.setItem("username", "John");
// Truy cập một số dữ liệu được lưu trữ
alert( "username = " + localStorage.getItem("username"));
```

- Đoạn mã sau truy cập đối tượng Lưu trữ cục bộ của miền hiện tại và thêm mục dữ liệu vào đối tượng đó bằng cách sử dụng ```Storage.setItem()```.

```javascripts
localStorage.setItem('myCat', 'Tom');
```

- Cú pháp để đọc mục ```localStorage``` như sau:

```javascripts
var cat = localStorage.getItem('myCat');
```

- Cú pháp để loại bỏ mục ```localStorage``` như sau:

```javascripts
localStorage.removeItem('myCat');
```

- Cú pháp để loại bỏ tất cả các mục ```localStorage``` như sau:

```javascripts
// clear all items
localStorage.clear();
```
