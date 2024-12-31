---
Title: Jq
Date: 2024-05-09 19:09
tags:
  - cheatsheet
  - bash
---

| Description                      | Command                               |
| -------------------------------- | ------------------------------------- |
| all                              | `jq .[]`                              |
| first                            | `jq '.[0]'`                           |
| range                            | `jq '.[2:4]'`                         |
| last                             | `jq '.[-2]'`                          |
| last 2                           | `jq '.[-2:]'`                         |
| select array of int by value     | `jq 'map(select(. >= 2))'`            |
| select array of objects by value | `jq '.[] \| select(.id == "second")'` |
|                                  |                                       |
