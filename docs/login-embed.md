# Login Embed

1. Go to "Embeddables"
1. Click on `Login`
1. Copy the HTML given
1. Paste on your existing site where you would like a login page to be generated

## Login  options

| Attribute        | Type           | Description  |
| ------------- |:-------------:| -----:|
| url      | string      |   URL of your servicebot instance |
| selector | [Element](https://developer.mozilla.org/en-US/docs/Web/API/Element)|  The element you want to turn into a form |
| handleResponse | function(response) | a function which gets called after the user logs in, response is a json containing the user obejct, token, owned service instances, and seats following the form `{seats, instances, user, token}`, will be called also after complete registration and after password reset completes |
| [uid] | string | userId of a user to reset password for, when paired with a resetToken, presents the user with a page to reset their password, also can be passed as a url variable like https://example.com/reset?resetToken=xxxxx&uid=12 |
| [resetToken] | string | resetToken generated by user using the forgot password functionality, when paired with a uid the login form will display a password reset form, also can be passed as a url variable like https://example.com/reset?resetToken=xxxxx&uid=12|
| [inviteToken] | string | inviteToken generated from the seat management form, if present, will present the user with an account registration page, also can be passed as a url variable like https://example.com/register?inviteToken=xxxxx|
| [googleScope] | string | the scopes requested of the client when using google authentication, should be a list of scopes seperated by spaces, defaults to "profile email", you can find a list of scopes [here](https://developers.google.com/identity/protocols/googlescopes)
| [accessType] | string | if set to "offline", a refresh_token will be generated and attached to the user object instead of the traditional access_token. The oauthResponse attribute will contain a useless code that was consumed by the server to generate the refresh_token. offline access also disables traditional username/password authentication. 


## Example Login Config
```javascript
    Servicebot.Login({
        url : "https://example.serviceshop.io", 
        selector : document.getElementById('servicebot-login-form'),
        handleResponse : (response) => {
            console.log(response.user) //user object
            console.log(response.token) //JSON Web Token to be validated from your app, also contains user object encoded
            console.log(response.seats) //seats this user belongs to
            console.log(response.instances) //service instances this user owns
            console.log(response.oauthResponse) //the response from an oauthProvider used to login such as Google
        }
    })
```
## Tips
- If you pass inviteToken or resetToken and uid as URL variables, they will be pulled automatically into the embed, the invite email and reset password email should have these url variables automatically attached to the URL so you just need to make sure the URLs your configure are pointed to a page with the login embed
- You can decode the JSON web token to get the user object which will include references to service instances, seats, and funds
