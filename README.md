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


### Merge All the Datasets:  

<img width="725" alt="Screen Shot 2023-03-07 at 10 45 11 PM" src="https://user-images.githubusercontent.com/68578215/223639716-1b690926-bd22-4b48-9c28-48c82312e12a.png">


1. Merge Inpatient and Outpatient data based on common columns.

2. Merge beneficiary details with inpatient and outpatient data on BeneID.

3. Merge provider details with previously merged data on ProviderID.

## Exploratory Data Analysis

### Distribution of Class Labels (Provider Data):

<img width="722" alt="Screen Shot 2023-03-07 at 10 26 51 PM" src="https://user-images.githubusercontent.com/68578215/223636860-cfac672a-c913-440f-b6db-542fc71d14fb.png">

**Observation:**

This is a highly imbalanced dataset. There are 10% fraudulent providers and 90% non-fraudulent providers.

### Distribution of Gender (Beneficiary Data):
<img width="724" alt="Screen Shot 2023-03-07 at 10 26 56 PM" src="https://user-images.githubusercontent.com/68578215/223636858-be67fb92-5a28-43e6-88e7-f39f88ef699d.png">

**Observation:**

The ratio of genders in beneficiary data is Gender_0 : Gender_1 = 57% : 43%.

### Distribution of State (Beneficiary Data):

<img width="754" alt="Screen Shot 2023-03-07 at 10 27 02 PM" src="https://user-images.githubusercontent.com/68578215/223636853-89ca3c3a-59cc-4b41-9f77-a2c7b22c83f3.png">

**Observation:**

1. The top 20 states in terms of the beneficiary count are shown in the above picture.
2. States with codes 5, 10, 45, 33, and 39 are the top 5 states.
3. 8.7% of the beneficiaries belong to state 5.


### Distribution of Country (Beneficiary Data):

<img width="738" alt="Screen Shot 2023-03-07 at 10 27 08 PM" src="https://user-images.githubusercontent.com/68578215/223636849-17458299-4873-4219-9e9b-86412bbb26a5.png">

**Observation:**

1. The top 20 countries in terms of the beneficiary count are shown in the above picture.

2. Countries with codes 200, 10, 20, 60, and 0 are the top 5 states.

3.85% of the beneficiaries belong to country code 200.


### Distribution of Race (Beneficiary Data):
<img width="740" alt="Screen Shot 2023-03-07 at 10 27 13 PM" src="https://user-images.githubusercontent.com/68578215/223636846-99e57445-5800-4393-b47b-69acc95d4140.png">


**Observation:**

1. Race 1 is the most in terms of beneficiary count.

2. 85% of the beneficiaries belong to race 1.


### Distribution of Patient Risk Score (Beneficiary Data):

<img width="797" alt="Screen Shot 2023-03-07 at 10 27 17 PM" src="https://user-images.githubusercontent.com/68578215/223636844-19d9e6f0-fb2f-4982-8c6d-f29e2b2bb344.png">

**Observation:**

1. The distribution of patient risk scores is right-tailed.

2. Most of the patients with risk scores 2, 3, 4, 5.

3. Very few patients are there with risk score 9, 10, 11, 12

### Attending Physician (Inpatient and Outpatient):

<img width="781" alt="Screen Shot 2023-03-07 at 10 27 31 PM" src="https://user-images.githubusercontent.com/68578215/223636843-0525a398-bd91-4030-89d2-3b1a4ccc4e93.png">

**Observation:**

1. PHY422134, PHY341560, PHY315112, PHY411541, PHY431177 are the top 5 attending physicians for inpatient and PHY422134, PHY341560, PHY315112, PHY411541, PHY431177 are the top 5 attending physicians for outpatient in terms of the number of patients visit.

2. Physician PHY422134 treated 1% of the total inpatients and physician PHY330576 treated 0.5% of the total outpatients.

### Operating Physician (Inpatient and Outpatient):

<img width="774" alt="Screen Shot 2023-03-07 at 10 27 36 PM" src="https://user-images.githubusercontent.com/68578215/223636833-d5fb181a-a998-4a48-9550-51cd1fda95bd.png">

