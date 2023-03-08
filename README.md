# Healthcare Provider Fraud Detection


## 1. What is Healthcare Fraud?

Fraud is defined as any deliberate and dishonest act committed with the knowledge that it could result in an unauthorized benefit to the person committing the act or someone else who is similarly not entitled to the benefit. Healthcare fraud is one of the types of fraud. Here we will analyze and detect “Healthcare Provider Fraud” where the provider fills in all the details and makes a claim on behalf of the beneficiary. Provider Fraud is one of the biggest problems that Medicare is facing currently. Healthcare fraud is an organized crime that involves peers of providers, physicians, beneficiaries acting together to make fraud claims. As per U.S. legislation, an insurance company should pay a legitimate healthcare claim within 30 days. So, there is very little time to properly investigate this. Insurance companies are the most vulnerable institutions impacted due to these bad practices. As per the Government, the total Medicare spending increased exponentially due to frauds in Medicare claims.

## 2. Types of Healthcare Provider Fraud - 

Healthcare fraud and abuse take many forms. Some of the most common types of frauds by providers are:

a) Billing for services that were not provided.

b) Duplicate submission of a claim for the same service.

c) Misrepresenting the service provided.

d) Charging for a more complex or expensive service than was actually provided.

e) Billing for a covered service when the service actually provided was not covered.

## 3. Business Problem -

Statistics show that 15% of the total Medicare expense is caused due to fraud claims. Insurance companies are the most vulnerable institutions impacted due to these bad practices. The insurance premium is also increasing day by day due to this bad practice.
Our objective is to predict whether a provider is potentially fraudulent or the probability score of that provider’s fraudulent activity and also find the reasons behind it as well to prevent financial loss.
Depending on the probability score and fraudulent reasons insurance company can accept or deny the claim or set up an investigation on that provider.
Find out the important features which are the reasons behind the potentially fraudulent providers. Such as if the claim amount is high for a patient whose risk score is low, then it is suspicious.
Not only the financial loss is a great concern but also protecting the healthcare system so that they can provide quality and safe care to legitimate patients.

## 4. ML Formulation - 

Build a binary classification model based on the claims filed by the provider along with Inpatient data, Outpatient data, Beneficiary details to predict whether the provider is potentially fraudulent or not.

## 5. Business Constraints-

a) The cost of misclassification is very high. False Negative and False Positive should be as low as possible. If fraudulent providers are predicted as non-fraudulent (False Negative) it is a huge financial loss to the insurer and if legitimate providers are predicted as fraudulent (False Positive) it will cost for investigation and also it’s a matter of reputation of the agency.

b)Model interpretability is very important because the agency or insurer should justify that fraudulent activity and may need to set up a manual investigation. It should not be a black box type prediction.

c) The insurer should pay the claim amount to the provider for legitimate claims within 30 days. So, there are no such strict latency constraints but it should not take more than a day because depending on the output of the model the agency may need to set up an investigation.


## 6. Dataset Column Analysis - 

**Source of Data**: The dataset is given on Kaggle's website.

### **Train-1542865627584.csv**:
It consists of provider numbers and corresponding whether this provider is potentially fraudulent. Provider ID is the primary key in that table.

### **Test-1542969243754.csv**:
It consists of only the provider number. We need to predict whether these providers are potential fraud or not.

### **Outpatient Data (Train and Test):**
It consists of the claim details for the patients who were not admitted into the hospital, who only visited there. Important columns are explained below.

**BeneID:** It contains the unique id of each beneficiary i.e patients.

**ClaimID:** It contains the unique id of the claim submitted by the provider.

**ClaimStartDt:** It contains the date when the claim started in yyyy-mm-dd format.

**ClaimEndDt:** It contains the date when the claim ended in yyyy-mm-dd format.

**Provider:** It contains the unique id of the provider.

**InscClaimAmtReimbursed:** It contains the amount reimbursed for that particular claim.

**AttendingPhysician:** It contains the id of the Physician who attended the patient.

**OperatingPhysician:** It contains the id of the Physician who operated on the patient.

**OtherPhysician:** It contains the id of the Physician other than AttendingPhysician and OperatingPhysician who treated the patient.

**ClmDiagnosisCode:** It contains codes of the diagnosis performed by the provider on the patient for that claim.

