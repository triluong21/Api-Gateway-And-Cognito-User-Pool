## Setting User Pool Domain Name, Resource servers and App client settings;
On AWS Cognito console:
1. Select "Manage User Pools"
2. Find and Select ApiGatewayAndCognitoUserPool-user-pool
3. Select App integration/Domain Name:
  - Domain prefix: Enter my-test-token
  - Save changes
4. Select App integration/Resource servers:
  - Name: ApiGatewayAndCognitoUserPool
  - Identifier: https://example.com
  - Scopes:
    + Name: api
    + Description: api
  - Save changes 
5. Select App integration/App client settings:
  - Enabled Identity Providers: Select Cognito User Pool
  - Callback URL(s): Enter "https://amazon.com
  - Sign out URL(s): Enter "https://google.com
  - Allowed OAuth Flows: Select Client credentials
  - Allowed Custom Scopes: Check mark on https://example.com/api
  - Save changes

## Setting dev-ApiGatewayAndCognitoUserPool API Gateway OauthAuthorizationScope:
On AWS Amazon API Gateway:
1. Select dev-ApiGatewayAndCognitoUserPool
2. Select Resource
3. Select GET method
4. Select Method Request
5. In OAuth Scopes input text box: 
  - Enter "https://example.com/api, click check mark.
.
6. After setup all methods:
  - Click on Action button
  - Select Deploy API
  - Select dev for Deployment stage
  - Select Deploy button

# Setting up Postman test to retrieve Access Token
Method: POST
URL: https://my-test-token.auth.us-east-2.amazoncognito.com/oauth2/token (Go to Cognito User Pool, select app integration, select Domain name and copy URL and add on /oauth2/token)
Params..: key: grant_type     value: client_credentials
          key: client_id      value: copy/paste client ID from App client 
          key: client_secret  value: copy/past client secret from App client 
Headers.: key: Accept         value: application/json
          key: Content-Type   value: application/x-www-form-urlencoded

# Setting up Postman test to call Lambda using provisioned Access Token
Method: GET
URL:  https://r5ic19chxk.execute-api.us-east-2.amazonaws.com/dev/user/pass (Go to API Gateway console, select the api's stages and copy Invoke URL and add on /user/pass path)
Headers.: key: Content-Type   value: application/json
          key: Authorization  value: copy/paste Access Token from the above test