
### Enable duplex printing on postscript driver
  * To enable duplex, select the Generic PS printer in Printers & Scanners, 
  * click on `Options & Supplies` and then 
  * select the `Options` tab. 
  * Here you can enable the `Duplex unit`.

### Raise a window using the keyboard

  * Create following script in `automator` and remember its `name`
```
on run {input, parameters}
   tell application "iTerm" to activate
   return input
end run
```
  * Open Settings -> Keyboard -> Keyboard Shortcuts -> Services -> General and the newly created script should be there and assign a shortcut
  * Open Settings -> Privacy -> Accessibility  and add `Automator` as app allowed to control the computer