**ClmProcedureCode:** It contains the codes of the procedures of the patient for treatment for that particular claim.

**DeductibleAmtPaid:** It consists of the amount by the patient. That is equal to Total_claim_amount — Reimbursed_amount.

### **Inpatient Data (Train and Test):**
It consists of the claim details for the patients who were admitted into the hospital. So, it consists of 3 extra columns Admission date, Discharge date, and Diagnosis Group code.

**AdmissionDt:** It contains the date on which the patient was admitted into the hospital in yyyy-mm-dd format.
**DischargeDt:** It contains the date on which the patient was discharged from the hospital in yyyy-mm-dd format.
**DiagnosisGroupCode:** It contains a group code for the diagnosis done on the patient.

### **Beneficiary Data (Train and Test):** This data contains beneficiary KYC details like DOB, DOD, Gender, Race, health conditions (Chronic disease if any), State, Country they belong to, etc. Columns of this dataset are explained below.

**BeneID:** It contains the unique id of the beneficiary.

**DOB:** It contains the Date of Birth of the beneficiary.

**DOD:** It contains the Date of Death of the beneficiary if the beneficiary id deal else null.

**Gender, Race, State, Country:** It contains the Gender, Race, State, Country of the beneficiary.

**RenalDiseaseIndicator:** It contains if the patient has existing kidney disease.

**ChronicCond_*:** The columns started with “ChronicCond_” indicates if the patient has existing that particular disease. Which also indicates the risk score of that patient.

**IPAnnualReimbursementAmt:** It consists of the maximum reimbursement amount for hospitalization annually.

**IPAnnualDeductibleAmt:** It consists of a premium paid by the patient for hospitalization annually.

**OPAnnualReimbursementAmt:** It consists of the maximum reimbursement amount for outpatient visits annually.

**OPAnnualDeductibleAmt:** It consists of a premium paid by the patient for outpatient visits annually.


## Exploratory Data Analysis

### Distribution of Class Labels (Provider Data):

<img width="722" alt="Screen Shot 2023-03-07 at 10 26 51 PM" src="https://user-images.githubusercontent.com/68578215/223636860-cfac672a-c913-440f-b6db-542fc71d14fb.png">

** Observation: **

This is a highly imbalanced dataset. There are 10% fraudulent providers and 90% non-fraudulent providers.

### Distribution of Gender (Beneficiary Data):
<img width="724" alt="Screen Shot 2023-03-07 at 10 26 56 PM" src="https://user-images.githubusercontent.com/68578215/223636858-be67fb92-5a28-43e6-88e7-f39f88ef699d.png">

** Observation: **

The ratio of genders in beneficiary data is Gender_0 : Gender_1 = 57% : 43%.

### Distribution of State (Beneficiary Data):

<img width="754" alt="Screen Shot 2023-03-07 at 10 27 02 PM" src="https://user-images.githubusercontent.com/68578215/223636853-89ca3c3a-59cc-4b41-9f77-a2c7b22c83f3.png">

** Observation: **

1. The top 20 states in terms of the beneficiary count are shown in the above picture.
2. States with codes 5, 10, 45, 33, and 39 are the top 5 states.
3. 8.7% of the beneficiaries belong to state 5.

<img width="738" alt="Screen Shot 2023-03-07 at 10 27 08 PM" src="https://user-images.githubusercontent.com/68578215/223636849-17458299-4873-4219-9e9b-86412bbb26a5.png">
** Observation: **
<img width="740" alt="Screen Shot 2023-03-07 at 10 27 13 PM" src="https://user-images.githubusercontent.com/68578215/223636846-99e57445-5800-4393-b47b-69acc95d4140.png">


** Observation: **
<img width="797" alt="Screen Shot 2023-03-07 at 10 27 17 PM" src="https://user-images.githubusercontent.com/68578215/223636844-19d9e6f0-fb2f-4982-8c6d-f29e2b2bb344.png">


<img width="781" alt="Screen Shot 2023-03-07 at 10 27 31 PM" src="https://user-images.githubusercontent.com/68578215/223636843-0525a398-bd91-4030-89d2-3b1a4ccc4e93.png">

<img width="774" alt="Screen Shot 2023-03-07 at 10 27 36 PM" src="https://user-images.githubusercontent.com/68578215/223636833-d5fb181a-a998-4a48-9550-51cd1fda95bd.png">
