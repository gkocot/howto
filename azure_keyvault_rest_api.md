# Access secrets in Azure Key Vault with REST API with Postman
## Key Vault API  
https://learn.microsoft.com/en-us/rest/api/keyvault/secrets/get-secret/get-secret?tabs=HTTP  
  
## How to get access to the secrets saved in Azure Key Vault using REST API with POSTMAN  
https://raaviblog.com/how-to-get-access-to-the-secrets-saved-in-azure-key-vault-using-rest-api-with-postman/

## HOWTO (modify the RG, S88493 in examples below)
`elements-keyvault-dev-app` principle is used to authorize access to key vault through REST API.  

Get parameters required to generate authorization token, run:
```
yo lng:upenv S88493-dev-rg
```
and save the following parameters from generated .env file:
```
KEYVAULT_CLIENT_ID
KEYVAULT_CLIENT_SECRET
KEYVAULT_TENANT_ID
```
In Postman create environment variables:
```
tenant_id       <KEYVAULT_TENANT_ID>
client_id       <KEYVAULT_CLIENT_ID>
client_secret   <KEYVAULT_CLIENT_SECRET>
grant_type      client_credentials
resource        https://vault.azure.net
vault_uri       https://s88493-dev-dkv.vault.azure.net
secret_name     aedf5b52-6d5d-4aeb-9af3-6f898ba16ef99cf9d838-e4bb-4a3b-a38c-7985c20b189dPassword
```
The secret name is generally `${customerId}${deviceId}${name}`  
In Postman create global variable `g_access_token`  
Add new request  
GET https://login.microsoftonline.com/{{tenant_id}}/oauth2/token  
with `x-www-form-urlencoded` parameters in the body  
```
clinet_id
client_secret
grant_type
resource
```
Add test script to save `access_token` from the response
```
var data = JSON.parse(responseBody);
postman.setGlobalVariable("a_access_token", data.access_token);
```
Add request to read key vault secret  
GET {{vault_uri}}/secrets/{{secret_name}}/?api-version=2016-10-01
with Authorization header `"Bearer {{g_access_token}}"`

# List keyvault secrets
In azure portal add access policy for s88493-dev-dkv for a user, then execute (may take minutes if there are lots of secrets in the keyvault):
```
az keyvault secret list --id https://s88493-dev-dkv.vault.azure.net
```