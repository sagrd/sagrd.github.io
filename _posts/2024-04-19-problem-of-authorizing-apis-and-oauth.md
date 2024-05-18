---
layout: post
---
- Video version of the concept/post can be found [here](https://www.youtube.com/watch?v=cFAG_yuzfkg)

Before we dive into what OAuth actually is and how it works, it’s important to understand the problem we are trying to solve with it—authorizing our API.
Authorization concerns determining what actions someone is permitted to do, dealing with permissions and access control. For example, a user might be allowed to read a file but not edit it, which is an aspect of authorization. This differs from authentication, which involves verifying an identity, typically with a combination of username and password.

## The Problem with Sharing Credentials
To illustrate the issues OAuth addresses, let’s consider a scenario involving a frame app that takes data from Facebook to create a framed profile picture—a common application many might have seen on Facebook. Here, Facebook needs to grant permissions to this frame app, such as reading the profile picture but not changing it or adding status updates.
One naive approach to solve this problem is sharing user credentials, like giving the frame app the username and password of the Facebook account. However, this approach has significant drawbacks:
- Unrestricted Access: The frame app would have unrestricted access to the user's Facebook account.
- User Impersonation: There’s no way to distinguish if the access is done by the user or the app.
- Password Changes: Users would need to update their credentials on the frame app every time they change their Facebook password.
- Security Risks: If the frame app is compromised, the hacker could access the user’s Facebook account.
- Multi-Factor Authentication: Implementing multi-factor authentication becomes challenging since the app still requires user credentials.
- User Credentials Exposure: Storing user credentials in the application poses a risk of exposure, necessitating complex measures like non-reversible password hashing algorithms.

## Cookies and Cross-Site Request Forgery (CSRF)
Using cookies is another method to maintain user session states across requests after a successful login. However, authorizing an application through cookies can lead to CSRF attacks, where unauthorized requests can be made from the user’s session.

## API Keys
API keys offer another mechanism for authorization. Here are key points about API keys:
- Unique Identifier: API keys uniquely authenticate and authorize requests.
- Separate Keys: Each application can have its own keys, simplifying authorization without sharing user credentials.
- Scopes: Key-specific permissions can be defined, allowing multi-factor authentication implementation.
However, API keys also have drawbacks:
- Lack of Standards: There is no standardized design or format for API keys.
- Expiration Issues: Keys need manual management for expiration and renewal.
- User Identity: API keys only identify the project/application but not individual users.

## OAuth: A Better Solution for Authorization
OAuth is an authorization framework designed to provide secure, delegated access to HTTP APIs. It enables users to grant third-party applications limited access to their resources without sharing their credentials. OAuth comprises four main components:
- Resource: API that requires authorization, such as Facebook's profile picture API.
- Client App: The application requesting access (e.g., frame app).
- User: The resource owner (e.g., Facebook user).
- Authorization Server: Trusted server managing authorization requests (e.g., Facebook’s authentication server).

### OAuth Flow
- Authorization Request: The client app requests authorization from the authorization server, typically through a browser redirect.
- User Authentication: The user authenticates and consents to the access request via the authorization server.
- Authorization Grant: The authorization server issues an authorization grant to the client app.
- Access Token Exchange: The client app exchanges the authorization grant for an access token.
- Resource Access: The client app uses the access token to access the protected resource. Example: The frame app requests Facebook’s authorization server to read a user's profile picture. Upon user consent and authentication, the app obtains an access token, which it uses to fetch the profile picture securely.

### Benefits of OAuth
- Scoped Access: Specify permissions explicitly for different access levels.
- Separation of Concerns: Separates user authentication from third-party application access.
- Enhanced Security: Minimizes risks of credential exposure and allows the use of multi-factor authentication.
- Extendable: Can be integrated with identity specifications like OpenID Connect for additional functions.
- Improvements and Additional Concepts in OAuth
- Refresh Tokens: OAuth supports refresh tokens, which allow clients to request a new access token without re-authenticating the user. This is useful for long-lived access.
- JWT Tokens: OAuth often uses JSON Web Tokens (JWT) for access tokens, which carry the claims, expiration times, and signatures, making verification efficient.

## OAuth 2.0: 
OAuth 2.0 is the industry-standard protocol for authorization, offering more flexibility, security, and ease of implementation compared to its predecessor, OAuth 1.0. It supports various grant types catering to different use cases such as Authorization Code Grant, Implicit Grant, Resource Owner Password Credentials Grant, and Client Credentials Grant.

### OAuth Grant Types
- Authorization Code Grant: Used in web applications to obtain both access tokens and refresh tokens by redirecting the user’s browser to the authorization server. It's suitable for scenarios where the client can protect the confidentiality of the authorization code.
- Implicit Grant: Simplified authorization code flow optimized for public clients, such as browser-based applications, where the access token is returned directly in the URL fragment. It does not support refresh tokens and is suitable for short-lived sessions.
- Resource Owner Password Credentials Grant: Allows the exchange of a user’s credentials (username and password) for an access token directly. This grant type is suitable for legacy applications where direct credential input is required but should be used sparingly due to security risks.
- Client Credentials Grant: Used in machine-to-machine communications where no user is present. The client credentials (client ID and secret) are used to authenticate and obtain an access token.

### Implementing OAuth 2.0
Here's a step-by-step outline of implementing OAuth 2.0 in your application:
- Register Your Application: Register your client application with the authorization server to obtain client credentials (client ID and secret).
- Redirect to Authorization Server: Redirect the user from your application to the authorization server's consent page where they grant access.
- Receive Authorization Code: Upon user consent, the authorization server redirects back to your application with an authorization code.
- Exchange Authorization Code for Access Token: The client application exchanges the received authorization code for an access token (and optionally a refresh token) by sending a request to the authorization server's token endpoint.
- Access Protected Resources: Use the access token to make authorized requests to the protected resources.

### Example OAuth Setup
- User Registration: Redirect users to the authorization server with necessary query parameters (client_id, redirect_uri, response_type, scope).
Example URL:
```
https://authorization-server.com/auth?client_id=CLIENT_ID&redirect_uri=REDIRECT_URI&response_type=code&scope=read_profile
```
- Handle Authorization Response:
Authorization code obtained from the query parameter upon redirection.
```
https://client-app.com/callback?code=AUTHORIZATION_CODE
```
- Exchange Code for Token:
```
curl -X POST \
https://authorization-server.com/token \
-H "Content-Type: application/x-www-form-urlencoded" \
-d "client_id=CLIENT_ID \
&client_secret=CLIENT_SECRET \
&code=AUTHORIZATION_CODE \
&grant_type=authorization_code \
&redirect_uri=REDIRECT_URI"
```
- Access API with Token:
```
curl -X GET \
https://resource-server.com/profile \
-H "Authorization: Bearer ACCESS_TOKEN"
```

To conclude, OAuth provides a robust framework for authorizing API access, addressing the shortcomings of sharing credentials, cookies, and API keys. By leveraging OAuth’s capabilities, such as scoped access, refresh tokens, and JWT, we can ensure secure and efficient interactions between users, clients, and resources. Moreover, the extensibility of OAuth with standards like OpenID Connect allows for even broader applications, making it a key technology in modern authentication and authorization infrastructures.

