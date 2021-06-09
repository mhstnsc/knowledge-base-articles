
## Syntax

* `[x for x in collection]`
* `str[begin:end]` - select from string a string (probably also collection)

## Date time

* String to date-time object
  ``` 
  from datetime import datetime
  a = datetime.strptime('30/03/09 16:31:32.123', '%d/%m/%y %H:%M:%S.%f')
  a.microsecond
  ```

## Printing stuff

* `"%-6s" % name` -  Indent left with fixed overall space

## Libraries
 * tatsu (ebnf grammar parsing) - nice experience with it, can match by power of regexp (even with lookahead) and then can manipulate the syntax tree
 * tenacity - retry library (not used) - https://github.com/jd/tenacity
 

