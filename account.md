# Đăng nhập ví PayME

## Mô tả

API dùng đăng nhập tài khoản ví PayME

## Đường dẫn

`/v1/account/login`

## Phương thức

POST

## Cú pháp gọi dịch vụ đăng nhập

```javascript
const res = await broker.call(actionName, params, opts);
```

| Tham số      | Type   | Mô tả                                      |
| ------------ | ------ | ------------------------------------------ |
| `actionName` | String | Tên hành động được định nghĩa trong broker |
| `params`     | Json   | Được truyền vào context của action         |
| `opts`       | Json   | Được ghi đè vào request                    |

Available calling options:

| Name               | Type    | Mặc định | Mô tả                                                                                                                                                                                                                                                      |
| ------------------ | ------- | -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `timeout`          | Number  | null     | Thời gian chờ yêu cầu tính bằng mili giây. Nếu thời gian request bị timeout, và `fallbackResponse` chưa được định nghĩa, broker sẽ trả về lỗi `RequestTimeout`. Để tắt đi set giá trị về `0`. Nếu trường này không được định nghĩa, broker sẽ lấy mặc định |
| `retries`          | Number  | null     | Số lần thử lại của một request. Để tắt set giá trị về `0`. Nếu trường này không được định nghĩa, broker sẽ lấy mặc định                                                                                                                                    |
| `fallbackResponse` | Any     | null     | Trả về chính nó khi request thất bại                                                                                                                                                                                                                       |
| `nodeID`           | String  | null     | Trường này được định nghĩa, hành động sẽ gọi trực tiếp đến node này                                                                                                                                                                                        |
| `meta`             | Object  | {}       | Metadata của request. Là `ctx.meta` trong action handlerF                                                                                                                                                                                                  |
| `parentCtx`        | Context | null     | Parent Context instance. Use it to chain the calls.                                                                                                                                                                                                        |
| `requestID`        | String  | null     | Request ID or Correlation ID. Use it for tracing.                                                                                                                                                                                                          |

## Request

- Params mẫu

```json
{
  "phone": "0333823057",
  "password": "0b76aaa9c150e2366126567d02909f4a7e6e8eab766bade7216153f2a67aaf1b",
  "clientId": "16f152a6d9c2c670"
}
```

| Key        | Type   | Required | Mô tả                                       | Ghi chú                     |
| ---------- | ------ | -------- | ------------------------------------------- | --------------------------- |
| `phone`    | String | Yes      | Số điện thoại đăng kí ví PayME              |                             |
| `password` | String | Yes      | Mật khẩu được hash sha256 trước khi gửi lên |                             |
| `clientId` | String | Yes      | Id của thiết bị                             | Id của thiết bị là duy nhất |

- Request mẫu

```javascript
const res = await broker.call(
  "v1.account.login",
  {
    phone: "0333823057",
    password:
      "0b76aaa9c150e2366126567d02909f4a7e6e8eab766bade7216153f2a67aaf1b",
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

| Key              | Type   | Mô tả                                           |
| ---------------- | ------ | ----------------------------------------------- |
| `code`           | String | Số điện thoại đăng kí ví PayME                  |
| `message`        | String | Mật khẩu được hash sha256 trước khi gửi lên     |
| `state`          | String | Trạng thái của tài khoản khi đăng nhập thất bại |
| `stateVersion`   | String | Trạng thái phiên bản                            |
| `updateTitle`    | String | Title cập nhật ứng dụng                         |
| `updateURL`      | String | URL cập nhật ứng dụng                           |
| `accessToken`    | String | Mã truy cập                                     |
| `accessTokenKey` | String | Mã truy cập                                     |

Các trạng thái đăng nhập thất bại

| Key                        | Mô tả                             |
| -------------------------- | --------------------------------- |
| `LOGIN_REQUIRE_VERIFY_OTP` | Đăng nhập yêu cầu nhập OTP        |
| `LOGIN_FAIL_OVER_OTP`      | Nhập OTP sai nhiều lần            |
| `ACCOUNT_EXIST`            | Tài khoản đã được liên kết        |
| `LOGIN_FAIL_OVER_PASSWORD` | Đăng nhập sai thông tin nhiều lần |
| `BUSINESS_ACCOUNT`         | Tài khoản doanh nghiệp            |

- Response mẫu

```javscript
{
  "succeeded": true,
  "message": "Đăng nhập thành công!",
  "state": null,
  "stateVersion": "",
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6Mjk5NzcsImFjY291bnRJZCI6Mzk0ODYzNTQxLCJzY29wZSI6W10sImNsaWVudElkIjoiMTZmMTUyYTZkOWMyYzY3MCIsImFwcElkIjpudWxsLCJpYXQiOjE2MjE1MzMxNzN9.K7Kl3uqwcYS5TSMPA5CJVg2Axy7UkThlqM9Lpr3Asro",
  "accessTokenKey": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6Mjk5NzcsImFjY291bnRJZCI6Mzk0ODYzNTQxLCJwaG9uZSI6Ijg0MzMzODIzMDU3IiwiYXBwSWQiOm51bGwsImlhdCI6MTYyMTUzMzE3M30.D7dwWLl_jY6KssIf3UDq5RytI8pA0DnunBexsAtOBfQ",
  "updateURL": "apple.com/app/payme.vn",
  "updateTitle": "update thanh toán   "
}
```
