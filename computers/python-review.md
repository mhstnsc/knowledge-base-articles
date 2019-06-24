
### What i did not like
 
* the lack of line terminator makes it cumbersome to break the long lines. if you break a line outside of a `(` `)` block then
gets a `\` suffix but this makes it hard to write things in a flow like this
  ```
  a.map(
      param
   )
   .filter(
      param
   )
   .doSomething(
      param
   )
  ```
  and you have to write
  ```
  a.map(
    param
  ).filter(
    param
  ).doSomething(
    param
  )
  ```
  
* inconsistent access patterns makes it hard to remember how to work with the language.
Sometimes things are part of the syntax, sometimes are object oriented
  * `len(str)` vs `str[10]` vs `str.find`
  * `x in map` vs `map[x]` vs `map.get(x)`
  
* lack of a project file or some manifest makes it hard to enumerate where to find files.
If your files are residing on a top level directory similar to your script then you need to fiddle either with the path or either with PYTHONPATH 
which is then not recognized by the IDEs.
  ```
  library/bla.py
  script/script.py - wants to include bla so i had to change syspath inside script.py to include also library
  ```
  Then packaging with pyinstaller failed because could not find these files
 
* treating string as a subtype of an enumeration sometimes makes things very annoying because works but in unexpected ways. for example doing `",".join(str)` gets a string like `b,r,o,w,n, ,f,o,x`
