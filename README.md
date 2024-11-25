# IPQualityScore NPM Device Fingerprint Tracker Package for React

IPQS combines our advanced industry blacklist fraud data and global threat network with device fingerprinting technologies to offer one of the most advanced anti-fraud tools on the market. The IPQS device fingerprint tracker tracks devices using advanced algorithms while offering websites the ability to safeguard themselves against bot attacks, duplicate account creation, chargeback fraud, and much more.

The IPQS device fingerprint tracker can help:

- Stop account takeover attacks
- Stop bot clicks
- Prevent chargebacks
- Stop fraudulant transactions
- Prevent affiliate fraud

And much more.

This NPM package is built for JavaScript frameworks SPA tools such as React, Vue, Angular, and more. It’s compatible with both JavaScript and Typescript.

## Further Reading

- [Creating a Device Fingerprint Tracker](https://www.ipqualityscore.com/user/tracker/new)
- [Device Fingerprint Overview](https://www.ipqualityscore.com/device-fingerprinting)
- [Device Fingerprint API](https://www.ipqualityscore.com/documentation/device-fingerprint/overview)

## Installation

npm i node_js_ipqs_device_tracker

## Initialization

First, import the IPQualityScore device fingerprint tracker into your project:

```javascript
import DeviceFingerprint from "node_js_ipqs_device_tracker";
```

Next, initialize the device fingerprint tracker in the webapp:

```javascript
const secretKey = "YourSecretKey";
DeviceFingerprint.initializeScriptAsync(secretKey)
  .then(async () => {
    DeviceFingerprint.AfterResult((result) => {
      console.log(result);
    });
    DeviceFingerprint.Init();
  })
  .catch((err) => {
    console.log("DT Error");
    console.log(err);
  });
```

### How To Find The Device Fingerprint Tracker Secret Key

Before integrating the IPQS device fingerprint tracker in the webapp, a device tracker needs to be created in your IPQS account. The secret key for the device fingerprint tracker is tied to the device tracker itself. It does not use your IPQS account's API key.

1. Log in to your IPQS account: [https://www.ipqualityscore.com/login](https://www.ipqualityscore.com/login)
2. Navigate to the Device Fingerprint Tracking Dashboard from the left-hand navigation bar: [https://www.ipqualityscore.com/user/tracker](https://www.ipqualityscore.com/user/tracker)
3. (A) If a tracker has not been created yet, click the blue 'Create New Fingerprint Tracker' button to create one first.
4. (B) Scroll to the bottom of the Device Fingerprint Tracking Dashboard, and find the device tracker that is going to be used in the webapp.
5. Click on the Red Details button next to the device tracker.

A new page will load with the documentation and JS snippet for the device tracker. The secret key is located in the JS snippet between "https://www.ipqscdn.com/api/*/" and "/learn.js". Copy long alphanumeric string in that URL. This is the device fingerprint tracker secret key.

# React Examples

To initialize the Device Tracker Package in React, you can do it in one of two ways

### Asynchronously (recommended)

```javascript
import DeviceFingerprint from "node_js_ipqs_device_tracker";

function App() {
  const secretKey = `YourSecretKey`;
  useEffect(() => {
    DeviceFingerprint.initializeScriptAsync(secretKey)
      .then(() => {
        DeviceFingerprint.Init();
      })
      .catch(() => {
        // Any errors loading the external script will be caught here
      });
  });
}
```

### Synchronously (not recommended)

This is not recommended as this will not tell you when the external script has been loaded, nor will it be easy to catch any errors loading an external script

```javascript
import DeviceFingerprint from "ipqs-device-fingerprint-for-react";

function App() {
  useEffect(() => {
    DeviceFingerprint.initializeScript();
    setTimeout(function () {
      DeviceFingerprint.AfterResult((result) => {
        console.log(result);
      });
      DeviceFingerprint.Init();
    }, 1000);
  });
}
```

# Vue Examples

### Options API

```javascript
export default {
  name: "App",
  components: {
    NavBar,
  },
  setup() {
    const secretKey = 'YourSecretKey';
    DeviceFingerprint.initializeScriptAsync(secretKey)
      .then(async () => {
        DeviceFingerprint.AfterResult((result) => {
          console.log(result);
        });
        DeviceFingerprint.Init();
      })
      .catch((err) => {
        console.log("DT Error");
        console.log(err);
      });
  },
  mounted() {},
  // created: {},
  computed: {},
  watch: {},
  methods: {},
};
</script>
```

## Other Methods

**NOTE**: The following methods will only work after `initializeScript()` or `initializeScriptAsync()` have successfully loaded in React.

### Init();

Initializes the Device Tracker

```javascript
DeviceFingerprint.initializeScriptAsync(secretKey).then(() => {
  const callback = (result) => {
    console.log(result);
  };
  DeviceFingerprint.AfterResult(callback);
  DeviceFingerprint.Init();
});
```

### AfterResult(callback);

Enables a callback function to be called when DeviceFingerprint.Init() succeeds

```javascript
DeviceFingerprint.initializeScriptAsync(secretKey).then(() => {
  const callback = (result) => {
    console.log(result);
  };
  DeviceFingerprint.AfterResult(callback);
  DeviceFingerprint.Init();
});
```

### AfterFailure(callback);

Enables a callback function to be called when DeviceFingerprint.Init() fails

```javascript
DeviceFingerprint.initializeScriptAsync(secretKey).then(() => {
  const callback = (result) => {
    console.log(result);
  };
  DeviceFingerprint.AfterFailure(callback);
  DeviceFingerprint.Init();
});
```

### Pause();

Pauses the Device Tracker

```javascript
DeviceFingerprint.initializeScriptAsync(secretKey).then(() => {
  DeviceFingerprint.Init();
  DeviceFingerprint.Pause();
});
```

### Resume();

Resumes the Device Tracker. This works in conjunction with `Resume()`

```javascript
DeviceFingerprint.initializeScriptAsync(secretKey).then(() => {
  DeviceFingerprint.Init();
  DeviceFingerprint.Pause();
  DeviceFingerprint.Resume();
});
```

### Trigger(formId, callback);

Sets a trigger on a form based on a specific id, and assigns a callback for when that form is submitted.

If used in conjunction with `AfterResult()`, you will not fire the result callback until that specific form is submitted.

This must be called before `Init()`

```javascript
DeviceFingerprint.initializeScriptAsync(secretKey).then(() => {
  const formId = "someFormId";
  const callback = (event) => {
    event.preventDefault();
  };
  DeviceFingerprint.Trigger(`#${formId}`, callback);
  DeviceFingerprint.Init();
});
```

```html
<form id="{formId}">
  <button type="submit">Submit</button>
</form>
```

### SetFormFieldPrepend(prefix: string);

Sets the Form Field Prepend prefix for form submission triggers.

This works in conjunction with `Trigger()` and must be called before `Init()`

```javascript
DeviceFingerprint.initializeScriptAsync(secretKey).then(() => {
  const prefix = "somePrefix";
  DeviceFingerprint.SetFormFieldPrepend(prefix);

  const formId = "someFormId";
  const callback = (event) => {
    event.preventDefault();
  };
  DeviceFingerprint.Trigger(`#${formId}`, callback);
  DeviceFingerprint.Init();
});
```

```html
<form id="{formId}">
  <button type="submit">Submit</button>
</form>
```

### Field(fieldName: string, fieldId: number);

Allows you to specify additional fields for order submission and payment processing

```javascript
DeviceFingerprint.initializeScriptAsync(secretKey).then(() => {
  const fieldName = "someField";
  const fieldId = "#someFieldId";
  DeviceFingerprint.Field(fieldName, fieldId);
  DeviceFingerprint.Init();
});
```

# Defining a Custom Domain & Tracker

The sync and async functions mentioned above use the default www.ipqscdn.com domain and a wildcard tracker. For security purposes, it may be a good practice to define the custom domain hosting the IPQS tracker script and the tracker name. Using the custom options will require the secret key, custom domain, and tracker name passed to the sync or async calls.

The IPQS custom domain must be registered to an IPQualityScore account before the custom domain can be used to host the device tracking scripts. If your account does not have a custom domain registered with it, pass the 'www.ipqscdn.com' domain instead.

Do not include 'https://' in the custom domain value. Only add the subdomain (if needed), the domain, and TLD in the custom_domain string value.

## Using Async Options

```javascript
    const secretKey = 'YourSecretKey';
    const tracker = "example.com";
    const custom_domain = "example-host-domain.com"
    DeviceFingerprint.initializeScriptAsyncCustom(secretKey,custom_domain, tracker )
      .then(async () => {
        DeviceFingerprint.AfterResult((result) => {
          console.log(result);
        });
        DeviceFingerprint.Init();
      });

</script>
```

## Or Using Sync Options

```javascript
import DeviceFingerprint from "ipqs-device-fingerprint-for-react";

const secretKey = "YourSecretKey";
const tracker = "example.com";
const custom_domain = "example-host-domain.com";

DeviceFingerprint.initializeScript(secretKey, custom_domain, tracker);
setTimeout(function () {
  DeviceFingerprint.AfterResult((result) => {
    console.log(result);
  });
  DeviceFingerprint.Init();
}, 1000);
```

# Debugging

Debugging is optional. Debugging is built into the library. Pass a 'true' boolean valaue as the last paramter in any function call to enable console logging for that function. The debugging parameter is optional, and no values need to be passed if debugging does not need to be enabled.

Examples:

```javascript
// initializeScript
DeviceFingerprint.initializeScript(secretKey, custom_domain, tracker, true);

// initializeScriptAsyncCustom
DeviceFingerprint.initializeScriptAsyncCustom(
  secretKey,
  custom_domain,
  tracker,
  true
);

// initializeScriptAsync
DeviceFingerprint.initializeScriptAsync(secretKey, true);

// AfterResult
DeviceFingerprint.AfterResult((result) => {
  console.log(result);
}, true);

// Init
DeviceFingerprint.Init(true);
```

**Warning**: Notice that the 'true' value is placed after the callback function as a second parameter in the 'AfterResult' function call above. The 'true' boolean value will always be the last parameter passed. If the function call includes a callback function, such as the 'AfterResult' function, the boolean value must be placed after the callback function.

# Need Help?

If you need additional help or would like to schedule a meeting for assistance, open a help ticket in your [IPQS account](https://www.ipqualityscore.com/user/support/new).
