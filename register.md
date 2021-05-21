# Đăng kí ví PayME <img class="emoji" src="https://github.githubassets.com/images/icons/emoji/memo.png" alt="memo">

## Mô tả

API dùng đăng kí tài khoản ví PayME

## Đường dẫn

`/v1/account/register`

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
  "phone": "0908663101",
  "password": "8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92",
  "fullname": "Đinh Minh Quang",
  "activeCode": "764631",
  "clientId": "16f152a6d9c2c670",
  "accountType": "PERSONAL"
}
```

| Key           | Type   | Required | Mô tả                                       | Ghi chú                     |
| ------------- | ------ | -------- | ------------------------------------------- | --------------------------- |
| `phone`       | String | Yes      | Số điện thoại đăng kí ví PayME              |                             |
| `password`    | String | Yes      | Mật khẩu được hash sha256 trước khi gửi lên | Mã hóa SHA256               |
| `fullname`    | String | Yes      | Tên đầy đủ của người sử dụng ví             |                             |
| `handShake`   | String | No       | Chuỗi handshake dùng để kết nối             |                             |
| `activeCode`  | String | Yes      | Chuỗi OTP được sinh ra khi đăng kí nhận OTP | OTP sẽ hết hạn trong 5 phút |
| `clientId`    | String | Yes      | Id của thiết bị                             | Id của thiết bị là duy nhất |
| `email`       | String | No       | Email của người dùng ví                     |                             |
| `accountType` | String | No       | Ví doanh nghiệp/cá nhân                     | Default PERSONAL            |

Các loại account

| Key        | Mô tả                  |
| ---------- | ---------------------- |
| `PERSONAL` | Tài khoản cá nhân      |
| `BUSINESS` | Tài khoản doanh nghiệp |

- Request mẫu

```javascript
const res = await broker.call(
  "v1.account.register.getOTP",
  {
    phone: "0908663101",
    password:
      "8d969eef6ecad3c29a3a629280e686cf0c3f5d5a86aff3ca12020c923adc6c92",
    fullname: "Đinh Minh Quang",
    activeCode: "764631",
    clientId: "16f152a6d9c2c670",
    accountType: "PERSONAL",
  },
  {
    timeout: 500,
    retries: 3,
    fallbackResponse: defaultRecommendation,
  }
);
```

## Response

| Key           | Type    | Mô tả                                                                                      |
| ------------- | ------- | ------------------------------------------------------------------------------------------ |
| `succeeded`   | Boolean | Trạng thái thành công hoặc thất bại của dịch vụ                                            |
| `message`     | String  | Lời nhắn                                                                                   |
| `state`       | String  | Trạng thái nhận biết để biết tài khoản này có vấn đề khi đăng nhập(nếu có(bị khoá, OTP..)) |
| `accessToken` | String  | Access Token                                                                               |

Trạng thái đăng kí thất bại

| Key                   | Mô tả                       |
| --------------------- | --------------------------- |
| `LOGIN_FAIL_OVER_OTP` | Đăng nhập sai OTP nhiều lần |
| `ACCOUNT_EXIST`       | Tài khoản đã liên kết       |

- Response mẫu

```json
{
  "state": null,
  "succeeded": true,
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6Mjk5OTEsImFjY291bnRJZCI6MTIzNzI3NjUxLCJzY29wZSI6W10sImNsaWVudElkIjoiMTZmMTUyYTZkOWMyYzY3MCIsImFwcElkIjpudWxsLCJpYXQiOjE2MjE1NzExMjd9.ERBt8UyY5siI3-VUU-omh_t6AkVnmLSLJHtgaq6wfgY",
  "message": "Khởi tạo tài khoản thành công"
}
```

<br></br>
