# Account

Main Service

# Schema

The schema has some main parts: name, version, settings, actions, methods, events.

## Base properties

The Service has some base properties in the schema.

```javascript
module.exports = {
  name: "account",
  version: 1,
};
```

The name is a mandatory property so it must be defined. It’s the first part of action name when you call it.

To disable service name prefixing set $noServiceNamePrefix: true in Service settings.

The version is an optional property. Use it to run multiple version from the same service. It is a prefix in the action name. It can be a Number or a String.

```javascript
// account.v1.service.js
module.exports = {
    name: "account",
    version: 1,
    actions: {
        login() {...}
    }
}
```

To call this find action on version 2 service:

```javscript
broker.call("v1.account.login");
```

REST call
Via API Gateway, make a request to POST /v1/account/login.

To disable version prefixing set $noVersionPrefix: true in Service settings.

<a id="query">
<h1> Define a Query</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: [
      "accountId",
      "fullname",
      "alias",
      "page",
      "phone",
      "email",
      "kyc",
      "avatar",
      "gender",
      "birthday",
      "address",
      "isActive",
      "state",
      "isHandShake",
      "isVerifiedEmail",
      "isWaitingEmailVerification",
      "accountType",
    ],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "GET /",
      params: {
        phone: { type: "string" },
        handShake: { type: "string" },
        client { type: "string" },
      },
      async handler(ctx) {
        /// handler module login
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is function handler a logic code

<a id="login">
<h1> Define a Login</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: [
      "state",
      "succeeded",
      "message",
      "stateVersion",
      "updateTitle",
      "updateURL",
      "accessToken",
      "accessTokenKey",
    ],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /login",
      params: {
        phone: { type: "string", require: true },
        password: { type: "string", require: true },
        activeCode: { type: "string" },
        client { type: "string" },
        handShake: { type: "string" },
      },
      async handler(ctx) {
        /// handler module login
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is function handler a logic code

<a id="logout">
<h1>Define a Logout</h2>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /logout",
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{handler} is a function handler a logic code

<a id="register">
<h1> Define a Register</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["state", "succeeded", "accessToken", "message"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /register",
      params: {
        phone: { type: "string", require: true },
        password: { type: "string", require: true },
        fullname: { type: "string" },
        activeCode: { type: "string" },
        client { type: "string" },
        handShake: { type: "string" },
        accountType: { type: "string" },
      },
      async handler(ctx) {
        /// handler module login
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is function handler a logic code

<a id="sendotpregister">
<h1> Define a Send OTP Register </h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["timeDelay", "succeeded", "state", "message"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /register/sendOTP",
      params: {
        phone: { type: "string", require: true },
        client { type: "string", require: true },
        handShake: { type: "string" },
      },
      async handler(ctx) {
        /// handler module login
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is function handler a logic code


<a id="verifyactivecoderegister">
<h1>
Define a VerifyActiveCode Register
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "state", "message"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /register/verifyActiveCode",
      params: {
        handShake: { type: String },
        phone: { type: "string", require: true },
        client { type: "string", require: true },
        client { type: "string" },
      },
      async handler(ctx) {
        /// handler module login
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is function handler a logic code

<a id="changepassword">
<h1>
Define a ChangePassword
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "state", "accessToken"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "PUT /changePassword",
      params: {
        lastPassword: { type: "string", require: true },
        password: { type: "string", require: true },
        client { type: "string", require: true },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="verifypassword">
<h1>
Define a Verify Password to Change Password
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /changePassword",
      params: {
        lastPassword: { type: "string", require: true },
        client { type: "string", require: true },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="sendotpforgotpassword">
<h1>
Define a SendOTP for Forgot Password
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /forgotPassword/sendOTP",
      params: {
        phone: { type: "string", require: true },
        client { type: "string", require: true },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="verifyotpforgotpassword">
<h1>
Define a VerifyOTP for Forgot Password
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message", "state", "linkedNumber"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /forgotPassword/sendOTP",
      params: {
        phone: { type: "string", require: true },
        activeCode: { type: "string", require: true },
        client { type: "string", require: true },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="verifyprofileforgotpassword">
<h1>
Define a Verify Profile for Forgot Password
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message", "state", "confirmCode"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /forgotPassword/sendOTP",
      params: {
        phone: { type: "string", require: true },
        client { type: "string", require: true },
        confirmInfo: {
          cardNumber: "string",
          identifyNumber: "string",
          birthday: "string",
        },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="updatepassword">
<h1>
Define a Update Password for Forgot Password
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message", "state", "confirmCode"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "PUT /forgotPassword/updatePassword",
      params: {
        phone: { type: "string", require: true },
        password: { type: "string", require: true },
        activeCode: { type: "string", require: true },
        client { type: "string", require: true },
        confirmCode: { type: "string" },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="kyc">
<h1>
Define a Register KYC
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: [
      "succeeded",
      "message",
      "createdAt",
      "limitTransactionAmount",
      "approvedTimeExpected",
    ],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "PUT /kyc",
      params: {
        fullname: { type: "string" },
        gender: { type: "string" },
        birthday: { type: "string" },
        address: { type: "string" },
        identifyType: { type: "string" },
        issuedAt: { type: "date" },
        placeOfIssue: { type: "string" },
        video: { type: "string" },
        face: { type: "string" },
        image: {
          front: { type: "string" },
          back: { type: "string" },
        },
        client { type: "string", require: true },
        merchant: {
          taxCode: { type: "string" },
          name: { type: "string" },
          shortName: { type: "string" },
          website: { type: "string" },
          logo: { type: "string" },
          address: { type: "string" },
          business: { type: "string" },
          representative: { type: "string" },
          openTime: { type: "string" },
          lincenseImage: { type: "array" },
        },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="securitycodepassword">
<h1>
Define a SecurityCode By Password
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message", "securityCode", "code"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /securityCode/password",
      params: {
        client { type: "string", require: true },
        password: { type: "string", require: true },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="securitycodetouchid">
<h1>
Define a SecurityCode by TouchId
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message", "state", "code"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /securityCode/touchId",
      params: {
        account { type: "number", require: true },
        sign: { type: "string", require: true },
        signType: { type: "string", require: true },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="sendotptrustdevice">
<h1>
Define a SendOTP TrustDevice
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /trustDevice/sendOTP",
      params: {
        client { type: "string", require: true },
        phone: { type: "string", require: true },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="deletetrustdevice">
<h1>
Define a Delete TrustDevice
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "DEL /trustDevice",
      params: {
        client { type: "string" },
      },
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code

<a id="verifyemail">
<h1>
Define a Verify Email
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "account",
  version: 1,
  settings: {
    fields: ["succeeded", "message"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /verifyEmail",
      params: {
        token: { type: "string", require: true },
      }
      async handler(ctx) {
        /// handler module
        return;
      },
    },
  },
};
```

{rest} is define method and end point of this action

{params} is validate a request

{handler} is a function handler a logic code
