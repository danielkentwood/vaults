# ç Find top providers by NSA
created:: 2022-07-27 10:42
modified:: <%+ tp.file.last_modified_date() %>
mode: #mode/praxis, #Aetna/data
kind:: #code
status:: #status/seed
language:: [[SQL]]
platform::
***

# Find top providers by Network Service Area

```sql
-- Top Providers by NSA
--This query ranks top providers by paid amount for each network service area, using the DENSE_RANK function.

SELECT T1.*
FROM (
	SELECT 
		CL.NTWK_SRV_AREA_ID,
		PD.SRC_PRVDR_ID,
		PD.PRINT_NM,
		SUM(CL.ADMIT_CNT) AS ADMIT_CNT,
		SUM(CL.DAYS_CNT) AS DAYS_CNT,
		SUM(CL.PAID_AMT) AS PAID_AMT,
		DENSE_RANK() OVER(
			PARTITION BY CL.NTWK_SRV_AREA_ID 
			ORDER BY SUM(CL.PAID_AMT) DESC
		) AS PROVIDER_RANK
	FROM
		IWH.MEDICAL_CLAIM_LINE CL,
		IWH.PROVIDER_DM PD
	WHERE 1=1
		AND CL.PAID_PRVDR_ID = PD.PROVIDER_ID
		AND CL.FUND_ARRNGMT_CD='01' 
		AND CL.PLC_SRV_CD='I' 
		AND PD.PROVIDER_TYPE_CD IN ('HO') 
		AND CL.SRV_START_DT BETWEEN '2001-01-01' AND '2001-01-31' 
		AND CL.SUMMARIZED_SRV_IND='Y' 
		AND CL.CLM_LN_STATUS_CD='P' 
		AND CL.NTWK_SRV_AREA_ID In ('NJ01','GN02')
	GROUP BY
		CL.NTWK_SRV_AREA_ID,
		PD.PROVIDER_TYPE_CD,
		PD.SRC_PRVDR_ID,
		PD.PRINT_NM
) AS T1
WHERE
  T1.PROVIDER_RANK <=5;
```

