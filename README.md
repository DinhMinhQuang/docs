# Trang Chủ :smiley:

## Tổng quan

Tài liệu hướng dẫn gọi các api của cụm Account Service

- Danh sách API

| API path                      | Mô tả API                                     |
| ----------------------------- | --------------------------------------------- |
| `/v1/account/login`           | Api đăng nhập tài khoản ví PayME              |
| `/v1/account/register`        | Api đăng kí tài khoản ví PayME                |
| `/v1/account/register/getOTP` | Api gửi OTP vào số tài khoản đăng kí ví PayME |

- Cú pháp gọi dịch vụ :heart:

```javascript
const res = await broker.call(actionName, params, opts);
```

?> `actionName` là một chuỗi được phân tách với nhau bằng dấu chấm, phần đầu là tên dịch vụ, trong khi phần thứ 2 đại diện cho tên dịch vụ. Vì vậy, nếu bạn có dịch vụ `account` với hành động `login` có thể gọi nó là `account.login`. [^1]

?> `params` là một đối tượng được truyền cho `action` như một phần của `Context`. Dịch vụ có thể truy cập nó qua `ctx.params`. Nó là tùy chọn. Nếu bạn không xác định, nó sẽ là `{}`. :smile:

?> `opts` là một đối tượng để thiết lập / ghi đè một số tham số yêu cầu. Ví dụ: `timeout`, `retryCount`. `otps` là một tùy chọn.

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

<br></br>