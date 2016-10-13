# lua-resty-datetime
Thread safe, lazy style, local datetime library

# Environment 
You can use this library under Windows or Linux, OpenResty or non-OpenResty.

# Futures
A datetime object `t` can be described by a readable table `t.table` or a string `t.string` or a number `t.number`(timestamp).
These attributes are lazy which means they're computed when needed, not when initialized.

# Requirements
Same as openresty

# Synopsis
```
local datetime = require"lua.resty.datetime".datetime
local timedelta = require"lua.resty.datetime".timedelta

local function strfmt(t)
  return string.format('%04d-%02d-%02d %02d:%02d:%02d', 
      t.year,  t.month,  t.day, 
      t.hour or 0,  t.min or 0,  t.sec or 0)
end

local now_table = os.date('*t')
local now_number = os.time(now_table)
local now_string = strfmt(now_table)
print('current localtime is', now_string, 'correspondent timestamp is', now_number)
-- create a datetime object in three ways:
local dtt = datetime.new(now_table) 
local dtn = datetime.new(now_number)
local dts = datetime.new(now_string)
assert(dtt==dtn and dtn==dts, 'these three datetime object should be equal')
local diff_days = 2
local diff_hours = 1
-- seconds = 2*24*3600 + 3600 = 176400
local diff = timedelta.new{day=diff_days, hour=diff_hours}
print(string.format('%s days and %s hour after   %s is %s(by table)', diff_days, diff_hours, dtt, dtt+diff))
print(string.format('%s days and %s hour after   %s is %s(by number)', diff_days, diff_hours, dtn, dtn+diff))
print(string.format('%s days and %s hour after   %s is %s(by string)', diff_days, diff_hours, dts, dts+diff))
print(string.format('%s days and %s hour before  %s is %s(by table)', diff_days, diff_hours, dtt, dtt-diff))
print(string.format('%s days and %s hour before  %s is %s(by number)', diff_days, diff_hours, dtn, dtn-diff))
print(string.format('%s days and %s hour before  %s is %s(by string)', diff_days, diff_hours, dts, dts-diff))
local dto = dtt + timedelta.new{hour=1, sec=1}
print(string.format('%s is later   than %s by %s seconds', dto, dtt, (dto - dtt).total_seconds))
local dto = dtt - timedelta.new{hour=1, sec=2}
print(string.format('%s is earlier than %s by %s seconds', dto, dtt, (dtt - dto).total_seconds))

```
