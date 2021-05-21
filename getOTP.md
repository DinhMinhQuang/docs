# Nhận OTP đăng kí ví PayME <img class="emoji" src="https://github.githubassets.com/images/icons/emoji/memo.png" alt="memo">

## Mô tả

API dùng để nhận OTP để đăng kí tài khoản ví PayME

## Đường dẫn

`/v1/account/register/getOTP`

## Phương thức

`POST`

## Cú pháp gọi dịch vụ

```javascript
const res = await broker.call(actionName, params, opts);
```

| Tham số      | Type   | Mô tả                                      |
| ------------ | ------ | ------------------------------------------ |
| `actionName` | String | Tên hành động được định nghĩa trong broker |
| `params`     | Json   | Được truyền vào context của action         |
| `opts`       | Json   | Được ghi đè vào request                    |

- Các tùy chọn có sẵn

| Name               | Type    | Mặc định | Mô tả                                                                                                                                                                                                                                                      |
| ------------------ | ------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `timeout`          | Number  | null     | Thời gian chờ yêu cầu tính bằng mili giây. Nếu thời gian request bị timeout, và `fallbackResponse` chưa được định nghĩa, broker sẽ trả về lỗi `RequestTimeout`. Để tắt đi set giá trị về `0`. Nếu trường này không được định nghĩa, broker sẽ lấy mặc định |
| `retries`          | Number  | null     | Số lần thử lại của một request. Để tắt set giá trị về `0`. Nếu trường này không được định nghĩa, broker sẽ lấy mặc định                                                                                                                                    |
| `fallbackResponse` | Any     | null     | Trả về chính nó khi request thất bại                                                                                                                                                                                                                       |
| `nodeID`           | String  | null     | Khi `nodeId` được định nghĩa, `broker.call()` sẽ gọi trực tiếp đến node này                                                                                                                                                                                |
| `meta`             | Object  | { }      | Metadata của request. Là `ctx.meta` trong action handler                                                                                                                                                                                                   |
| `parentCtx`        | Context | null     | Parent `Context` instance. Use it to chain the calls.                                                                                                                                                                                                      |
| `requestID`        | String  | null     | `requestID` or `correlationId`. Dùng để `tracing`                                                                                                                                                                                                          |

## Request

- Params mẫu

```json
{
  "phone": "0333803751",
  "clientId": "16f152a6d9c2c670"
}
```

| Key        | Type   | Required | Mô tả                                    | Ghi chú                     |
| ---------- | ------ | -------- | ---------------------------------------- | --------------------------- |
| `phone`    | String | Yes      | Số điện thoại đăng kí ví PayME, nhận OTP |                             |
| `clientId` | String | Yes      | Id của thiết bị                          | Id của thiết bị là duy nhất |

- Request mẫu

```javascript
const res = await broker.call(
  "v1.account.register.getOTP",
  {
    phone: "0333803751",
    clientId: "16f152a6d9c2c670",
  },
  {
    timeout: 500,
    retries: 3,
    fallbackResponse: defaultRecommendation,
  }
);
```

## Response

| Key         | Type    | Mô tả                                           |
| ----------- | ------- | ----------------------------------------------- |
| `succeeded` | Boolean | Trạng thái thành công hoặc thất bại của dịch vụ |
| `message`   | String  | Lời nhắn trạng thái của dịch vụ                 |
| `timeDelay` | Float   | Số giây đợi gửi lại OTP                         |
| `state`     | String  | Mô tả trạng thái dịch vụ                        |

OTP được gửi về số điện thoại sau khi request thành công

Trạng thái thất bại

| Key             | Mô tả                               |
| --------------- | ----------------------------------- |
| `ACCOUNT_EXIST` | Tài khoản đã tồn tại trong hệ thống |

- Response mẫu

```JSON
  {
    "succeeded": true,
    "message": "Gửi OTP thành công",
    "timeDelay": "-2",
    "state":null
  }
```

<br></br>
