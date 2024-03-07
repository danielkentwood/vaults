# ç Find jupyter server token
title:: ç Find jupyter server token
created:: 2022-10-14 09:50
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[ç Python]]
related:: [[Jupyter]], [[Linux]] 
***

If you get detached from your jupyterlab session and need to find the token, you can just list the currently running jupyter servers:

```bash
jupyter server list
```

This will show you an output like the following:

```
Currently running servers:

http://xhadrevrm7p:23457/?token=5be3ab48ef392fc74e506711a774bec1384d4f9bb2f66741 :: /had/home/a522860

http://xhadrevrm7p:23457/?token=4d00557322a301e21c16c58e282d7717aa4af8e62936d667 :: /had/home/a522860

http://xhadrevrm7p:23456/?token=b2482285a2b1fbe55ff4d092a350427541827a65e22ebc0b :: /had/home/a522860
```

You can just copy the token and give it to the jupyter dialogue that is asking for it.

Or you can copy/paste the entire url (ending with the token itself) into the browser.
