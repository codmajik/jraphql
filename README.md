# jraphql
JSON Graph-based Query Language

Using a json structure to provide GraphQL features.

```json5
//TYPES: int | float | str | enum | object | $customType
{
    "$schema": {
        "enumStatus": {
            "$type": "enum", // if amited assume object
            "$values": [
                {"name":"active", "value": "A"},
                {"name":"suspended", "value":"I"},
                {"mame":"deleted", "value": "D"}
            ]
        },
        "userInfo": {
            "id": {
               "$type": "int!",
               "readonly": true
            },
            "firstName": "str!",
            "lastName": "str",
            "address": "$addressInfo",
            "status": "$enumStatus"
        },
        "addressInfo": {
            "streetName": "str!",
            "houseNo": "str"
        }
    },

    "$query": {
        "listUsers": { 
            "@return": {
                "arrayOf": "$userInfo"
            },
            "@args": {
                "offset": "int",
                "limit": "int"
            }
        },
        "searchUsers": {
            "@return": { 
                "arrayOf": "$userInfo" 
            },
            "@args": { 
                "name": "str!" 
            }
        },

        "saveUser": {
            "@mutation": true,
            "@return": "$userInfo",
            "@args": "$userInfo"
        }
    }
}
```

#### query and muation
```json5
{
    "users-list-1083746374": {
        "$query": "listUsers",
        "$args": {
            "offset": 100,
            "limit": 300
        },
        "$fields": {
            
        }
    },

    "users-28394783423": {
        "$query": "saveUser",
        "$args": {
          "id": 9349384, // this would cause it to fail -- would be marked as readonly
          "firstName": "John",
          "lastName": "Doe",
          "address": {
            "streetName": "21 Klaana St. Ako Adei Osu. Accra Ghana"
          }
        }
    }
}
```


##### TODO
Write actual spec.
