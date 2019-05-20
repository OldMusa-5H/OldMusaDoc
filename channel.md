# Channels

- [Get channel details](#get-channel-details)
- [Update channel details](#update-channel-details)
- [Delete channel](#delete-channel)
- [Get channel readings](#get-channel-readings)

## Get channel details

Get the details about a channel identified by ID.

### Permission
User

### Request

**URL**: `/channel/{ID}`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     ${API_URL}/channel/1
```

### Attributes

#### Required

#### Optional

### Response

#### Successful query

| name   | type   | description |
| ------ | ------ | ----------- |
| **id** | id    | channel id |
| **sensor_id** | id    | sensor id |
| **name** | string    | channel name |
| **id_cnr** | string    | cnr channel id |
| **measure_unit** | string    | measure unit |
| **range_min** | decimal    | alarm min value |
| **range_max** | boodecimallean    | alarm max value |

```json
{
    "id": 1,
    "sensor_id": 3,
    "id_cnr": "11",
    "name": "Temperatura ",
    "measure_unit": "C\u00b0",
    "range_min": "10",
    "range_max": "100"
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


## Update channel details

Update the details about a channel identified by ID.

### Permission
Admin

### Request

**URL**: `/sensor/{ID}`  
**HTTP method**: PUT

```sh
data='{
    "id_cnr": "05",
    "name": "Doc Heat Channel",
    "measure_unit": "F",
    "range_min": "10",
    "range_max": "50"
  }';

curl -X PUT \
     -H "Content-Type: application/json" \
     -d "$data" \
     -H "Token: $TOKEN" \
     ${API_URL}/channel/11
```

### Attributes

#### Required

#### Optional

| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **name** | string    | sensor name |    old value    |
| **id_cnr** | string    | cnr sensor id |    old value    |
| **measure_unit** | string    | measure unit |    old value    |
| **range_min** | decimal    | alarm min value |    old value    |
| **range_max** | boodecimallean    | alarm max value |    old value    |

### Response

#### Successful query
```json
{
    "id": 11,
    "sensor_id": 15,
    "id_cnr": "05",
    "name": "Doc Heat Channel",
    "measure_unit": "F",
    "range_min": "10",
    "range_max": "50"
}
```

#### Channel not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find channel with id 111"
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


## Delete channel

Delete the channel dentified by ID.

### Permission
Admin

### Request

**URL**: `/channel/{ID}`  
**HTTP method**: DELETE

```sh
curl -X DELETE \
     -H "Token: $TOKEN" \
     ${API_URL}/channel/11
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
    "message": "Cannot find Channel '11'"
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


## Get channel readings

Get all of the readings inside a range of two dates, choosing the precision to use.
For now the only precision available is "atomic" (that means that every single measure is returned).

### Permission
User

### Request

**URL**: `/channel/{ID}/readings`  
**HTTP method**: GET

```sh
curl -X GET \
     -H "Token: $TOKEN" \
     "${API_URL}/channel/1/readings?start=2014-03-31T22:00:00.000Z&end=2014-04-01T00:20:00.000Z&precision=atomic"
```

### Attributes

#### Required
| name   | type   | description |
| ------ | ------ | ----------- |
| **start** | date    | start date |
| **end** | date    | end date |
| **precision** | enum    | write atomic |

#### Optional

### Response

#### Successful query
A json array of measure with this format:

| name   | type   | description | default value |
| ------ | ------ | ----------- | ------------- |
| **date** | date    | measure date |    required    |
| **value_min** | decimal    | min reading value |    required    |
| **value_max** | decimal    | max reading value |    empty    |
| **value_avg** | decimal    | avg reading value |    empty    |
| **deviation** | decimal    | reading deviation |    empty    |
| **error** | enum    | reading error |    N    |

```json
[
    {
        "date": "2014-04-01T00:00:00.000000Z",
        "value_min": "19.56",
        "value_avg": "19.56",
        "value_max": "19.56",
        "deviation": "0.0",
        "error": "N"
    },
    {
        "date": "2014-04-01T00:10:00.000000Z",
        "value_min": "19.54",
        "value_avg": "19.55",
        "value_max": "19.56",
        "deviation": "0.01",
        "error": "N"
    },
    {
        "date": "2014-04-01T00:20:00.000000Z",
        "value_min": "19.54",
        "value_avg": "19.55",
        "value_max": "19.56",
        "deviation": "0.01",
        "error": "N"
    }
]
```

#### Site not found
Error type: 404 (Not found)

```json
{
    "message": "Cannot find Channel '111'"
}
```

#### Invalid token

Error code: 401
```json
{
    "message": "Invalid token"
}
```
