# Manage account Embed (Add/update card and cancel/reactivate subscription)

!!! warning "Note"
    This embed will require code to be placed in your server

1. Go to "Embeddables"
1. Click on `Billing Settings`
1. Select your backend language/framework
1. Place the server code in your server
1. Place the client code on the client, and insert the token from the server when a logged in user visits the page
1. Customers can now add/update a funding source and cancel/reactivate their subscriptions using this page

## Billing Settings options
In the init for a request embed, these are the options which can customize the embed

| Attribute        | Type           | Description  |
| ------------- |:-------------:| -----:|
| url      | string      |   URL of your servicebot instance |
| selector | [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)|  The element you want to turn into a form |
| handleResponse | function(response) | a function which gets called after billing operations occur |
| token | string | A JSON web token for the user account being managed (generated by the server code) |
| [disablePlanChange] | boolean | if true, a customer will not be able to change their plan using the embeddable |
| [serviceInstanceId] | string | If specified, only pull up the billing settings for this specific instance, useful if your customers can have multiple subscriptions and you don't want them to see all of them on one page |

## Example Billing Settings Config
```javascript
    Servicebot.BillingSettings({
        url : "https://example.serviceshop.io", 
        selector : document.getElementById('servicebot-management-form'),
        handleResponse : (response) => { 
            console.log(response);
        },
        token: "INSERT_TOKEN_HERE",
        disablePlanChange: false
    })
```

## Tips
- If your language/framework is not available, you can use a JSON Web Token library to generate a token, or, using an administrator account, use [this](https://api-docs.servicebot.io/#operation--users--id--token-post) API to get a token for a specific customer
- The server side code can be reused for the [seat management embed](https://docs.servicebot.io/seat-management-embed) as it also uses a JSON Web Token
- Changing a pricing plan will trigger a webhook call
