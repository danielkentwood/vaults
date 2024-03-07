# Change AetnaCVS passwords

##### Metadata
created:: 2023-02-07 08:57
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #aetna 
status:: #status/evergreen 
language:: 
platform::
***

```ad-important
DO NOT change your LDAP and C-ID passwords before changing your network ID password on your local macbook. See [here](https://aetnao365.sharepoint.com/sites/Virtual_Service_Desk/HPSM_Diagnostics/Forms/AllItems.aspx?id=%2Fsites%2FVirtual%5FService%5FDesk%2FHPSM%5FDiagnostics%2FExternal%2FCorp%20Comm%2FMAC%20Computer%20%2D%20Changing%20your%20Password%2Epdf&parent=%2Fsites%2FVirtual%5FService%5FDesk%2FHPSM%5FDiagnostics%2FExternal%2FCorp%20Comm)

```

### Change A-ID (network ID)
1. Change password on mac with the Kerberos SSO Extension
2. Change password on proxy authentication settings (this will pop up automatically at some point)
3. Open CVS Heartbeat on Chrome. When prompted, update the password.
4. Close and re-open OneDrive. Update password.
5. Go to Preferences for Outlook. Accounts. Update password.

### Change LDAP (CVS ID) and C-ID
1. Go to https://mypassword.cvs.com/AIMS/PS/
2. Enter CVS ID 
3. Update both the CVS ID (LDAP) and the C-ID
**4. DO NOT change the password for your network ID (A-ID); do this only through your Mac.**

### Update kerberos
For any edge node that you're working on, run the following: 
```bash
/var/hdpeng/scripts/create_user_keytab.sh
```


### Encrypt password for Kerberos tickets
If you have boa installed, execute the following on your edge node:

> `python ~/boa/boa/crypto.py update_password` then type your new password when prompted  
> If you also updated your CVS cID password, also execute this:  
> `python ~/boa/boa/crypto.py update_password2` then type your new cID password when prompted  
> Source: [boa update password instructions](https://github.aetna.com/analytics-org/boa#updating-old-passwords)

### Update password in proxy settings
Get the URL-encoded password with python:
```python
import urllib.parse

example_pw = '5%69oekjfn12$'
encoded_pw = urllib.parse.quote(example_pw)
print(encoded_pw)
```

Update the password in the following locations on your local computer:
- ~/.config/pip/pip.conf
- ~/.condarc
- ~/.bashrc
- ~/Repos/external/.gitconfig
