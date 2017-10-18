# Authentication

To query the api you'll have to authenticate yourself.
This is done by OAuth 2 and for a stand-alone application we would suggest using Client Credentials as grant type.

## Client Credentials Flow

`GET https://signport.se/api/oauthservice/token?grant_type=client_credentials&client_id=<CLIENT_ID>&client_secret=<CLIENT_SECRET>`

```shell
curl "https://signport.se/api/oauthservice/token?grant_type=client_credentials&client_id=<CLIENT_ID>&client_secret=<CLIENT_SECRET>"
```

> The above command returns JSON structured like this:

```json
{
  "access_token": "<ACCESS_TOKEN>",
  "expires_in": 3600,
  "refresh_token": "<REFRESH_TOKEN>",
  "token_type": "Bearer"
}
```

### Url Parameters

Parameter | Description
--------- | -----------
CLIENT_ID | The ID identifying your application
CLIENT_SECRET | The secret received from us for your application

Save the access_token and refresh_token for use with all your requests against the api.

<aside class="success">
Remember — All requests against the backend needs to be authenticated!
</aside>

## Example api-call

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here"
  -H "Authorization: <ACCESS_TOKEN_HERE>"
```
> Make sure to replace `ACCESS_TOKEN_HERE` with your API key.

Signport uses API keys to allow access to the API. You can get your key by following the authentication flow above.

Signport expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: ACCESS_TOKEN_HERE`

<aside class="notice">
You must replace <code>ACCESS_TOKEN_HERE</code> with your personal API key.
</aside>