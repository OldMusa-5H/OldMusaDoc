# Users

- [Get current user](#get-current-user)
- [Get user list](#get-user-list)
- [Get user details](#get-user-details)
- [Add user](#add-user)
- [Update user details](#update-user-details)
- [Delete user](#delete-user)
- [Get user access list](#get-user-access-list)
- [Add user access](#add-user-access)
- [Remove user access](#remove-user-access)
- [Add FCM token](#add-fcm-token)
- [Delete FCM token](#delete-fcm-token)

## Get current user

Get the current user.

### Permission
Login needed, both users and admins can perform this operation

### Request

**URL**: `/user_me`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/user_me
```

### Attributes
#### Required
none

#### Optional
none

### Response

#### Successful response
```json
{
    "id": 1,
    "username": "root",
    "permission": "A"
}
```

| name   | type   | description     |
| ------ | ------ | --------------- |
| **id** | int    | User global id |
| **username** | string | Username |
| **permission** | enum | User or Admin |

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Get user list

Get the global user list.

### Permission
Admin

### Request

**URL**: `/user`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/user
```

### Attributes
#### Required
none

#### Optional
none

### Response

#### Successful query
```json
[
    1, 3, 15
]
```

#### Insufficient permission
Error type: 401 (Unauthorized)

```json
{
    "message": "Insufficient permission"
}
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Get user details

Request the details of the user speficied by ID.

### Permission
Admin unless the ID is your own

### Request

**URL**: `/user/{ID}`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/user/1
```

### Attributes

#### Required
none

#### Optional
none

### Response

#### Successful query
```json
{
    "id": 1,
    "username": "root",
    "permission": "A"
}
```


#### User not found

```json
{
    "message": "Cannot find User '10'"
}
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```

#### Insufficient permission
Error type: 401 (Unauthorized)

```json
{
    "message": "Insufficient permission"
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Add user

Create an user

### Permission
Admin

### Request

**URL**: `/user`  
**HTTP method**: POST

```sh
data='{
    "username": "groot",
    "password": "iamgroot",
    "permission": "U"
}';

curl -X POST \
     -H "Content-Type: application/json" \
     -d "$data" \
     -H "Token: $TOKEN" \
     ${API_URL}/user
```

### Attributes

#### Required

URL parameters:  

| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **username** | string    | user's username |           |
| **password** | string    | user's password |           |

#### Optional

| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **permission** | enum    | user's permission |  U  |

### Response

#### Successful creation
```json
{
    "id": 2,
    "username": "iamgroot",
    "permission": "U"
}
```

#### Username already in use

Error code: 404
```json
{
    "message": "Username already in use"
}
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```

#### Invalid arguments

Error code: 400
The message will vary

#### Insufficient permission
Error type: 401 (Unauthorized)

```json
{
    "message": "Insufficient permission"
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Update user details

Change the details of an user identified by ID.

### Permission
Normal users can only change their passwords,
Admin users don't have this restriction, they can change any details of any
user.

### Request

**URL**: `/user/{ID}`  
**HTTP method**: PUT

```sh
data='{
    "username": "groot",
    "password": "thanosaccess",
    "permission": "A"
}';

curl -X PUT \
     -H "Content-Type: application/json" \
     -d "$data" \
     -H "Token: $TOKEN" \
     ${API_URL}/user/2
```

### Attributes

#### Required

URL parameters:  

| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **username** | string    | username |  (old value) |
| **password** | string    | new password | (old value)  |

#### Optional

| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **permission** | enum    | user's permission |  (old value)  |

### Response

#### Successful creation
```json
{
    "id": 2,
    "username": "groot",
    "permission": "A"
}
```

#### Username already in use

Error code: 404
```json
{
    "message": "Username already in use"
}
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```

#### Invalid arguments

Error code: 400
The message will vary

#### Insufficient permission
Error type: 401 (Unauthorized)

```json
{
    "message": "Insufficient permission"
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Delete user

Delete a single user specified by ID. (that user cannot be yourself)

### Permission
Admin

### Request

**URL**: `/user/{ID}`  
**HTTP method**: DELETE

```sh
curl -X DELETE \
     -H "Token: $TOKEN" \
     ${API_URL}/user/3
```

### Attributes

#### Required
none

#### Optional
none

### Response

#### Successful creation
```json
null
```

#### Username already in use

Error code: 404
```json
{
    "message": "Cannot find user 3"
}
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```

#### Insufficient permission
Error type: 401 (Unauthorized)

```json
{
    "message": "Insufficient permission"
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Get user access list

Get the list of sites an user can access, ID indicates the id of the user to check.

### Permission
Admin

### Request

**URL**: `/user/{ID}/access`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/user/3/access
```

### Attributes

#### Required
none

#### Optional
none

### Response
A json list representing the site ids.

#### Successful query
```json
[
    4, 6, 7
]
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```

#### Insufficient permission
Error type: 401 (Unauthorized)

```json
{
    "message": "Insufficient permission"
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Add user access

Add a site to the user's access list, ID indicates the id of the user.

### Permission
Admin

### Request

**URL**: `/user/{ID}/access`  
**HTTP method**: POST

```sh
data='{
    "id": 11
}';

curl -X POST \
     -H "Content-Type: application/json" \
     -d "$data" \
     -H "Token: $TOKEN" \
     ${API_URL}/user/3/access
```

### Attributes

#### Required
none

#### Optional
none

### Response

#### Successful query
```json
null
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```

#### Insufficient permission
Error type: 401 (Unauthorized)

```json
{
    "message": "Insufficient permission"
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Remove user access

Remove a site from the user's access list, UID indicates the id of the user while SID specifies the ID of the site to remove from the access list.

### Permission
Admin

### Request

**URL**: `/user/{UID}/access/{SID}`  
**HTTP method**: DELETE

```sh
curl -X DELETE \
     -H "Token: $TOKEN" \
     ${API_URL}/user/3/access/11
```

### Attributes

#### Required
none

#### Optional
none

### Response

#### Successful query
```json
null
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```

#### Insufficient permission
Error type: 401 (Unauthorized)

```json
{
    "message": "Insufficient permission"
}
```

#### Access not found
Error type: 404 (Not Found)
```json
{
    "message": "Cannot find entry ('3', '12')"
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Add FCM token

Add an FCM token for contact to the user identified by UID.

### Permission
Admin unless the ID is your own

### Request

**URL**: `/user/{UID}/contact/fcm/{TOKEN}`  
**HTTP method**: PUT

```sh
curl -X PUT \
     -H "Token: $TOKEN" \
     ${API_URL}/user/3/contact/fcm/lusdhfiusgluop1827g4
```

### Attributes

#### Required
none

#### Optional
none

### Response

#### Successful query
```json
null
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```

#### Insufficient permission
Error type: 401 (Unauthorized)

```json
{
    "message": "Insufficient permission"
}
```

- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Delete FCM token

Remove an FCM token for contact to the user identified by UID.

### Permission
Admin unless the ID is your own

### Request

**URL**: `/user/{UID}/contact/fcm/{TOKEN}`
**HTTP method**: DELETE

```sh
curl -X DELETE \
     -H "Token: $TOKEN" \
     ${API_URL}/user/3/contact/fcm/lusdhfiusgluop1827g4
```

### Attributes

#### Required
none

#### Optional
none

### Response

#### Successful query
```json
null
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```

#### Insufficient permission
Error type: 401 (Unauthorized)

```json
{
    "message": "Insufficient permission"
}
```
