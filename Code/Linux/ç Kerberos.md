# ç Kerberos
created:: 2022-09-01 10:10
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis 
kind:: #code
status:: #status/seed
language:: [[Linux]]
platform:: [[Crontab]]
***

### After changing your password
If you're renewing your Kerberos authentication after changing your password, you should:
1. Create a new Kerberos keytab
2. Use the "already have a keytab" approach for immediately activating a ticket.

### To create a Kerberos ticket
This creates an authentication ticket that gives you access to hadoop resources for 10 hours.

	kinit ${USER^}@AETH.AETNA.COM

If you already have a keytab created, you should use this:

	kinit ${USER^}@AETH.AETNA.COM -kt ~/${USER}.keytab

### To create a Kerberos keytab
This will essentially create a persistent ticket

	/var/hdpeng/scripts/create_user_keytab.sh

### Using crontab to automatically renew the Kerberos ticket

```bash
crontab -l > ~/$USER.crontab

echo "00 */6 * * * kinit  ${USER^}@AETH.AETNA.COM  -kt ~/$USER.keytab 2>&1 >> $HOME/kinit.log" >> ~/$USER.crontab

crontab ~/$USER.crontab
```