**Observation:**

1. PHY429430, PHY341560, PHY411541, PHY352941, PHY314410 are the top 5 operating physicians for inpatient and PHY330576, PHY424897, PHY314027, PHY423534, PHY357120 are the top 5 operating physicians for outpatient in terms of the number of patients operated.

2. Physician PHY429430 operated 0.56% of the total inpatients and physician PHY330576 operated 0.08% of the total outpatients.

### Procedure Code (Inpatient and Outpatient):

<img width="798" alt="Screen Shot 2023-03-07 at 10 55 47 PM" src="https://user-images.githubusercontent.com/68578215/223640968-556dfe01-7186-4748-aca7-7fb9da53c845.png">

**Observation:**

1. 4019, 9904, 2714, 8154, 66 are the top 5 procedures for inpatient, and 9904, 3722, 4516, 2744, 66 are the top 5 procedures for outpatient in terms of the number of diagnoses done.

2. Procedure 4019 is done 6.5% of the total procedures for inpatient and procedure 9904 is done 7.35% of total procedures for outpatient.

### Diagnosis Code (Inpatient and Outpatient):

<img width="742" alt="Screen Shot 2023-03-07 at 10 55 41 PM" src="https://user-images.githubusercontent.com/68578215/223640964-c5beb249-285b-429a-8248-0323fda9ff83.png">


**Observation:**

1. 4019, 2724, 25000, 41401, 4280 are the top 5 diagnosis codes for inpatient, and 44019, 25000, 2724, V5869, 4011 are the top 5 diagnosis codes for outpatient in terms of the number of diagnoses done.

2. Procedure 4019 test is done 4.3% of the total diagnosis for inpatient and 4.65% for outpatient.


### Distribution of Inpatient Outpatient in Final Dataset

<img width="751" alt="Screen Shot 2023-03-07 at 10 55 36 PM" src="https://user-images.githubusercontent.com/68578215/223640961-24a3cb83-3285-496e-afa1-5844a105fe86.png">

**Observation:**

1. The number of claims is less for inpatient data compared to outpatient data.

2. Even though the claims are less in inpatient data, the percentage of fraudulent activity is more in inpatient data(57.8%) whereas it is 36.5% in outpatient data. This is because the per claim reimbursement amount for inpatient is much higher(35 times calculated earlier) than the per claim reimbursement amount for outpatient.

### Scatter Plot of Patient Age vs InscClaimAmtReimbursed:

<img width="604" alt="Screen Shot 2023-03-07 at 10 59 18 PM" src="https://user-images.githubusercontent.com/68578215/223641591-335f4bed-f44a-468e-ad6b-637d38e844d0.png">


**Observation:**

1. From the Scatter Plot of Patient Age vs InscClaimAmtReimbursed, I can observe that if patient’s age60000 it tends to be a fraudulent transaction.
2. If the patient’s age>88 yrs and claim amount>60000 the probability to be fraudulent is high.

### Scatter Plot of IP_OP_TotalReimbursementAmt vs InscClaimAmtReimbursed:

<img width="634" alt="Screen Shot 2023-03-07 at 10 59 23 PM" src="https://user-images.githubusercontent.com/68578215/223641589-9f8cc100-a2d5-49df-abba-add6ec73cec2.png">


**Observation:**

If InscClaimAmtReimbursed>10000 and IP_OP_TotalReimbursementAmt>120000 then the chance to be a fraudulent transaction is high.

### Scatter Plot of IP_OP_AnnualDeductibleAmt vs InscClaimAmtReimbursed:

<img width="694" alt="Screen Shot 2023-03-07 at 10 59 29 PM" src="https://user-images.githubusercontent.com/68578215/223641585-f9e62d83-9bc2-4c12-ae38-23ee1915f4dc.png">

**Observation:**

If IP_OP_AnnualDeductibleAmt<5000 and InscClaimAmtReimbursed>600000 then the chance to be a fraudulent transaction is high.
