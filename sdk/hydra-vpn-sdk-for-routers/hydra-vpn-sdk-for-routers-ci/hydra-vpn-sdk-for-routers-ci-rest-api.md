# REST API CI

Dynamic Configuration Interface based on REST API.

* Supports only synchronous requests
* Can be used from all machines in network

## Configuration

### Minimal working configuration

```text
{
    ...SDK config params...
    "ci_rest" : {
        "token" : "your_secret_token"
    }
}
```

### All configuration parameters

```text
"token"
```

Authorization token used to restrict access.

```text
"host"
```

IP address on which REST API should listen. 

_Default:_ `"127.0.0.1"`

```text
"port"
```

Port to listen on. 

_Default:_ `61438`

```text
"disabled"
```

Handy flag to fast disable dynamic interface not removing `"ci_rest"` configuration section 

_Default:_ `0`

## Response codes

* 500 - internal error. Allocation errors, internal exceptions.
* 200 - success.
* 404 - request unrecognized.
* 400 - bad request. Required request parameters are missing. 
* 413 - request body is too long.

To provide detailed information `"status"` field is also available in [response body](./#responses).

## Requests examples

### Ping. 

```text
<host>:<port>/api/ping
```

_Type:_ `POST` 

_Body:_ `{ "token" : "your_secret_token" }`

### Protect IP address 

```text
<host>:<port>/api/protected_ip
```

_Type:_ `POST` 

_Body:_ `{ "token" : "your_secret_token", "ip_addr" : "192.168.50.149", "country_code" : "ca" }`

### Unprotect IP

```text
<host>:<port>/api/protected_ip
```

_Type:_ `PUT`

_Body:_ `{ "token" : "your_secret_token", "ip_addr" : "192.168.50.149" }`

### Protect MAC

```text
<host>:<port>/api/protected_mac
```

_Type:_ `POST`

_Body:_ `{ "token" : "your_secret_token", "mac_addr" : "08:00:27:aa:d7:17", "country_code" : "ca" }`

### Unprotect MAC

```text
<host>:<port>/api/protected_mac
```

_Type:_ `PUT`

_Body:_ `{ "token" : "your_secret_token", "mac_addr" : "08:00:27:aa:d7:17" }`

### Protect interface

```text
<host>:<port>/api/protected_iface
```

_Type:_ `POST`

_Body:_ `{ "token" : "your_secret_token", "iface" : "eth2", "country_code" : "ca" }`

### Unprotect interface

```text
<host>:<port>/api/protected_iface
```

_Type:_ `PUT`

_Body:_ `{ "token" : "your_secret_token", "iface" : "eth2" }`

### Dump config file

```text
<host>:<port>/api/dump_config
```

_Type:_ `POST`

_Body:_ `{ "token" : "your_secret_token", "config_path" : "/etc/afwrt/afwrt-ci.conf" }`

### Get available countries

```text
<host>:<port>/api/countries
```

_Type:_ `POST`

_Body:_ `{ "token" : "your_secret_token" }`

