### OAuth2 flows
[Cloud Foundry Authorization](https://docs.cloudfoundry.org/api/uaa/version/76.3.0/index.html#overview)  

### OAuth2SAMLBearerAssertion 

```mermaid
sequenceDiagram
    autonumber
	participant client as Destination Service
    participant resource as Resource Server<br>(URL)
	participant oauth as Authorization Server<br>(tokenServiceURL)
    participant IDP as Identity Provider
    client ->> oauth: Registration of OAuth2 client application
    Note over client,oauth: One time configuration event
    oauth ->> client: API key (client_id)
    client ->> IDP: Request SAML Assertion
    IDP ->> client: SAML Assertion
    client ->> oauth: /oauth/token<br>request access token<br>client_id + SAML Assertion
    oauth ->> client: access token (+refresh token)
    loop Data Transfer
        client ->> resource: /odata/v2/... (access token)
        opt Optional
            resource ->> oauth: /oauth/validate<br>validate token
            oauth ->> resource: token validated
        end
        resource ->> client: data
    end
    client ->> oauth: Request a new token<br>refresh token, client_id, ...
    Note over client,oauth: After some time, access token expires
    oauth ->> client: access token (+refresh token)
```
