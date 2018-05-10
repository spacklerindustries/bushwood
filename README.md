# Readme

## Authenticate
Authenticate will return a token in the response that should be used for all other requests
```
curl -H "Content-Type: application/json" -X POST -d '{"username": "bob", "password": "bob" }' localhost:8080/api/v1/auth
token=$(curl -s -H "Content-Type: application/json" -X POST -d '{"username": "admin", "password": "password"}' 10.1.1.44:8081/api/v1/auth | jq '.token'); token=${token:1:${#token}-2}
```

## List Slots
```
curl -H "Authorization: Bearer $token" -X GET localhost:8080/api/v1/slots
```

## Slot Edit (Options listed below)
```
curl -H "Authorization: Bearer $token" -H "Content-Type: application/json" -X POST -d '{"consoleudev": "1-1.5.1:1.0", "consolebaudrate": "115200"}' localhost:8080/api/v1/slots/3af991a6-9d79-4d70-a1e1-55a5d9182b46
```

### Edit Slot Options
The following can be used to update a slot, one or many
```
{
  "consoleudev": "1-1.5.1:1.0",
  "consoleserver": "http://console.server.local:8001",
  "consolepath": "0cdc7a44-6c13-4788-a8b1-2d13e8bee242",
  "consolebaudrate": "115200",
  "slotname": "Gilmore"
}
```

## Power On Slot
```
curl -H "Authorization: Bearer $token" -X POST localhost:8080/api/v1/slots/1fd44a10-4370-456e-b5f1-ab553abf6e7a/power_on
```

## Power Off Slot
```
curl -H "Authorization: Bearer $token" -X POST localhost:8080/api/v1/slots/1fd44a10-4370-456e-b5f1-ab553abf6e7a/power_off
```

## Caddy Slot Data
The following can be used to update a slot, one or many
This should not be required to use, shouldn't be used except for testing
```
curl -H "Authorization: Bearer $token" -H "Content-Type: application/json" -X POST -d '{"slottype": 15, "powerstatus": 1, "alwayson": 0}' localhost:8080/api/v1/caddydata/i2c/8/slot/1
{
  "slottype": "15",
  "powerstatus": 0,
  "alwayson": 0
}
```

## Register new slot
When a slot comes online, it will register itself via MQTT, but incase it doesn't you can register it manually
```
curl -H "Authorization: Bearer $token" -X POST localhost:8080/api/v1/slots/i2c/8/slot/1
```

## New User
Create a new user
```
curl -H "Authorization: Bearer $token" -H "Content-Type: application/json" -X POST -d '{"username": "bob", "password": "bob" }' localhost:8080/api/v1/users
```

## List users
```
curl -H "Authorization: Bearer $token" -X GET localhost:8080/api/v1/users
```

## List types
```
curl -H "Authorization: Bearer $token" -X GET localhost:8080/api/v1/types
```
