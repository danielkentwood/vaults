# ç List all windowed processes and their dimensions
created:: 2022-11-11 09:41
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]], [[Linux]]
platform:: [[Jupyter]]
***

I modified a script (found on Stack Overflow) that shows all running PIDs, the window ID, the window coordinates, and the process name. The code below is meant to be run in Jupyter.

```python
# %pip install pyobjc-framework-Quartz

import Quartz
import pandas as pd

pd.set_option('display.max_columns', 1000)
pd.set_option('display.max_rows', 1000)
pd.set_option('display.float_format', lambda x: '%.3f' % x)

wl = Quartz.CGWindowListCopyWindowInfo( Quartz.kCGWindowListOptionAll, Quartz.kCGNullWindowID)

wl = sorted(wl, key=lambda k: k.valueForKey_('kCGWindowOwnerPID'))

pid_list = []
for i,v in enumerate(wl):
    pid_list.append([
        v.valueForKey_('kCGWindowOwnerPID') or '?',
        v.valueForKey_('kCGWindowNumber') or '?',
        '' if v.valueForKey_('kCGWindowBounds') is None else 
            ( 
                str(int(v.valueForKey_('kCGWindowBounds')
	                .valueForKey_('X'))),
                str(int(v.valueForKey_('kCGWindowBounds')
	                .valueForKey_('Y'))),
                str(int(v.valueForKey_('kCGWindowBounds')
	                .valueForKey_('Width'))),
                str(int(v.valueForKey_('kCGWindowBounds')
	                .valueForKey_('Height'))) 
            ), 
        '[' + (v.valueForKey_('kCGWindowOwnerName') or '') + ']',
        '' if v.valueForKey_('kCGWindowName') is None 
	        else (' ' + v.valueForKey_('kCGWindowName') or '') 
    ])

display(pd.DataFrame(pid_list, columns=['PID','WinID','x,y,w,h','[Title]','Subtitle']))
```

