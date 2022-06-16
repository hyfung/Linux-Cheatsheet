# Simple Guide To Curl

## Frequently Used Arguments
|Function           |Argument                   |
|-------------------|---------------------------|
|Adding Header      |`--header`                 |
|ASCII Data         |`--data`                   |  
|ASCII Data (w/o @) |`--data-raw "DATA"`        |
|Binary Body        |`--data-binary`            |
|URL Encoded Data   |`--data-urlencode "DATA"`  |
|HTML Formdata      |`--form <name=content>`    |
|Ignore SSL Cert    |`--insecure`               |
|Print Res Headers  |`-i`                       |
|Setting Method     |`-X METHOD`                |

## Basic CRUD

Get
`curl http://localhost`

Put
`curl -X PUT http://localhost`

Post
`curl -X POST http://localhost`

Delete
`curl -X DELETE http://localhost`

## CRUD with custom headers
```bash
curl
-H "Content-type: application/json" \
--data "" \
"http://localhost"
```

## CRUD with payloads
```bash
curl --data "helloworld" "http://localhost"
```

### Post with JSON Body
```bash
curl -X POST \
-H "Content-type: application/json" \
--data-raw '{"key":"value"}' \
"http://localhost"
```
