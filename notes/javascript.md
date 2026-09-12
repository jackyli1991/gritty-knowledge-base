
## Intl

一个国际化命名空间，提供一系列构造函数和方法用于实现日期、时间、数字、货币、列表等格式的本地化，以及进行语言敏感的字符串比较。

#### 基本模式

```javascript
new Intl.XXX('locale', options).format(data) // locale用于指定语言和地区，例如zh-CN、en-US
```

#### 金额格式化

```javascript
const formatterMoney = new Intl.NumberFormat('zh-CN', {
  style: 'currency', // 格式风格: decimal-纯数字、currency-货币、percent-百分比
  currency: 'CNY', // ISO 货币代码，当 style 设为货币时必填
  currencDisplay: 'long',
  minimumFractionDigits: 2, // 小数最少保留几位（不足补 0）
  maximumFractionDigits: 2, // 小数最多保留几位（多余四舍五入）
  useGrouping: true, // 是否显示千分位分隔符
  notation: 'compact' // 紧凑模式
});
```
