Pern Stack Tutorials to watch:

https://www.youtube.com/watch?v=5vF0FGfa0RQ
https://www.youtube.com/watch?v=7UQBMb8ZpuE
https://www.youtube.com/watch?v=cjqfF5hyZFg 
https://www.youtube.com/watch?v=sQBA0sq9G0A
https://www.youtube.com/watch?v=_Mun4eOOf2Q
https://www.youtube.com/watch?v=vxu1RrR0vbw

Look up some Bootstrap tutorials to watch so you can add that in here (the classnames are already here)

===

The Azure cloud platform allows you to use any of the Azure databases (as services) or bring your own database. Once your server and database are set up, your existing code will only need to change the connection settings.

When you do use a database on Azure, there are several common tasks you need to accomplish to use the database from your JavaScript app. 


* Azure Database for SQL Server 
* cosmos db
* azure key vault
* azure redis cache
* azure active directory
* portal 
* graph
* azure data factory
* azure data lake
* azure monitor
* azure stream analytics
* Microsoft identity platform

Authentication is the process of proving that you are who you say you are. It's sometimes shortened to AuthN. The Microsoft identity platform uses the OpenID Connect protocol for handling authentication.

Authorization is the act of granting an authenticated party permission to do something. It specifies what data you're allowed to access and what you can do with that data. Authorization is sometimes shortened to AuthZ. The Microsoft identity platform uses the OAuth 2.0 protocol for handling authorization.

Creating apps that each maintain their own username and password information incurs a high administrative burden when adding or removing users across multiple apps. Instead, your apps can delegate that responsibility to a centralized identity provider.

Azure Active Directory (Azure AD) is a centralized identity provider in the cloud. Delegating authentication and authorization to it enables scenarios such as:

Conditional Access policies that require a user to be in a specific location.
The use of multi-factor authentication, which is sometimes called two-factor authentication or 2FA.
Enabling a user to sign in once and then be automatically signed in to all of the web apps that share the same centralized directory. This capability is called single sign-on (SSO).
The Microsoft identity platform simplifies authorization and authentication for application developers by providing identity as a service. It supports industry-standard protocols and open-source libraries for different platforms to help you start coding quickly. It allows developers to build applications that sign in all Microsoft identities, get tokens to call Microsoft Graph, access Microsoft APIs, or access other APIs that developers have built.

When possible, we recommend you use the supported Microsoft Authentication Libraries (MSAL) instead to acquire tokens and call secured web APIs.


===

The {tenant} value in the path of the request can be used to control who can sign into the application. The allowed values are common, organizations, consumers, and tenant identifiers. For more detail, see protocol basics. Critically, for guest scenarios where you sign a user from one tenant into another tenant, you must provide the tenant identifier to correctly sign them into the resource tenant.

* A tenant represents an organization. It's a dedicated instance of Azure AD that an organization or app developer receives at the beginning of a relationship with Microsoft. That relationship could start with signing up for Azure, Microsoft Intune, or Microsoft 365, for example.

===

All confidential clients have a choice of using client secrets (symmetric shared secrets generated by the Microsoft identity platform) and certificate credentials (asymmetric keys uploaded by the developer). For best security, we recommend using certificate credentials. Public clients (native applications and single page apps) must not use secrets or certificates when redeeming an authorization code - always ensure that your redirect URIs correctly indicate the type of application and are unique.

The user will be asked to enter their credentials and complete the authentication. The Microsoft identity platform will also ensure that the user has consented to the permissions indicated in the scope query parameter. If the user has not consented to any of those permissions, it will ask the user to consent to the required permissions. Details of permissions, consent, and multi-tenant apps are provided here.

Once the user authenticates and grants consent, the Microsoft identity platform will return a response to your app at the indicated redirect_uri, using the method specified in the response_mode parameter.

Now that you've acquired an authorization_code and have been granted permission by the user, you can redeem the code for an access_token to the desired resource. Do this by sending a POST request to the /token endpoint:

Now that you've successfully acquired an access_token, you can use the token in requests to web APIs by including it in the Authorization header:

