# lua-resty-datetime
Thread safe, lazy style, ffi based localtime datetime library.

# Requirements
1. linux 64 bit
2. luajit 2.0 +

# Synopsis
```
local datetime = require"lua.resty.datetime".datetime
local timedelta = require"lua.resty.datetime".timedelta

local a = datetime.new(os.time())
local b = datetime.new(os.date('*t')) 
local c = a + timedelta:new{day=3}
local d = b - timedelta:new{day=4}
print('3 days after  '..tostring(a)..' is '..tostring(c))
print('4 days before '..tostring(b)..' is '..tostring(d))

local n= 0
local s= '1970-01-01 00:00:00'
local t= {year=1970,month=1,day=1}
for i,v in ipairs({n,s,t}) do
   local r = datetime.new(v)
   print(r, r.number)
end
print(datetime.new('1969-1-01 0:02:00')>datetime.new(s))
print(datetime.new('1970-1-1 3:02:0')>datetime.new(s))

```
