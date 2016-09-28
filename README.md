# lua-resty-datetime
Thread safe, ffi based datetime library.

# Synopsis
```
local datetime = require"lua.resty.datetime".datetime
local timedelta = require"lua.resty.datetime".timedelta

-- create from string
local x = datetime.new('2016-01-01 00:01:00') 

-- create from number from os.time
local y = datetime.new(os.time())

-- create from table from os.date
local b = datetime.new(os.date('*t'))

-- two days after now
local a = b + timedelta:new{day=2}

print(b)
print('after two days:',a)
print()
-- n, s, t are the same
local n=3600
local s='1970-01-01 01:00:00'
local t={year=1970,month=1,day=1,hour=1}
for i,v in ipairs({n,s,t}) do
   local r = datetime.new(v)
   print(r)
   print(r.number)
   print(r + timedelta:new{day=3})
   print(r - timedelta:new{day=3})
end

-- comparison
print(datetime.new('1970-1-01 0:02:00')>datetime.new(s))
print(datetime.new('1970-1-1 3:2:0')>datetime.new(s))

```