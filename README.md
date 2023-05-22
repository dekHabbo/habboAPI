# habboEnhancer
Greasemonkey script for checking names, registering accounts and offering a quick-launch Habbo button.

## API Documentation

This documentation provides information about the API endpoints and requests related to account creation and name availability on Habbo.com. The API allows you to interact with the Habbo platform programmatically. You can use it to obtain tokens, create accounts, and check name availability.

### Base URL
The base URL for all API requests is:
```
https://www.habbo.com/api
```

### Authentication
Authentication is required for some API endpoints to ensure the security of user data. The `x-habbo-fingerprint` header should be included in the requests to authenticate the client. The fingerprint value uniquely identifies the client.

### Headers
The following headers are commonly used in the API requests:

- `User-Agent` (string): The user agent string of the client making the request. It helps identify the client software and version.
- `Accept` (string): The accepted response content types. It specifies the format in which the client expects the response.
- `Accept-Language` (string): The preferred language for the response. It helps determine the language of the returned data.
- `Content-Type` (string): The content type of the request body. It specifies the format of the data sent in the request.
- `x-habbo-fingerprint` (string): The unique fingerprint of the client. It authenticates the client making the request.
- `Sec-Fetch-Dest` (string): The destination type of the fetch request. It specifies the destination of the fetch request.
- `Sec-Fetch-Mode` (string): The mode of the fetch request. It specifies the mode of the fetch request.
- `Sec-Fetch-Site` (string): The site of the fetch request. It specifies the site of the fetch request.

### Endpoints

#### 1. Token Request

This endpoint is used to obtain a token for the client.

- Endpoint: `/client/clientnative/url`
- Method: `POST`

##### Request

```javascript
fetch("https://www.habbo.com/api/client/clientnative/url", {
    credentials: "include",
    headers: {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/113.0",
        "Accept": "application/json, text/plain, */*",
        "Accept-Language": "en-GB,en;q=0.5",
        "x-habbo-fingerprint": "#",
        "Sec-Fetch-Dest": "empty",
        "Sec-Fetch-Mode": "cors",
        "Sec-Fetch-Site": "same-origin"
    },
    referrer: "https://www.habbo.com/",
    method: "POST",
    mode: "cors"
});
```

##### Response

The response is a JSON object containing the following properties:

- `clienturl` (string): The URL used to connect the client to the Habbo server.
- `ticket` (string): The ticket associated with the token.

#### 2. Account Creation

This endpoint is used to create a new Habbo account.

- Endpoint: `/user/avatars`
- Method: `POST`

##### Request

To create a new account, replace `USERNAME` in the request body with the desired username.

```javascript
fetch("https://www.habbo.com/api/user/avatars", {
    credentials: "include",
    headers: {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/113.0",
        "Accept": "application/json, text/plain, */*",
        "Accept-Language": "en-GB,en;q=0.

5",
        "Content-Type": "application/json;charset=utf-8",
        "x-habbo-fingerprint": "#",
        "Sec-Fetch-Dest": "empty",
        "Sec-Fetch-Mode": "cors",
        "Sec-Fetch-Site": "same-origin"
    },
    referrer: "https://www.habbo.com/settings/avatars",
    body: JSON.stringify({
        "name": "USERNAME"
    }),
    method: "POST",
    mode: "cors"
});
```

##### Response

The response is a JSON object containing the following properties:

- `uniqueId` (string): The unique identifier for the created account.
- `name` (string): The username of the created account.
- `figureString` (string): The figure string associated with the account.
- `motto` (string): The motto of the account.
- `buildersClubMember` (boolean): Indicates whether the account has Builders Club membership.
- `habboClubMember` (boolean): Indicates whether the account has Habbo Club membership.
- `lastWebAccess` (string): The timestamp of the last web access for the account.
- `creationTime` (string): The timestamp of the account creation.

#### 3. Name Check Request

This endpoint is used to check the availability of a username.

- Endpoint: `/user/avatars/check-name`
- Method: `GET`

##### Request

To check the availability of a username, replace `TESTNAME` in the request URL with the desired username.

```javascript
fetch("https://www.habbo.com/api/user/avatars/check-name?name=TESTNAME", {
    credentials: "include",
    headers: {
        "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:109.0) Gecko/20100101 Firefox/113.0",
        "Accept": "application/json, text/plain, */*",
        "Accept-Language": "en-GB,en;q=0.5",
        "x-habbo-fingerprint": "#",
        "Sec-Fetch-Dest": "empty",
        "Sec-Fetch-Mode": "cors",
        "Sec-Fetch-Site": "same-origin"
    },
    referrer: "https://www.habbo.com/settings/avatars",
    method: "GET",
    mode: "cors"
});
```

##### Response

The response is a JSON object containing the following property:

- `isAvailable` (boolean): Indicates whether the specified username is available (`true`) or unavailable (`false`).

Please note that a user must be logged in to habbo.com to use this API.