Refresh the access token
Access_tokens are short lived, and you must refresh them after they expire to continue accessing resources. You can do so by submitting another POST request to the /token endpoint, this time providing the refresh_token instead of the code. Refresh tokens are valid for all permissions that your client has already received consent for - thus, a refresh token issued on a request for scope=mail.read can be used to request a new access token for scope=api://contoso.com/api/UseResource.

Refresh tokens for web apps and native apps do not have specified lifetimes. Typically, the lifetimes of refresh tokens are relatively long. However, in some cases, refresh tokens expire, are revoked, or lack sufficient privileges for the desired action. Your application needs to expect and handle errors returned by the token issuance endpoint correctly. Single page apps, however, get a token with a 24-hour lifetime, requiring a new authentication every day. This can be done silently in an iframe when 3rd party cookies are enabled, but must be done in a top-level frame (either full page navigation or a popup) in browsers without 3rd party cookies such as Safari.

Although refresh tokens aren't revoked when used to acquire new access tokens, you are expected to discard the old refresh token. The OAuth 2.0 spec says: "The authorization server MAY issue a new refresh token, in which case the client MUST discard the old refresh token and replace it with the new refresh token. The authorization server MAY revoke the old refresh token after issuing a new refresh token to the client."

===

Learn how to enable authentication for your web app running on Azure App Service and limit access to users in your organization.

App Service provides built-in authentication and authorization support, so you can sign in users and access data by writing minimal or no code in your web app. Using the App Service authentication/authorization module isn't required, but helps simplify authentication and authorization for your app. You can secure your web app with the App Service authentication/authorization module by using Azure Active Directory (Azure AD) as the identity provider.

The authentication/authorization module is enabled and configured through the Azure portal and app settings. No SDKs, specific languages, or changes to application code are required. A variety of identity providers are supported, which includes Azure AD, Microsoft Account, Facebook, Google, and Twitter. When the authentication/authorization module is enabled, every incoming HTTP request passes through it before being handled by app code. 

===

Why use the built-in authentication?
You're not required to use this feature for authentication and authorization. You can use the bundled security features in your web framework of choice, or you can write your own utilities. However, you will need to ensure that your solution stays up to date with the latest security, protocol, and browser updates.

Implementing a secure solution for authentication (signing-in users) and authorization (providing access to secure data) can take significant effort. You must make sure to follow industry best practices and standards, and keep your implementation up to date. The built-in authentication feature for App Service and Azure Functions can save you time and effort by providing out-of-the-box authentication with federated identity providers, allowing you to focus on the rest of your application.

Azure App Service allows you to integrate a variety of auth capabilities into your web app or API without implementing them yourself.
It’s built directly into the platform and doesn’t require any particular language, SDK, security expertise, or even any code to utilize.
You can integrate with multiple login providers. For example, Azure AD, Facebook, Google, Twitter.

===

Access tokens enable clients to securely call protected web APIs, and are used by web APIs to perform authentication and authorization. Per the OAuth specification, access tokens are opaque strings without a set format - some identity providers (IDPs) use GUIDs, others use encrypted blobs. The Microsoft identity platform uses a variety of access token formats depending on the configuration of the API that accepts the token. Custom APIs registered by developers on the Microsoft identity platform can choose from two different formats of JSON Web Tokens (JWTs), called "v1" and "v2", and Microsoft-developed APIs like Microsoft Graph or APIs in Azure have additional proprietary token formats. These proprietary formats might be encrypted tokens, JWTs, or special JWT-like tokens that will not validate.

Clients must treat access tokens as opaque strings because the contents of the token are intended for the resource (the API) only. For validation and debugging purposes only, developers can decode JWTs using a site like jwt.ms. Be aware, however, that the tokens you receive for a Microsoft API might not always be a JWT, and that you can't always decode them.

For details on what's inside the access token, clients should use the token response data that's returned with the access token to your client. When your client requests an access token, the Microsoft identity platform also returns some metadata about the access token for your app's consumption. This information includes the expiry time of the access token and the scopes for which it's valid. This data allows your app to do intelligent caching of access tokens without having to parse the access token itself.

