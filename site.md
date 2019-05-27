# Sites

- [Get visible site list](#get-visible-site-list)
- [Add site](#add-site)
- [Get site details](#get-site-details)
- [Update site details](#update-site-details)
- [Delete site](#delete-site)
- [Get site sensors](#get-site-sensors)
- [Add sensor to site](#add-sensor-to-site)
- [Get site map](#get-site-map)
- [Change site map](#change-site-map)
- [Delete site map](#delete-site-map)

## Get visible site list

Get the list of sites visible to the current user.
If the user is an admin it will always be the global site list,
otherwise the list will be the access list of the user.

### Permission
Login needed, both users and admins can perform this operation

### Request

**URL**: `/site`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/site
```

### Attributes
#### Required
none

#### Optional
none

### Response
A json list of the available sites

#### Successful response
```json
[
    12,
    13,
    14
]
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```


- - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -


## Add site

Add a site to the global list

### Permission
Admin

### Request

**URL**: `/site`  
**HTTP method**: POST

```sh
data='{
    "name": "Doc Site",
    "id_cnr": "DS-XL"
}';


curl -X POST \
     -H "Content-Type: application/json" \
     -d "$data" \
     -H "Token: $TOKEN" \
     ${API_URL}/site
```

### Attributes
#### Required
| name   | type   | description |
| ------ | ------ | ----------- |
| **name** | string    | site name |

#### Optional
| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **id_cnr** | string    | cnr site id |    empty    |

### Response

#### Successful query
```json
{
    "id": 22,
    "name": "Doc Site",
    "id_cnr": "DS-XL"
}
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


## Get site details

Get the details about a site identified by ID.

### Permission
User

### Request

**URL**: `/site/{ID}`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/site/22
```

### Attributes

#### Required

#### Optional

| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **name** | string    | site id |  (old value) |
| **id_cnr** | string    | site cnr id | (old value)  |

### Response

#### Successful query
```json
{
    "id": 22,
    "name": "Doc Site",
    "id_cnr": "DS-XL"
}
```

#### Site not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find site 22"
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


## Update site details

Update the details about a site identified by ID.

### Permission
Admin

### Request

**URL**: `/site/{ID}`  
**HTTP method**: PUT

```sh
data='{
    "name": "Doc Site2",
    "id_cnr": "DS-XL2"
}';

curl -X PUT \
     -H "Content-Type: application/json" \
     -d "$data" \
     -H "Token: $TOKEN" \
     ${API_URL}/site/22
```

### Attributes

#### Required

#### Optional

### Response

#### Successful query
```json
{
    "id": 22,
    "name": "Doc Site2",
    "id_cnr": "DS-XL2"
}
```

#### Site not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find site 22"
}
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


## Delete site

Delete the site dentified by ID.

### Permission
Admin

### Request

**URL**: `/site/{ID}`  
**HTTP method**: DELETE

```sh
curl -X DELETE \
     -H "Token: $TOKEN" \
     ${API_URL}/site/22
```

### Attributes

#### Required

#### Optional

### Response

#### Successful query
```json
null
```

#### Site not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find site 22"
}
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


## Get site sensors

Get the list of sensors ids insite a site specified by ID.

### Permission
User

### Request

**URL**: `/site/{ID}/sensor`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/site/22/sensor
```

### Attributes

#### Required

#### Optional

### Response

#### Successful query
```json
[
    3,
    5,
    14
]
```

#### Site not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find site 22"
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


## Add sensor to site

Add a sensor to the site specified by ID.

### Permission
Admin

### Request

**URL**: `/site/{ID}/sensor`  
**HTTP method**: POST

```sh
data='{
    "name": "Doc Sensor",
    "id_cnr": "04",
    "loc_x": 123
    "loc_y": 456,
    "enabled": true
}';

curl -X POST \
     -H "Content-Type: application/json" \
     -d "$data" \
     -H "Token: $TOKEN" \
     ${API_URL}/site/23/sensor
```

### Attributes
#### Required

#### Optional
| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **name** | string    | sensor name |    empty    |
| **id_cnr** | string    | cnr sensor id |    empty    |
| **loc_x** | decimal    | x coordinate in map |    empty    |
| **loc_y** | decimal    | y coordinate in map |    empty    |
| **enabled** | boolean    | sensor enable state |    false    |

### Response

#### Successful query
```json
{
    "id": 15,
    "site_id": 23,
    "id_cnr": "04",
    "name": "Doc Sensor",
    "loc_x": 123,
    "loc_y": 456,
    "enabled": true,
    "status": "ok"
}
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


## Get site map

Get the image map of the site (if one is set) in bytes.

### Permission
User

### Request

**URL**: `/site/{ID}/map`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/site/22/map
```

### Attributes

#### Required

#### Optional

### Response

#### Successful query
image binary data

#### Site not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find site 22"
}
```

#### No map in site
Error type: 404 (Not found)

```json
{
    "message": "No map image found"
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


## Change site map

Replace or create the map of the site identified by ID.
You can also reposition the sensors inside the site by specifying the image size (and the old one's too).

### Permission
Admin

### Request

**URL**: `/site/{ID}/map`  
**HTTP method**: PUT

```sh
data='binary image data';

curl -X PUT \
     -H "Content-Type: image/png" \
     -d "$data" \
     -H "Token: $TOKEN" \
     "${API_URL}/site/22/map?resize_from_w=1920&resize_from_h=1080&resize_to_w=640&resize_to_h=480"
```

### Attributes

#### Required

#### Optional

| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **resize_from_w** | decimal    | old image width |    none    |
| **resize_from_h** | decimal    | old image height |    none    |
| **resize_to_w** | decimal    | new image width |    none    |
| **resize_to_h** | decimal    | new image height |    none    |

### Response

#### Successful query
```json
null
```

#### Site not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find site 22"
}
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


## Delete site map

Delete the map of the site identified by ID.

### Permission
Admin

### Request

**URL**: `/site/{ID}/map`  
**HTTP method**: DELETE

```sh
curl -X DELETE \
     -H "Token: $TOKEN" \
     "${API_URL}/site/22/map"
```

### Attributes

#### Required

#### Optional

### Response

#### Successful query
```json
null
```

#### Site not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find site 22"
}
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
