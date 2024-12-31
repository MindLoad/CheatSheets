---
Title: Pytz
Date: 01.09.2023
Time: 18:21
Tags: [cheatsheet]
---
## Cheat Sheet

| COMMAND                                                 | DESCRIPTION                                |
| ------------------------------------------------------- | ------------------------------------------ |
| `utc = pytz.utc`                                          | retrieve UTC timezone                      |
| `tz_kiev = pytz.timezone('Europe/Kiev')`                  | retrieve Kiev timezone                     |
| `kiev_time = datetime.now(tz_kiev)`                       | retrieve Kiev time                          |
| `utc_date = utc.localize(datetime(2023, 9, 1, 12, 35))`   | set UTC `datetime` 12:35                     |
| `convert_kiev = utc_date.astimezone(tz_kiev)`             | convert previous date due to Kiev timezone |
| `offset = divmod(convert_kiev.utcoffset().seconds, 3600)` | time offset due to UTC in hours            |
| `convert_kiev.tzname()`                                   | Timezone info                              |
|                                                         |                                            |

## Time slots & Intersection

```python
import pytz
from datetime import datetime
tz = pytz.timezone('Etc/UTC')
slot1_s = tz.localize(datetime(2023, 2, 9, 0, 30))
slot1_e = tz.localize(datetime(2023, 2, 9, 1, 30))
slot2_s = tz.localize(datetime(2023, 2, 9, 1, 0))
slot2_e = tz.localize(datetime(2023, 2, 9, 2, 0))
if slot1_s <= slot2_e and slot1_e >= slot2_s:
	intersection_start = max(slot1_s, slot2_s)
	intersection_end = min(slot1_e, slot2_e)
	return f'Intersection: {intersection_start} to {intersection_end}'
return None
```