What app is a token "for"?
There are two parties involved in an access token request: the client, who requests the token, and the resource (the API) that accepts the token when the API is called. The aud claim in a token indicates the resource the token is intended for (its audience). Clients use the token but should not understand or attempt to parse it. Resources accept the token.

The Microsoft identity platform supports issuing any token version from any version endpoint - they are not related. This is why a resource setting accessTokenAcceptedVersion to 2 means that a client calling the v1.0 endpoint to get a token for that API will receive a v2.0 access token. Resources always own their tokens (those with their aud claim) and are the only applications that can change their token details. This is why changing the access token optional claims for your client does not change the access token received when a token is requested for user.read, which is owned by the Microsoft Graph resource.

JWTs (JSON Web Tokens) are split into three pieces:

Header - Provides information about how to validate the token including information about the type of token and how it was signed.
Payload - Contains all of the important data about the user or app that is attempting to call your service.
Signature - Is the raw material used to validate the token.
Each piece is separated by a period (.) and separately Base64 encoded.

===

A centralized identity provider is especially useful for apps that have users located around the globe who don't necessarily sign in from the enterprise's network. The Microsoft identity platform authenticates users and provides security tokens, such as access tokens, refresh tokens, and ID tokens. Security tokens allow a client application to access protected resources on a resource server.

Access token: An access token is a security token that's issued by an authorization server as part of an OAuth 2.0 flow. It contains information about the user and the resource for which the token is intended. The information can be used to access web APIs and other protected resources. Access tokens are validated by resources to grant access to a client app. To learn more about how the Microsoft identity platform issues access tokens, see Access tokens.

Refresh token: Because access tokens are valid for only a short period of time, authorization servers will sometimes issue a refresh token at the same time the access token is issued. The client application can then exchange this refresh token for a new access token when needed. To learn more about how the Microsoft identity platform uses refresh tokens to revoke permissions, see Token revocation.

ID token: ID tokens are sent to the client application as part of an OpenID Connect flow. They can be sent alongside or instead of an access token. ID tokens are used by the client to authenticate the user. To learn more about how the Microsoft identity platform issues ID tokens, see ID tokens.

Validate security tokens
It's up to the app for which the token was generated, the web app that signed in the user, or the web API being called to validate the token. The token is signed by the authorization server with a private key. The authorization server publishes the corresponding public key. To validate a token, the app verifies the signature by using the authorization server public key to validate that the signature was created using the private key.

Tokens are valid for only a limited amount of time. Usually, the authorization server provides a pair of tokens, such as:

An access token, which accesses the application or protected resource.
A refresh token, which is used to refresh the access token when the access token is close to expiring.
Access tokens are passed to a web API as the bearer token in the Authorization header. An app can provide a refresh token to the authorization server. If the user access to the app wasn't revoked, it will get back a new access token and a new refresh token. This is how the scenario of someone leaving the enterprise is handled. When the authorization server receives the refresh token, it won't issue another valid access token if the user is no longer authorized.

JSON Web Tokens and claims
The Microsoft identity platform implements security tokens as JSON Web Tokens (JWTs) that contain claims. Since JWTs are used as security tokens, this form of authentication is sometimes called JWT authentication.

A claim provides assertions about one entity, such as a client application or resource owner, to another entity, such as a resource server. A claim might also be referred to as a JWT claim or a JSON Web Token claim.

Claims are name or value pairs that relay facts about the token subject. For example, a claim might contain facts about the security principal that was authenticated by the authorization server. The claims present in a specific token depend on many things, such as the type of token, the type of credential used to authenticate the subject, and the application configuration.

Applications can use claims for various tasks, such as to:

Validate the token.
Identify the token subject's tenant.
Display user information.
Determine the subject's authorization.
A claim consists of key-value pairs that provide information such as the:

Security Token Server that generated the token.
Date when the token was generated.
Subject (such as the user--except for daemons).
Audience, which is the app for which the token was generated.
App (the client) that asked for the token. In the case of web apps, this app might be the same as the audience.


===