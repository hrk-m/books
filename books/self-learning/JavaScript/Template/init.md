# JavaScript 便利メソッド

## 0 埋め のサンプル

```js
const zeroPadding = ((num, length) = ("0000000000" + num).slice(-length));
const num = zeroPadding(346, 8);
alert(num); // 00000346が表示されます。
```
