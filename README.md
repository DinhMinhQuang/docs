# Danh sách API

/v1/account/login

## Đặc tả

- Mô tả

API dùng đăng nhập tài khoản ví

- API Path

/v1/account/login

- Method

POST

- Cú pháp gọi dịch vụ đăng nhập

```javascript
const res = await broker.call(actionName, params, opts);
```

| Tham số    | Mô tả                                               |
| ---------- | --------------------------------------------------- |
| actionName | Tên hành động được định nghĩa trong broker          |
| params     | Được truyền vào context của action kiểu Json Object |
| opts       | Được ghi đè vào request kiểu Json Object            |

- Request mẫu:

```json
{
  "phone": "0333823057",
  "password": "0b76aaa9c150e2366126567d02909f4a7e6e8eab766bade7216153f2a67aaf1b",
  "clientId": "16f152a6d9c2c670"
}
```

| Key      | Type   | Required | Mô tả                                       | Ghi chú                     |
| -------- | ------ | -------- | ------------------------------------------- | --------------------------- |
| phone    | String | Yes      | Số điện thoại đăng kí ví PayME              |                             |
| password | String | Yes      | Mật khẩu được hash sha256 trước khi gửi lên |                             |
| clientId | String | Yes      | Id của thiết bị                             | Id của thiết bị là duy nhất |

- Response

| Key      | Type   | Mô tả                                       |
| -------- | ------ | ------------------------------------------- |
| code    | String | Số điện thoại đăng kí ví PayME              |
| message | String | Mật khẩu được hash sha256 trước khi gửi lên |
| clientId | String | Id của thiết bị                             |

## Writing content

After the `init` is complete, you can see the file list in the `./docs` subdirectory.

- `index.html` as the entry file
- `README.md` as the home page
- `.nojekyll` prevents GitHub Pages from ignoring files that begin with an underscore

You can easily update the documentation in `./docs/README.md`, of course you can add [more pages](more-pages.md).

## Preview your site

Run the local server with `docsify serve`. You can preview your site in your browser on `http://localhost:3000`.

```bash
docsify serve docs
```

?> For more use cases of `docsify-cli`, head over to the [docsify-cli documentation](https://github.com/docsifyjs/docsify-cli).

## Manual initialization

If you don't like `npm` or have trouble installing the tool, you can manually create `index.html`:

```html
<!-- index.html -->

<!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
    <meta name="viewport" content="width=device-width,initial-scale=1" />
    <meta charset="UTF-8" />
    <link rel="stylesheet" href="//unpkg.com/docsify/themes/vue.css" />
  </head>
  <body>
    <div id="app"></div>
    <script>
      window.$docsify = {
        //...
      };
    </script>
    <script src="//unpkg.com/docsify/lib/docsify.min.js"></script>
  </body>
</html>
```

If you installed python on your system, you can easily use it to run a static server to preview your site.

```bash
cd docs && python -m SimpleHTTPServer 3000
```

## Loading dialog

If you want, you can show a loading dialog before docsify starts to render your documentation:

```html
<!-- index.html -->

<div id="app">Please wait...</div>
```

You should set the `data-app` attribute if you changed `el`:

```html
<!-- index.html -->

<div data-app id="main">Please wait...</div>

<script>
  window.$docsify = {
    el: "#main",
  };
</script>
```
