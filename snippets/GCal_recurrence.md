# GCal event recurrence
### This is an example method for quickly adding recurrence to existing Google Calendar url invitations, created for Dr Jennifer Polk! 

**Original url**

https://calendar.google.com/calendar/event?action=TEMPLATE&tmeid=MzBtNzNpZWhoYWxzM3B2OWttMGVnanZkZW9fMjAyMzA2MTdUMjAwMDAwWiBqZW5uaWZlci5wb2xrQG0&tmsrc=jennifer.polk%40gmail.com&scp=ALL

**New url**

https://calendar.google.com/calendar/event?action=TEMPLATE&tmeid=MzBtNzNpZWhoYWxzM3B2OWttMGVnanZkZW9fMjAyMzA2MTdUMjAwMDAwWiBqZW5uaWZlci5wb2xrQG0&tmsrc=jennifer.polk%40gmail.com&scp=ALL&recur=RRULE:FREQ=DAILY;UNTIL=20230620

**What has been added?**

The url remains as before, except a 'recur' parameter has been added to the end. This looks as such
`&recur=RRULE:FREQ=DAILY;UNTIL=20230620`. The RRULE parameter follows strict guidelines, which can be found [here](https://datatracker.ietf.org/doc/html/rfc5545#section-3.8.5.3). 

Some of the most simple cases contain `FREQ=DAILY`, `FREQ=WEEKLY`, `FREQ=MONTHLY`. 
Any more complex repeat can also be made, for example "every other month on the second Friday of the month" - see the above link for details which include the `INTERVAL`, `BYDAY`, and `BYMONTHDAY` parameters. 
The `UNTIL` parameter takes a date in YYYYMMDD format, at minimum. A specific time and timezone can be added in **T**HHMMSS**Z** format (eg: "T000000Z", where "Z" indicates the UTC timezone, but it seems this superfluous detail is not required by Google Calendar. 
