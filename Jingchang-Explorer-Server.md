<!-- markdownlint-disable MD024 -->
<!-- markdownlint-disable MD033 -->

# Jingchang Explorer Server

## APIs

### 1. 查询交易列表

#### 1.1 查询最新的6个交易列表

* route

   `/trans/new/:uuid`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id

#### 1.2 查询所有交易列表

* route

   `/trans/all/:uuid?p=&s=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   p|number|是|-|-|页数，从0开始
   s|number|是|10/20/50/100|20|每页条数

### 2. 查询区块信息列表

#### 2.1 查询最新的6个区块

* route

   `/block/new/:uuid`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id

#### 2.2 查询所有区块信息列表

* route

   `/block/all/:uuid?p=&s=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   p|number|是|-|-|页数，从0开始
   s|number|是|10/20/50/100|20|每页条数

### 3. 根据哈希查询交易详细

* route

   `/hash/detail/:uuid?h=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   h|string|是|-|-|hash

### 4. 根据区块HASH查询其包含的交易列表

* route

   `/hash/trans/:uuid?p=&s=&n=&h=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   h|string|是|-|-|交易hash
   p|number|是|-|-|页数，从0开始
   s|number|是|10/20/50/100|20|每页条数
   n|number|是|-|-|区块中一共有多少个交易记录

### 5. 指定钱包查询

#### 5.1 指定钱包的余额查询（包括所有Token的余额、所有Token的冻结数量）

* route

   `/wallet/balance/:uuid?w=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   w|string|是|-|-|钱包地址

### 5.2 指定钱包的当前委托单查询

* route

   `/wallet/offer/:uuid?p=&s=&c=&bs=&w=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   p|number|是|-|-|页数，从0开始
   s|number|否|10/20/50/100|20|每页条数
   w|string|是|-|-|钱包地址
   c|string|否|-|-|交易对（可以不传值，不传值表示查询全部类型交易对的委托单。形如：SWTC-CNY或swtc-cny，必须是交易对本来的顺序base-counter的形式，比如这里不能是CNY-SWTC，否则买卖关系可能就乱了，另外交易对可以只指定base或counter，如swtc-或-cny，所有的交易对请参见附录）
   bs|number|否|0:买或卖<br>1:买<br>2:卖|0|委托性质,如果传值必须与c参数一起使用

#### 5.3 指定钱包的历史交易查询

* route

   `/wallet/trans/:uuid?p=&s=&b=&e=&t=&bs=&c=&w=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   p|number|是|-|-|页数，从0开始
   s|number|是|10/20/50/100|20|每页条数
   b|string|否|-|-|开始日期，形如YYYY-MM-DD
   e|string|否|-|-|结束日期，形如YYYY-MM-DD
   t|string|否|OfferCreate/OfferAffect/OfferCancel/Send/Receive|-|交易类型（多个类型以逗号分隔，可以不传值，不传值表示查询所有类型）
   c|string|否|-|-|交易对或币种（可以不传值，不传值表示币种不作为查询条件。在t=OfferCreate或OfferAffect或OfferCancel时，传值必须形如：SWTC-CNY或swtc-cny，必须是交易对本来的顺序base-counter的形式，比如这里不能是CNY-SWTC，否则买卖关系可能就乱了，另外交易对可以只指定base或counter，如swtc-或-cny，所有的交易对请参见附录；在t=Send或Receive时，传值必须长度<8，如JJCC）
   bs|number|否|0:买或卖<br>1:买<br>2:卖|-|只有在t=OfferCreate或OfferAffect或OfferCancel时有效果
   w|string|是|-|-|钱包地址

#### 5.4 指定钱包收益分析

* route

   `/wallet/profit/:uuid?t=&v=&w=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   t|number|是|1:日<br>2:周<br>3:月<br>4:年|-|类型
   w|string|是|-|-|钱包地址

### 6. 持仓排行

#### 6.1 获取所有tokens列表

* route

   `/sum/all/:uuid?t=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   t|string|否|-|-|token名称

### 7. 获取某种token的100排名

* route

   `/sum/list/:uuid?t=&p=&s=&b=&e=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   t|string|否|-|-|token名称（SWT无需发行方，值为SWTC_，其他token需要带发行方，币种大写, 如c=CNY_jGa9J9TkqtBcUoHe2zqhVFFbgUVED6o9or）
   p|number|是|-|-|页数，从0开始
   s|number|否|10/20/50/100|20|每页条数
   b|string|否|-|-|开始日期，形如YYYY-MM-DD
   e|string|否|-|-|结束日期，形如YYYY-MM-DD

