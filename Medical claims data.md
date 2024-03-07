# Medical claims data

parent:: [[AI-DS-ML in Healthcare]]

ICD Code training:

- [https://icd.who.int/training/icd10training/ICD-10%20training/Start/index.html](https://icd.who.int/training/icd10training/ICD-10%20training/Start/index.html)

Example of using claims data for EDA

- [https://github.com/NYU-CS6313-Projects/Medicare-Claims-Cost-Analysis](https://github.com/NYU-CS6313-Projects/Medicare-Claims-Cost-Analysis)
- [https://www.cms.gov/Research-Statistics-Data-and-Systems/Downloadable-Public-Use-Files/SynPUFs/DE_Syn_PUF](https://www.cms.gov/Research-Statistics-Data-and-Systems/Downloadable-Public-Use-Files/SynPUFs/DE_Syn_PUF)

**Medical claims include institutional and professional services:**

- Included in APCD:
    - hospital inpatient stays and outpatient visits
    - doctor office visits
    - fee-for-service and capitated payment claims (capitation payments are monthly per-capita payments from the insurance provider to the medical provider based on the number of patients the medical provider has on the insurance provider's plan)
- Excluded in APCD:
    - dental claims
    - prescription drug claims
    - fully-denied claims

**Claim versioning**

- re-adjudication: review results in decision that incorrect amount was paid on a claim
    - prior paid amounts are zeroed-out and new amount is entered into data
    - this causes APCD to contain multiple versions of same claim
    - APCD contains a "highest version" (most recent version) indicator field that prevents double counting.

**Medical Data Codes**

- ICD Codes: diagnosis data using International Classification of Disease methodology.
- E-Codes: Codes that identify external injuries
- Revenue Codes: Describe medical goods and services
- Procedure Codes (CPT): Identify medical procedures performed
- Diagnostic Related Group (DRG) Code: Classify claims into groups based on the type of service the patient received
    - These classify hospital visits into related groups.
        - e.g., all claims related to a heart attack would have a single DRG
    - Used by analysts to analyze episodes of care

**Member eligibility data**

- Member must be enrolled in a health insurance product before the insurance org will pay the member's providers for that member's claims.
    - Every enrollment record can be mapped to a single product (plan) record.
    - Every medical and pharmacy claim can be mapped to a single enrollment record.
    - Therefore, claims can be mapped to the member's active PCP.
- Why do we need member eligibility data?
    - Member eligibility data is the key to linking claims, products, and PCPs.

**Product Data**

- Product is a set of benefits sold by health insurance org.
    - deductibles
    - co-pay
    - coinsurance
    - network of doctors
    - services covered
    - etc.
- Different categories:
    - carrier license types: HMO, Commercial Carrier, Senior Care option, etc.
    - Line of Business: HMO, PPO, Medicare Advantage, etc.
    - Insurance market: individual, health exchange, group, student, etc.
    - Type of benefit: medical, pharm, dental, vision, etc.
    - Risk type: self-insured, fully-insured
- Why do we need product data?
    - Which products result in the best patient behavior?
        - Do patients with high deductibles have a different pattern of claims than patients with low deductibles?
        - Do medical providers treat patients differently based on the insurance product?

**Provider Data**

- Provider ID
    - Tax ID
    - UPIN: Unique Physician ID Number (medicare)
    - DEA Number
    - License ID
    - State Provider Org ID
    - NPI: National Provider ID number
- Provider Organizations
    - Sometimes there are hierarchies, parent companies
- Why do we need provider data?
    - Which providers offer the highest quality care?
    - Did a recent hospital merger lead to higher costs at one of the hospitals?
    - Are there providers who are significantly over-utilizing certain procedures, medications, etc?
    - Are there geographic regions that do not have some specialists available?
    - How do HMO doctors compare to fee-for-service doctors?

**PHI**

- Protected Health Information (PHI). Anything that can link medical information back to an individual.
- PHI identifiers are encrypted in the APCD.
- Levels
    - 1: Public Use
    - 2: Restricted to qualified individuals and parties
    - 3: No release (only available to government agencies, providers, and payers following approval by the Data Privacy Committee)
- Limited Data Sets (LDS) are a subset of APCD that exclude PHI identifiers.
- SSN are very sensitive form of PHI; they must be redacted.

**Administrative Simplification**

- Reduction of regulatory compliance costs for insurance orgs
- Does this by helping gov agencies use the APCD to meet their data needs
- Example: Merged Market Risk Adjustment for ACA
    - Health of individual patients is estimated by analyzing their recent medical history. This estimate is known as the Risk Score.
    - Instead of giving their own data, insurance orgs can point to the APCD.
- Example: GIC Tiering
    - Group Insurance Commission (GIC) ranks doctors based on the cost and quality of care they provide.
        - This ranking process uses detailed claims data. Historically, insurance companies had to submit data directly to the GIC, but a project is underway to source the data from the APCD.

**How are claims paid?**

- Fee for service payments
    - Most traditional
    - provider is reimbursed for each test/procedure that a patient receives
    - Not ideal because it can lead to an inflation of procedures/claims
- Bundled-episode payments
    - Providers are reimbursed based on diagnosis
    - Common for maternity claims, where providers are paid a fixed amount for all services leading up to delivery.
    - Sometimes also used for Medicare claims
- Capitation & Global Payments
    - Providers are paid a fixed amount per member per month
    - Covers all services provided to the member
    - Some high-cost services (e.g., advanced imaging) can be carved out of capitation agreement.
    - Gives providers strong incentive to reduce over-utilization and maximize preventative care.
    - Foundation of the HMO business model.

**Billing data**

- Billed amount: Amount the provider billed.
- Allowed amount: max amount the insurance org has agreed to pay the provider for the service rendered.
- Paid amount: amount actually paid by the insurance company.
    - For capitated claims, it can be entered as 0, or as the "fee-for-service equivalent": a statistical value that represents the estimated amount the insurance org would have paid if the claim was under a fee-for-service agreement.
- Cost Sharing
    - Copays: out of pocket payment at the time of service.
        - Designed to encourage members to choose the lowest cost source of appropriate care.
    - Deductibles: amount a member agrees to pay before the insurance company will begin paying for medical services.
    - Coinsurance: member pays a fixed percent of each medical bill.
        - Allows member to pay a higher share of their medical bills in exchange for lower monthly premiums.
- Out-of-pocket max: caps the total amount a member will pay in a given year.

**Inpatient data elements:**

- Admission date
- Admission type (emergency, urgent, elective)
- Admission source (referred by whom, via emergency, via ambulatory care facility)
- Discharge status code (discharged, transferred)
- Admitting diagnosis
- Present on admission code (all diagnoses present on admission)

**ICD Codes**

- Identify all possible medical diagnoses
- ICD-9 was used from 1978-2015
- ICD-10 was adopted by US in 2015
    - contains 14,400 different codes
    - Clinical modifications version in US contains over 68,000 codes
    - Provides detailed diagnosis data, along with info about reason for health care visit
    - Permits recording lab results and quality metrics like body-mass index
- Hierarchical Condition Categories (HCCs)
    - These group ICD codes
        - There is an HCC for depression and one for diabetes.
    - They provide a high-level look at the patient's main medical conditions
    - HCCs are used to measure a patient's likely future costs based on chronic conditions in the patient's medical history.

**Procedure and Revenue Codes**

- Current Procedural Terminology Codes *(CPT) identify medical procedures.
    - Category 1: common billable procedures
    - Category 2: non-billable codes used to describe patient history, interventions, lab results, quality metrics.
    - Category 3: emerging technologies.
- HCPCS Codes (Hick Picks)
    - Healthcare Common Procedure Coding System
    - 3 levels
        - 1: Consist of the CPT codes
        - 2: Non-physician services and supplies. e.g., durable medical goods, ambulance, rehab, etc.
        - 3: no longer used.
- Revenue codes are 4-digit numbers that provide details about a medical service
    - type of room, type of medical supply, type of clinic
    - They help distinguish between similar procedures that have different costs due to location, supplies, facilities, etc.

**Facilities**

- General acute care facility
    - treat acute conditions like injuries, illnesses, and other urgent medical conditions
    - examples: emergency dept., ICU, coronary care, cardiology, neonatal ICU, and other areas where the patient could become acutely unwell and require stabilization.
- Skilled nursing facilities
    - For long-term patients (elderly, disabled) who require level of care provided by doctor or registered nurse.
- Intermediate care facilities
    - Medicaid-funded facility for those with intellectual disabilities
    - Comprehensive care
    - Often are "day programs" which allow patients to work in the community.
- Hospice
    - end-of-life care
    - inpatient or in patient's home
- Cancer Center
    - provide cutting edge treatments for cancer and related illnesses
    - also conduct cancer research and train cancer specialists
- Inpatient children's hospitals
    - pediatric care
    - they incur higher costs
- Inpatient rehab facilities
    - For patients who require at least 3 hours of intense rehab per day.
    - Often recovering from surgery or illness.
- Inpatient Psychiatric hospital
    - treating mental health disorders
- Critical Access Hospital
    - Smaller facilities (< 25 beds) in rural communities (<35 miles from another hospital) that provide emergency care services.
    - Provide short-term care (< 96 hours) for common illnesses and injuries.
    - Triage more complex cases and refer them to larger facilities.

**Types of Commercial Health Insurance**

- Health Maintenance Organizations (HMO)
- Exclusive Provider Organization (EPO)
- Preferred Provider Organization (PPO)
- Point of Service (POS)
- Indemnity Insurance
- Worker's Compensation

**Federal Healthcare**

- Medicare
    - Provides insurance for Americans age 65 and older
    - 43 million elderly and 9 million disabled people currently receive medicare.
    - Spending accounted for 20% of nation's health care expenditures in 2014.
    - Covers about half of cost of health care charges.
        - You can purchase advantage or supplement plans to cover additional charges.
- Medicaid
    - For low-income citizens and legal permanent residents
    - Accounted for 16% of nation's health care expenditures in 2014
    - Federal gov provides matching funds to states that provide assistance to low income individuals and families.
- Federal employee health benefit program
    - insurance to 8 mil fed employees and their dependents
    - pays about 72% of the average premium
    - can cover insurance from about 250 different insurance orgs

**Member Months**

- What's wrong with member eligibility data?
    - Time period that member has had insurance can be a single day or several years.
    - Hard to compare two enrollment records or the claims incurred during those two different amounts of time.
- "Member months" are defined as one member being enrolled for one month.
- Different calculation methods
    - Count members active on some specific day of the month (first, last, 15th)
    - Count members active for at least one day during the month
    - Count members active on every day of the month
- PMPM (per member per month)
    - common values that are calculated PMPM
        - medical claims
        - premium
        - tax
        - administrative service fee
    - A PMPM value is calculated by dividing some metric by the number of member months for the related members and time period.
- Member Months are often used to monitor an insurance org's membership trends.
    - Used internally to measure sales goals and success of marketing campaigns
    - Used by industry regulators to monitor risks to insurance company solvency

**Actuarial Values**

- Benefit Plan design
    - describes the product being sold. Includes:
        - type of policy
        - doctor network
        - deductibles, copay, coinsurance, etc.
- Actuarial value
    - Comparing policies with different benefit plan designs is difficult
        - "Should a plan with a $250 copay cost more or less than a similar plan with a $1500 deductible?"
    - Actuarial values are the % of total average costs for covered benefits that a plan will cover.
        - e.g., person who buys policy with 80% actuarial value should expect to pay approx. 20% of their medical costs out of pocket.
        - helps to measure and compare relative value of each policy's benefits.
- "Metal Levels":
    - Platinum has actuarial value of 90%
    - Gold = 80%
    - Silver = 70%
    - Bronze = 60%