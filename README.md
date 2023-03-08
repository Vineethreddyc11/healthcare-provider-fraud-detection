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

## 5. Business Constraints:

a) The cost of misclassification is very high. False Negative and False Positive should be as low as possible. If fraudulent providers are predicted as non-fraudulent (False Negative) it is a huge financial loss to the insurer and if legitimate providers are predicted as fraudulent (False Positive) it will cost for investigation and also it’s a matter of reputation of the agency.

b)Model interpretability is very important because the agency or insurer should justify that fraudulent activity and may need to set up a manual investigation. It should not be a black box type prediction.

c) The insurer should pay the claim amount to the provider for legitimate claims within 30 days. So, there are no such strict latency constraints but it should not take more than a day because depending on the output of the model the agency may need to set up an investigation.
