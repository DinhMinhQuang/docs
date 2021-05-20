# ISec

Main Service

# Schema

The schema has some main parts: name, version, settings, actions, methods, events.

## Base properties

The Service has some base properties in the schema.

```javascript
module.exports = {
  name: "isec",
  version: 1,
};
```

The name is a mandatory property so it must be defined. It’s the first part of action name when you call it.

To disable service name prefixing set $noServiceNamePrefix: true in Service settings.

The version is an optional property. Use it to run multiple version from the same service. It is a prefix in the action name. It can be a Number or a String.

```javascript
// isec.v1.service.js
module.exports = {
    name: "isec",
    version: 1,
    actions: {
        create() {...}
    }
}
```

To call this create action on version 1 service:

```javscript
broker.call("v1.isec.create");
```

REST call
Via API Gateway, make a request to GET /v1/isec/create.

To disable version prefixing set $noVersionPrefix: true in Service settings.

<a id="transferinfo">
<h1> Define a Transfer Information</h1>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: ["message", "fullname", "phone"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    getTransferInfo: {
      rest: "GET /transferInformation",
      params: {
        input: {
          iSecId: { type: "number" },
          phone: { type: "string" },
        },
        paging: {
          start: { type: "number" },
          limit: { type: "number" },
        },
        clientId: { type: "string" },
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

<a id="getisec">
<h1> Define a Query</h1>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: ["message", "count", "countPending", "balancePending", "items"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    getISecList: {
      rest: "GET /",
      params: {
        filter: {
          iSecCode: { type: "string" },
          state: { type: "string" },
          iSecHint: { type: "string" },
          iSecId: { type: "number" },
          bulkId: { type: "string" },
          partnerTransaction: { type: "string" },
          createdAt: {
            from: { type: "date" },
            to: { type: "date" },
          },
          orderId: { type: "string" },
        },
        paging: {
          start: { type: "number" },
          limit: { type: "number" },
        },
        clientId: { type: "string" },
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

<a id="scratchinfo">
<h1>Define a Scratch Information</h2>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: ["message", "iSecInfo"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    getScratchInfo: {
      rest: "GET /scratchInformation",
      params: {
        iSecCode: { type: "string" },
        clientId: { type: "string" },
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

{handler} is a function handler a logic code

<a id="depositinfo">
<h1> Define a Deposit Information</h1>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: ["message", "items"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    getDepositInfo: {
      rest: "GET /depositInformation",
      params: {
        filter: {
          id: { type: "number" },
          state: { type: "string" },
          iSecHint: { type: "string" },
          iSecId: { type: "number" },
          createdAt: {
            from: { type: "date" },
            to: { type: "date" },
          },
        },
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

<a id="redeeminfo">
<h1> Define a Redeem Information</h1>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: ["message", "iSecInfo"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  getRedeemInfo: {
    login: {
      rest: "GET /redeemInfo",
      params: {
        iSecCode: { type: "string" },
        clientId: { type: "string" },
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

<a id="createisec">
<h1>
Define a Create ISec
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: ["succeeded", "message", "iSecInfo", "history", "payment"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /create",
      params: {
        amount: { type: String },
        clientId: { type: "string", require: true },
        transaction: { type: "String" },
        payment: {
          wallet: {
            active: { type: "boolean" },
            securityCode: { type: "number" },
          },
        },
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

<a id="redeemisec">
<h1>
Define a Redeem ISec
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: [
      "accountId",
      "receiverId",
      "iSecId",
      "transaction",
      "description",
      "iSecInfo",
      "state",
      "createdAt",
      "history",
      "succeeded",
      "message",
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
      rest: "POST /redeemISec",
      params: {
        iSecCode: { type: "string" },
        description: { type: "string" },
        clientId: { type: "string" },
        transport: {
          wallet: {
            accountId: { type: "number", require: true },
          },
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

<a id="saveisec">
<h1>
Define a Verify Password to Change Password
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: ["succeeded", "message", "iSecInfo", "history"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /saveISec",
      params: {
        iSecCode: { type: "string" },
        clientId: { type: "string", require: true },
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

<a id="transferisec">
<h1>
Define Transfer ISec
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: [
      "succeeded",
      "message",
      "iSecId",
      "iSecinfo",
      "transaction",
      "description",
      "fullname",
      "phone",
      "history",
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
      rest: "POST /transferISec",
      params: {
        iSecId: { type: "number", require: true },
        phone: { type: "string", require: true },
        securityCode: { type: "string", require: true },
        isRemember: { type: "boolean", require: true },
        clientId: { type: "string", require: true },
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

<a id="canncelisec">
<h1>
Define a Cancel ISec
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: [
      "succeeded",
      "message",
      "accountId",
      "iSecId",
      "transaction",
      "description",
      "iSecInfo",
      "history",
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
      rest: "POST /cancelIsec",
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

<a id="saveisecinfo">
<h1>
Define a Save ISec Information
</h1>
</a>

## Response

```javascript
module.exports = {
  name: "isec",
  version: 1,
  settings: {
    fields: ["succeeded", "message", "iSecInfo"],
  },
};
```

{fields} are validate response to this action

## Action

```javascript
module.exports = {
  actions: {
    login: {
      rest: "POST /saveISecInfo",
      params: {
        iSecCode: { type: "string" },
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