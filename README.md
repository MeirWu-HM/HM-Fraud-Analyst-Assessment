# HM-Fraud-Analyst-Assessment

## Problem Statement
You are working for an online personal loans lending platform called “Joyful Dollars” as a lead fraud analyst. Your responsibilities include monitoring the fraud model performance and adjusting the fraud pass/review/reject trigger rules appropriately.

Currently, Joyful Dollars (JD) is facing a significant challenge. Over the past quarter, Joyful Dollars has experienced thousands of fraud attacks, leading to overly aggressive fraud review/reject rules. These stringent rules have resulted in relatively high false positive rates. Therefore, as the lead fraud analyst, you are responsible not only for monitoring model performance but also for proactively identifying trends, optimizing rule configurations, and recommending data-driven improvements. This involves analyzing historical data to pinpoint patterns and anomalies, visualizing key performance indicators, investigating specific rule triggers, and suggesting enhancements to the data collection process. 

Be sure to read the tips at the bottom of the page!

---

## Assignment:
You have been tasked with analyzing the available data to identify:
- Given the data available, which dates are Joyful Dollars most likely to encounter spike(s) in fraud?
- Create a graph outlining the percentage of Confirmed Fraud to False Positive based on Fraud Model Reason (fictitious example: vpn_review accounts for 50% Confirmed Fraud and 50% False positive) 
- Which rule produces the highest number of false positives?
- Build a model to replace the rule identified in question #3 using the model evaluation metrics below. (Hint: Focus on False positive and confirmed fraud population.)  
  Sample Model evaluation metrics: Recall, AUC-ROC, Accuracy  
  You are welcome to provide any other performance metrics as you see fit
- Are there any features or data points that are missing from this dataset that you would have liked to have?

---

## Tools:
You may use any tool that uses Python and R. Below are some free options but feel free to use whatever you are most comfortable with to manipulate the datasets below.

---

## Reference:
- https://code.visualstudio.com/ 
- https://www.anaconda.com/docs/getting-started/anaconda/install 

---

## Dataset:
Please download the data and metadata within this repo: 

---

## Tips:
To help the analysis, there are some hints and additional information candidate should know:

Joyful Dollars’ fraud framework comprises three main components:
- **Device and Behavior (DNB, D&B) model:**  
  Most applications include a DnB result since this model monitors the entire process of the applicant’s behavior and device information. The outcomes are reflected in the BEHAVIOR_CHECK_SCORE and DEVICE_CHECK_SCORE.
- **Digital Identity Trust (DIT) model:**  
  The DIT model is triggered when an application is approved by Joyful Dollars’ credit policy. If the application does not move to the offer stage or is not approved by the credit policy, the DIT model will not be activated. The outcome of this model is captured in DIT_DECISION.
- **Kount model:**  
  Like the DIT model, the Kount model is only run when an application is approved by the credit policy. It is not triggered if the application fails to reach the offer stage or is not approved. The outcome of the Kount model is captured in KOUNT_AUTO.

Based on the outcomes of these three models and additional rules set by Joyful Dollars’ fraud experts, a consolidated field, FRAUD_MODEL_RESULT, is generated with the following possible values:
- fraud_pass: No friction caused by JD’s fraud model
- fraud_reject: Application was rejected by the fraud model before executing the credit policy
- fraud_decline: Application was rejected by the fraud model after credit policy processing
- fraud_review: Application was tagged for review by the fraud modell
- fraud_review_no_case: The flag is identical to fraud_review in this case

After the credit policy and fraud screening, applications proceed to the underwriting stage. During underwriting, the FRAUD_MODEL_RESULT is translated into a new field, FRAUD_STATUS, with the following outcomes:
- Pass: FRAUD_MODEL_RESULT = ‘fraud_pass’
- Fail: FRAUD_MODEL_RESULT = ‘fraud_decline’ or ‘fraud_fail’
- Manual Review: FRAUD_MODEL_RESULT = ‘fraud_review’
- Manual Review No Case: FRAUD_MODEL_RESULT = ‘fraud_review_no_case’
- False Positive: Following manual review, if the agent determines the case was a false positive, the status becomes “False Positive”.
- Confirmed Fraud: Following manual review, if the agent determines the case is genuine fraud, the status becomes “Confirmed Fraud”.

Note: In the analysis dataset, if FRAUD_STATUS is “Manual Review” or “Manual Review No Case”, it typically indicates that the application expired or was declined due to criteria unrelated to fraud. This may include:
- Decline by credit policy
- Offer not selected by the applicant
- Failure to submit required documents on time

The rules that triggered fraud reject/decline/review are detailed in the FRAUD_MODEL_REASONS column. We expect you to review and understand these rules as part of your analysis.

Please note that real-world data is rarely perfect. Expect to encounter discrepancies and dirty data; your ability to process and clean such data will be an important part of this case assessment.

Notes:
- Data Source: The dataset is a single CSV file attached with your take home challenge. If you encounter any difficulty in opening this CSV file or have any questions during the take-home challenge, please reach out to your recruiter.
- Tools for analysis: Feel free to use whatever tools or analysis software you think makes the most sense. But we suggest using python as a widely accepted programming language in our team.
- Outside help: Basic internet search for generic questions is fine, but you are expected to complete this challenge without consulting other individuals for help or collaboration. The use of AI tools (e.g., ChatGPT, GitHub Copilot) is strictly prohibited during live interviews and any take-home or assigned interview tasks. We expect all submissions to reflect the candidate’s own work. Please note that we actively monitor for AI-generated content and take violations seriously, as they compromise the fairness and integrity of our hiring process.
- Submission: You will need to reply to the take home challenge Email to your recruiter with your completed answers including codes to question above. The submission can be in any format you prefer and be several files if you wish. Please submit your written response to your recruiter within 24 hours of receipt.
