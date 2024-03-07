# ç Get current channel permissions coverage
created:: 2022-07-06 13:54
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis, #Aetna/data  
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform:: [[CPL]]
***


```sql
WITH member_permissions AS (
	SELECT
		individual_id,
		max(if(trim(channel) = 'ivr',
			int(permissions_flag), -- TRUE = 1, FALSE = 0
			NULL)) AS ivr_permissions,
		max(if(trim(channel) = 'allied_dm',
			int(permissions_flag), -- TRUE = 1, FALSE = 0
			NULL)) AS dm_permissions,
		max(if(trim(channel) = 'email',
			int(permissions_flag), -- TRUE = 1, FALSE = 0
			NULL)) AS email_permissions,
		max(if(trim(channel) = 'sms',
			int(permissions_flag), -- TRUE = 1, FALSE = 0
			NULL)) AS sms_permissions,
		max(if(trim(channel) = 'push_braze',
			int(permissions_flag), -- TRUE = 1, FALSE = 0
			NULL)) AS push_braze_permissions,
		max(if(trim(channel) = 'pull_web',
			int(permissions_flag), -- TRUE = 1, FALSE = 0
			NULL)) AS pull_web_permissions,
		max(if(trim(channel) = 'pull_mobile',
			int(permissions_flag), -- TRUE = 1, FALSE = 0
			NULL)) AS pull_mobile_permissions,
		max(if(trim(channel) = 'arna',
			int(permissions_flag), -- TRUE = 1, FALSE = 0
			NULL)) AS arna_permissions,
		max(if(trim(channel) = 'sfsc_call_pod',
			int(permissions_flag), -- TRUE = 1, FALSE = 0
			NULL)) AS sfsc_call_pod_permissions
	FROM prod_nba_enc.cpl_program_permissions_eligibility
	WHERE 1=1
		AND program_id IN (0)
		AND channel IN (
			'ivr', 'allied_dm', 'email', 'sms', 'push_braze', 'pull_web',
			'pull_mobile', 'arna', 'sfsc_call_pod'
		)
	GROUP BY individual_id
)
SELECT
	count(*) AS n_rows,
	count(DISTINCT individual_id) AS distinct_id_cnt,
	round(sum(ivr_permissions) / count(*), 4) AS ivr,
	round(sum(dm_permissions) / count(*), 4) AS dm,
	round(sum(email_permissions) / count(*), 4) AS email,
	round(sum(sms_permissions) / count(*), 4) AS sms,
	round(sum(pull_web_permissions) / count(*), 4) AS pull_web,
	round(sum(push_braze_permissions) / count(*), 4) AS push_braze,
	round(sum(pull_mobile_permissions) / count(*), 4) AS pull_mobile,
	round(sum(arna_permissions) / count(*), 4) AS arna,
	round(sum(sfsc_call_pod_permissions) / count(*), 4) AS sfsc_call_pod,
	round((count(*) - count(ivr_permissions)) / count(*), 4) AS missing
FROM member_permissions;
```

| ivr | dm | email | sms | pull<br>web | push<br>braze | pull<br>mobile | arna | call<br>pod | 
| --- | --- | --- | --- | --- | ---| --- | --- | --- | 
| 0.77 | 0.81 | 0.46 | 0.44 | 0.88 | 0.04 | 0.07 | 0.80 | 0.70 | 





