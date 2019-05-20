# Sensors

- [Get sensor details](#get-sensor-details)
- [Update sensor details](#update-sensor-details)
- [Delete sensor](#delete-sensor)
- [Get sensor channels](#get-sensor-channels)
- [Add channel to sensor](#add-channel-to-sensor)

## Get sensor details

Get the details about a sensor identified by ID.

### Permission
User

### Request

**URL**: `/sensor/{ID}`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/sensor/22
```

### Attributes

#### Required

#### Optional

### Response

#### Successful query

| name   | type   | description |
| ------ | ------ | ----------- |
| **id** | id    | sensor id |
| **site_id** | id    | parent id |
| **name** | string    | sensor name |
| **id_cnr** | string    | cnr sensor id |
| **loc_x** | decimal    | x coordinate in map |
| **loc_y** | decimal    | y coordinate in map |
| **enabled** | boolean    | sensor enable state |
| **status** | string    | sensor status |

```json
{
    "id": 3,
    "site_id": 12,
    "id_cnr": "13061840",
    "name": "Sensore 1",
    "loc_x": 430,
    "loc_y": 240,
    "enabled": true,
    "status": "ok"
}
```

#### Sensor not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find Sensor '4'"
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


## Update sensor details

Update the details about a sensor identified by ID.

### Permission
Admin

### Request

**URL**: `/sensor/{ID}`  
**HTTP method**: PUT

```sh
data='{
    "name": "Doc Sensor2"
}';

curl -X PUT \
     -H "Content-Type: application/json" \
     -d "$data" \
     -H "Token: $TOKEN" \
     ${API_URL}/sensor/15
```

### Attributes

#### Required

#### Optional

| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **name** | string    | sensor name |    old value    |
| **id_cnr** | string    | cnr sensor id |    old value    |
| **loc_x** | decimal    | x coordinate in map |    old value    |
| **loc_y** | decimal    | y coordinate in map |    old value    |
| **enabled** | boolean    | sensor enable state |    old value    |

### Response

#### Successful query
```json
{
    "id": 15,
    "site_id": 23,
    "id_cnr": "04",
    "name": "Doc Sensor2",
    "loc_x": 123,
    "loc_y": 456,
    "enabled": true,
    "status": "ok"
}
```

#### Sensor not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find sensor with id 16"
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


## Delete sensor

Delete the sensor dentified by ID.

### Permission
Admin

### Request

**URL**: `/sensor/{ID}`  
**HTTP method**: DELETE

```sh
curl -X DELETE \
     -H "Token: $TOKEN" \
     ${API_URL}/sensor/15
```

### Attributes

#### Required

#### Optional

### Response

#### Successful query
```json
null
```

#### Sensor not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find sensor 22"
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


## Get sensor channels

Get the list of sensors ids insite a site specified by ID.

### Permission
User

### Request

**URL**: `/sensor/{ID}/channel`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/sensor/15/channel
```

### Attributes

#### Required

#### Optional

### Response

#### Successful query
```json
[
    8,
    11
]
```

#### Site not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find sensor 16"
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


## Add channel to sensor

Add a channel to the sensor specified by ID.

### Permission
Admin

### Request

**URL**: `/sensor/{ID}/channel`  
**HTTP method**: POST

```sh
data='{
    "name": "Doc Temperature Channel",
    "id_cnr": "04",
    "measure_unit": "T""
    "range_min": 20,
    "range_max": 60
}';

curl -X POST \
     -H "Content-Type: application/json" \
     -d "$data" \
     -H "Token: $TOKEN" \
     ${API_URL}/sensor/15/channel
```

### Attributes
#### Required

#### Optional
| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **name** | string    | sensor name |    empty    |
| **id_cnr** | string    | cnr sensor id |    empty    |
| **measure_unit** | string    | measure unit |    empty    |
| **range_min** | decimal    | alarm min value |    empty    |
| **range_max** | boodecimallean    | alarm max value |    empty    |

### Response

#### Successful query
```json
{
    "id": 11,
    "sensor_id": 15,
    "id_cnr": "04",
    "name": "Doc Temperature Channel",
    "measure_unit": "T",
    "range_min": "20",
    "range_max": "60"
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