### 8. 查看自己排名

* route

   `/sum/self/:uuid?t=&w=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   t|string|是|-|-|token名称（SWT无需发行方，值为SWTC_，其他token需要带发行方，币种大写, 如c=CNY_jGa9J9TkqtBcUoHe2zqhVFFbgUVED6o9or）
   w|string|是|-|-|钱包地址

### 9. 查看银关地址发行过tokens

* route

   `/wallet/fingate_tokenlist/:uuid?w=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   w|string|是|-|-|银关地址

### 10. 查询某个token在某个时间段内的转账交易hash信息

* route

   `/hash/payment_trans/:uuid?p=&s=&b=&e=&t=&c=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   p|number|是|-|-|页数，从0开始
   s|number|否|10/20/50/100|20|每页条数
   b|string|否|-|-|开始日期，形如YYYY-MM-DD
   e|string|否|-|-|结束日期，形如YYYY-MM-DD
   t|string|是|Payment|-|交易类型
   c|string|是|-|-|token名称

### 11. 查询某个钱包每天/月/年的支付或收到某个token的笔数和数量

* route

   `/sum/payment_summary/:uuid?w=&b=&dt=&t=&c=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   w|string|是|-|-|钱包地址
   dt|number|是|2: 日<br>3:月<br>4:年|-|日期类型
   b|string|是|-|-|具体某一天/月/年的日期，若dt=2，则必须形如YYYY-MM-DD；若dt=3，则必须形如YYYY-MM；若dt=4，则必须形如YYYY
   e|string|否|-|-|格式要求同b参数。若指定e的值，则累加统计b～e时间段范围内相同token的值，另外e的值必须大于b的值。对于dt=2或3时，b和e之间天数之差不能超过一年的时间；dt=4时，b和e之间的间隔没有限制
   t|string|否|Send/Receive|-|交易类型
   c|string|否|-|-|token名称（SWT无需发行方，值为SWTC_，其他token需要带发行方，币种大写, 如c=CNY_jGa9J9TkqtBcUoHe2zqhVFFbgUVED6o9or）

### 12. 查询收费平台对应token的收费详情接口

* route

   `/wallet/fee_config/:uuid?p=&w=&k=&s=&t=`

* method

   `get`

* 请求参数说明

   参数|类型|必填|可选值 |默认值|描述
   --|:--:|:--:|:--:|:--:|:--
   uuid|string|是|-|-|唯一id
   p|number|是|-|-|页数，从0开始
   s|number|否|10/20/50/100|20|每页条数
   w|string|是|-|-|平台地址
   k|number|否|1:gas费设置<br>2:手续费设置|2|收费类型
   t|string|否|-|-|token名称（SWT无需发行方，值为SWTC，其他token需要带发行方，币种大写, 如t=CNY_jGa9J9TkqtBcUoHe2zqhVFFbgUVED6o9or）

## 附录

* 交易对说明:

```json
{
    "BASE_COUNTER": {
        "CNY": [
            { "base": "SWTC", "counter": "CNY" },
            { "base": "JJCC", "counter": "CNY" },
            { "base": "JMOAC", "counter": "CNY" },
            { "base": "JETH", "counter": "CNY" },
            { "base": "JSTM", "counter": "CNY" },
            { "base": "VCC", "counter": "CNY" },
            { "base": "JCALL", "counter": "CNY" },
            { "base": "JSLASH", "counter": "CNY" },
            { "base": "CSP", "counter": "CNY" }
        ],
        "JETH": [
            { "base": "SWTC", "counter": "JETH" },
            { "base": "JMOAC", "counter": "JETH" }
        ],
        "SWTC": [
            { "base": "JJCC", "counter": "SWTC" },
            { "base": "JMOAC", "counter": "SWTC" },
            { "base": "JBIZ", "counter": "SWTC" },
            { "base": "JSLASH", "counter": "SWTC" },
            { "base": "JDABT", "counter": "SWTC" },
            { "base": "HJT", "counter": "SWTC" },
            { "base": "JSTM", "counter": "SWTC" },
            { "base": "JSNRC", "counter": "SWTC" },
            { "base": "MYT", "counter": "SWTC" },
            { "base": "JCALL", "counter": "SWTC" },
            { "base": "JEKT", "counter": "SWTC" },
            { "base": "BIC", "counter": "SWTC" },
            { "base": "YUT", "counter": "SWTC" },
            { "base": "VCC", "counter": "SWTC" },
            { "base": "JCKM", "counter": "SWTC" }
        ]
    }
}
```