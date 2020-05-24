---
layout: post
title: Time series analysis - I
date: 2020-04-20
category: machine learning
---

## Generate series of times

```python
import pandas as pd
import numpy as np
```



```python
rng = pd.date_range('2016 Jul 15 10:15', periods = 10, freq = '2Y')
type(rng)
```




    pandas.core.indexes.datetimes.DatetimeIndex



`date_range` creates a series of times. It is an object of type `DateTimeIndex`. 

The individual elements are of type `Timestamp`. In general, an array containing elements of type `Timestamp` is of type `DateTimeIndex`. 

**`Timestamp` --> `DateTimeIndex`**.

`periods` sets the length of the array i.e. the number of `datetime` objects created.

The parameter `freq` determines what is changed to get a new date.

* The default is to increment the date
* If `freq = Y`, year is incremented to create a new date
* If `freq = M`, month is incremented to create a new date
* `freq= D, H, T, S` increment day, hour, minute, and second respectively
* `freq = M` increments month with date set to last day of the month. The start date is changed to last day of the month
* `freq = B` increments days but considers only business days
* `freq = MS` increments month with date set to last day of the month
* `freq = 2D` increments day by 2. Similarly for `Y`, `M`, `H`, `T`, and `S`
* For a complete list of frequency strings, please refer to [offset aliases](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html#timeseries-offset-aliases).


`date_range` can generate `date_time` objects by taking start and end dates.

Suppose that a nurse needs to record the temperature of a patient every 8 hours between the dates July 3 and July 17. How many readings does she take in total?


```python
rng = pd.date_range(start='2020 Jul 15 10:15', end='2020 Jul 25', freq='8H', normalize=True)
rng
```




    DatetimeIndex(['2020-07-15 00:00:00', '2020-07-15 08:00:00',
                   '2020-07-15 16:00:00', '2020-07-16 00:00:00',
                   '2020-07-16 08:00:00', '2020-07-16 16:00:00',
                   '2020-07-17 00:00:00', '2020-07-17 08:00:00',
                   '2020-07-17 16:00:00', '2020-07-18 00:00:00',
                   '2020-07-18 08:00:00', '2020-07-18 16:00:00',
                   '2020-07-19 00:00:00', '2020-07-19 08:00:00',
                   '2020-07-19 16:00:00', '2020-07-20 00:00:00',
                   '2020-07-20 08:00:00', '2020-07-20 16:00:00',
                   '2020-07-21 00:00:00', '2020-07-21 08:00:00',
                   '2020-07-21 16:00:00', '2020-07-22 00:00:00',
                   '2020-07-22 08:00:00', '2020-07-22 16:00:00',
                   '2020-07-23 00:00:00', '2020-07-23 08:00:00',
                   '2020-07-23 16:00:00', '2020-07-24 00:00:00',
                   '2020-07-24 08:00:00', '2020-07-24 16:00:00',
                   '2020-07-25 00:00:00'],
                  dtype='datetime64[ns]', freq='8H')



If the start time is not specified, then the 00:00:00 is taken as the default time.

If `normalize=True`, then time is reset to 00:00:000. In the example above, start time is reset.

Refer to `date_range` documentation for setting complecated frequencies.

## Timestamp

It is Pandas replacement for Python `datetime.datetime` object.

`Timestamp` objects are interchangeable with `datetime.datetime` objects, in most cases.

second can be a decimal with 9 digit accuracy. e.g 59.128769634 is a valid value for second

Refer to documentation for a list of attributes.


```python
pd.Timestamp('2019-04-20 3:41:59.128769634')
t = pd.Timestamp.now()
type(t)
```




    pandas._libs.tslibs.timestamps.Timestamp



## Time offsets


```python
pd.Timedelta('10 day 1H 10T 1S 1 us') # us - microsecond
```




    Timedelta('10 days 01:10:01.000001')



A `Timedelta` object can be added to a `Timestamp` object resulting in a `Timestamp` object.


```python
pd.Timestamp('2016-07-01 8:00') + pd.Timedelta('1.5 hours')
```




    Timestamp('2016-07-01 09:30:00')




```python
rng + pd.Timedelta('1 day')
```




    DatetimeIndex(['2020-07-16 00:00:00', '2020-07-16 08:00:00',
                   '2020-07-16 16:00:00', '2020-07-17 00:00:00',
                   '2020-07-17 08:00:00', '2020-07-17 16:00:00',
                   '2020-07-18 00:00:00', '2020-07-18 08:00:00',
                   '2020-07-18 16:00:00', '2020-07-19 00:00:00',
                   '2020-07-19 08:00:00', '2020-07-19 16:00:00',
                   '2020-07-20 00:00:00', '2020-07-20 08:00:00',
                   '2020-07-20 16:00:00', '2020-07-21 00:00:00',
                   '2020-07-21 08:00:00', '2020-07-21 16:00:00',
                   '2020-07-22 00:00:00', '2020-07-22 08:00:00',
                   '2020-07-22 16:00:00', '2020-07-23 00:00:00',
                   '2020-07-23 08:00:00', '2020-07-23 16:00:00',
                   '2020-07-24 00:00:00', '2020-07-24 08:00:00',
                   '2020-07-24 16:00:00', '2020-07-25 00:00:00',
                   '2020-07-25 08:00:00', '2020-07-25 16:00:00',
                   '2020-07-26 00:00:00'],
                  dtype='datetime64[ns]', freq='8H')



## Time spans

In real life, we deal more with periods of time rather than instances of time. For example, air traffic controllers want to know how many aircrafts land and takeoff between 6 and 9 am on different days of the week. They may not be so much interested in knowing how many aircrafts are taking off and landing at a particular instant. For such requirements, `Timestamp` objects are not useful because they represent instances of time, but not periods of time.

What we need is a `Period` object. As shown below, each `Period` object has a `start_time` and an `end_time`. Since `start_time` and `end_time` are instants of time (not durations), they are of type `Timestamp`.

Note that the `Period` object can represent different time spans like month, day etc. Also notice how start and end times are taken care of automatically.


```python
p1 = pd.Period('7/2020') # Represents a month
p2 = pd.Period('7/21/2020') # Represents a day

print(p1.start_time)
print(p1.end_time)

print(p2.start_time)
print(p2.end_time)
```

    2020-07-01 00:00:00
    2020-07-31 23:59:59.999999999
    2020-07-21 00:00:00
    2020-07-21 23:59:59.999999999


Since `Period` objects represent a duration, as opposed to a specific instant, they can be used to check if a particular instant lies with in a duration.

As an example, let's check if a particualr day lies in the month of July in 2020.


```python
p3 = pd.Timestamp('7/21/2020') # This is an instant of time, not a duration
p1.start_time < p3 < p1.end_time
```




    True



`period_range` creates an object of type `PeriodIndex`. This object contains multiple date time objects of type `Period`.

Date-time series generated by `date_range` represent instances. 

Date-time series generated by `period_range` represent durations. 


```python
p4 = pd.period_range('2020 Apr 20 3:55 pm', freq='H', periods=10)
#print(p4)
type(p4)
print(type(p4[0]))
```

    <class 'pandas._libs.tslibs.period.Period'>


In the example above, we are generating 10 `period` objects starting from the time given. Note that the time has been rolled back to 3 pm from 3:55 pm. This happens because we have set `freq='H'`. In general, when `freq='H'`, time is reset to the beginning of the hour.

To retain the time we have given, we have to set `freq='60T'`.

`p4` is an object of type `PeriodIndex`, while the individual elements are of type `Period`.

In general, an array of objects of type `Period` is of type `PeriodIndex`.

**`Period` --> `PeriodIndex`**

## Indexing a time series with a date_range


```python
num_periods = 40

ts_dt = pd.Series(range(num_periods), pd.date_range('2016 Jul 15 10:15', periods = num_periods, freq = '60T'))
#print(ts_dt.head())
#print(ts_dt.index)
print(type(ts_dt))
print(type(ts_dt.index))
print(type(ts_dt.index[0]))
```

    2016-07-15 10:15:00    0
    2016-07-15 11:15:00    1
    2016-07-15 12:15:00    2
    2016-07-15 13:15:00    3
    2016-07-15 14:15:00    4
    Freq: 60T, dtype: int64
    <class 'pandas.core.series.Series'>
    <class 'pandas.core.indexes.datetimes.DatetimeIndex'>
    <class 'pandas._libs.tslibs.timestamps.Timestamp'>


`ts_dt` is an object of type `Series` - a generic data structure in Pandas

`ts_dt.index` is an object of type `DateTimeIndex`

The individual elements in `ts_dt.index` are of type `Timestamp`

The inividual elements of the series are of type `Timestamp`, but the series is of type `DateTimeIndex`.

## Converting between `DateTimeIndex` and `PeriodIndex`

`DateTimeIndex`: The individual elements of the time series are of type `Timestamp`. They represent specific instances.

`PeriodIndex`: The individual elements are of type `Period`. They represent time spans (durations).

**`Timestamp` --> `DateTimeIndex`**

**`Period` --> `PeriodIndex`**

It is possible to convert from one type of indexing to another.


```python
ts_pd = ts_dt.to_period(freq='60T') # Frequency parameter must be mentioned
ts_pd.head()

#ts_pd = ts_pd.to_timestamp()
```




    2016-07-15 10:15    0
    2016-07-15 11:15    1
    2016-07-15 12:15    2
    2016-07-15 13:15    3
    2016-07-15 14:15    4
    Freq: 60T, dtype: int64



## String indexing

We can search a time series using strings as indices.


```python
ts_dt['2016-07-15 10'] #ts_dt is datetime indexed
```




    2016-07-15 10:15:00    0
    Freq: 60T, dtype: int64




```python
ts_pd['2016-07-15 10'] # ts_pd is period indexed
```




    2016-07-15 10:15    0
    2016-07-15 11:15    1
    Freq: 60T, dtype: int64



Period indexing gives out more results. This is because of overlapping (God knows what it is).


```python
#ts_pd['2016-07-15':'2016-07-16'] # picking up entries for a range of dates
ts_pd['2016-07-15':] # Everything on after July 15
#ts_pd['start':'end']
```




    2016-07-15 10:15     0
    2016-07-15 11:15     1
    2016-07-15 12:15     2
    2016-07-15 13:15     3
    2016-07-15 14:15     4
    2016-07-15 15:15     5
    2016-07-15 16:15     6
    2016-07-15 17:15     7
    2016-07-15 18:15     8
    2016-07-15 19:15     9
    2016-07-15 20:15    10
    2016-07-15 21:15    11
    2016-07-15 22:15    12
    2016-07-15 23:15    13
    2016-07-16 00:15    14
    2016-07-16 01:15    15
    2016-07-16 02:15    16
    2016-07-16 03:15    17
    2016-07-16 04:15    18
    2016-07-16 05:15    19
    2016-07-16 06:15    20
    2016-07-16 07:15    21
    2016-07-16 08:15    22
    2016-07-16 09:15    23
    2016-07-16 10:15    24
    2016-07-16 11:15    25
    2016-07-16 12:15    26
    2016-07-16 13:15    27
    2016-07-16 14:15    28
    2016-07-16 15:15    29
    2016-07-16 16:15    30
    2016-07-16 17:15    31
    2016-07-16 18:15    32
    2016-07-16 19:15    33
    2016-07-16 20:15    34
    2016-07-16 21:15    35
    2016-07-16 22:15    36
    2016-07-16 23:15    37
    2016-07-17 00:15    38
    2016-07-17 01:15    39
    Freq: 60T, dtype: int64



## Creating a `Timestamp` object from a date formatted in European style


```python
eu_date = pd.to_datetime('4/3/2020', dayfirst=True)
print(eu_date)
```

    2020-03-04 00:00:00


## Generating a string representation in a desired format from a `Timestamp` object


```python
eu_date.strftime(format = '%m-%Y-%d') # Returns a string in month-year-day format
```




    '03-2020-04'



## Valid date time formats

'2020 Apr 02', '4/2/2020', '2/4/2020', '2020-04-02'. In cases like '4/2/2020', it is assumed that the first number (4) corresponds to month. Therefore, '4/2/2020' and '2/4/2020' represent two different dates.


## Reference
*Time series analysis tutorial by Aileen Nielsen. YouTube video [here](https://www.youtube.com/watch?v=JNfxr4BQrLk).*
