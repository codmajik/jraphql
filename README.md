# jraphql
JSON Graph-based Query Language

Using a json structure to provide GraphQL features.

```json5
// int | float | str | enum | $customType
{
    "$schema": {
        "enumStatus": {
            "$type": "enum",
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
        "$scope": "listUsers",
        "$args": {
            "offset": 100,
            "limit": 300
        },
        "$fields": {
            
        }
    },

    "users-28394783423": {
        "$scope": "saveUser",
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
