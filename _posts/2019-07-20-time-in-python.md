---
layout: post
title: Time in Python
date: 2019-07-20
category: programming
---
Python's `datetime` module provides the necessary tools to process
information related to time. Specifically, the module supplies classes for
manipulating dates and times. Given below are a few examples.

<br />
### To find current local time 
`datetime.now()` is a classmethod that returns current local time. We first
have to import `datetime` module because `datetime.now()` is part of it.

We can get time information in another format by using the `timetuple()`
method. `timetuple()` provides year, month, day, hour, second, weekday,
yearday, and information on daylight saving. 

```python
import datetime   # module for manipulating times and dates

Now = datetime.datetime.now() # returns local current date and time

Now   # year, month, date, hour, minute, second, microsecond
print(Now) # Neatly formatted output
print(Now.year)
print(Now.second)
print(Now.microsecond)

Now.timetuple()
year, month, day,  hour, minute, second, weekday, yearday, dst = Now.timetuple()
# dst = 1 means daylight saving is on
# dst = 0 means daylight saving is not on
#dst = -1 means daylight saving info is not available 
```

`datetime` contains the following classes and classmethods

* `timedelta` 
* `date`
  * `fromtimestamp`
  * `today`
  * `fromordinal` 
  * `fromisoformat`
* `tzinfo`
* `time`
  * `fromisoformat`
* `datetime`
  * `fromtimestamp` 
  * `utcfromtimestamp`
  * `now`
  * `utcnow`
  * `combine`
  * `fromisoformat`
  * `strptime` 
* `timezone`
