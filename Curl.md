---
Title: Curl
Date: 15.09.2023
Time: 12:36
tags:
  - cheatsheet
---
| command                                                                        | description                     |
| ------------------------------------------------------------------------------ | ------------------------------- |
| curl -X POST https://example.com                                               | `POST` \| `GET` requests        |
| curl -o output.html https://example.com                                        | save output to file             |
| curl -L                                                                        | Follow redirects                |
| curl -H "Authorization: Bearer TOKEN"                                          | set Headers                     |
| curl -b "session_id=1234"                                                      | set Coockie                     |
| curl -c cookies.txt https://example.com                                        | store Cookie                    |
| curl --connect-timeout 10                                                      | set timeout                     |
| curl -A "Mozilla/5.0"                                                          | set User-Agent                  |
| curl -k                                                                        | ignore ssl certificate          |
| curl -u user:pass                                                              | Basic authentication            |
| curl -X POST -d "name=John&age=30"                                             | Send data in POST request       |
| curl -X POST -H "Content-Type: application/json" -d '{"name":"John","age":30}' | Send json data in POST request  |
| curl -I                                                                        | Return only headers in response |
|                                                                                |                                 |

