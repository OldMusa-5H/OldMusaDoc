# Tokens

- [Obtain token](#obtain-token)

## Obtain token

Obtain a login token

### Request

**URL**: `/token`  
**HTTP method**: POST | GET

```sh
data='{
    "username": "root",
    "password": "password"
}';

curl -X POST \
     -H "Content-Type: application/json" \
     -d "$data" \
     ${API_URL}/token
```

### Attributes
#### Required
username and password

| name              | type   | description | default value |
| ----------------- | ------ | ----------- | ------------- |
| **username**  | string | account username | |
| **password**     | string | account password | |

#### Optional
none


### Response

#### Successful creation
The token will be expressed as an ascii string
```json
{
    "token": "eyJhbGciOiJIUzUxMiJ9.eyJpZCI6MSwiZGF0ZSI6MTU1Nzg1MDQ5OH0.VtZE2cpxuzEjrqqhzieMIzODRr7ptHUrI4yoHl1EncSmTuaNRA45fnBeu-hyyljATzM9vJhrwCCBSQRnsoElWA"
}
```

#### Wrong credentials
Http code: 404
```json
{
    "message": "Wrong username or password"
}
```

#### Missing parameters
Http code: 400
```json
{
    "message": {
        "password": "Missing required parameter in the JSON body or the post body or the query string"
    }
}
```
