# Lending club - Risk Analytics 

Consumer finance company ( Banking and financial ) which specializes in lending various types of loans to urban customers. When the company receives a loan application, the company has to make a decision for loan approval based on the applicant’s profile. 
Two types of risks are associated with the bank’s decision:
If the applicant is likely to repay the loan, then not approving the loan results in a loss of business to the company
If the applicant is not likely to repay the loan, i.e. he/she is likely to default, then approving the loan may lead to a financial loss for the company
Two type of decision will take for any loan application as “Loan Accepted “ and “Loan Rejected” 
Identify the loan Accepted  and load Rejected applications & criteria

## Table of Contents
* [General Info](#general-information)
* [Technologies Used](#technologies-used)
* [Conclusions](#conclusions)
* [Acknowledgements](#acknowledgements)

# General Information
# Introduction
Solving this assignment will give you an idea about how real business problems are solved using EDA. In this case study, apart from applying the techniques you have learnt in EDA, you will also develop a basic understanding of risk analytics in banking and financial services and understand how data is used to minimise the risk of losing money while lending to customers.

# Business Understanding
You work for a consumer finance company which specialises in lending various types of loans to urban customers. When the company receives a loan application, the company has to make a decision for loan approval based on the applicant’s profile. Two types of risks are associated with the bank’s decision:

If the applicant is likely to repay the loan, then not approving the loan results in a loss of business to the company

If the applicant is not likely to repay the loan, i.e. he/she is likely to default, then approving the loan may lead to a financial loss for the company

The data given below contains the information about past loan applicants and whether they ‘defaulted’ or not. The aim is to identify patterns which indicate if a person is likely to default, which may be used for taking actions such as denying the loan, reducing the amount of loan, lending (to risky applicants) at a higher interest rate, etc.

In this case study, you will use EDA to understand how consumer attributes and loan attributes influence the tendency of default.

# Business Objectives
This company is the largest online loan marketplace, facilitating personal loans, business loans, and financing of medical procedures. Borrowers can easily access lower interest rate loans through a fast online interface.

Like most other lending companies, lending loans to ‘risky’ applicants is the largest source of financial loss (called credit loss). The credit loss is the amount of money lost by the lender when the borrower refuses to pay or runs away with the money owed. In other words, borrowers who default cause the largest amount of loss to the lenders. In this case, the customers labelled as 'charged-off' are the 'defaulters'.

If one is able to identify these risky loan applicants, then such loans can be reduced thereby cutting down the amount of credit loss. Identification of such applicants using EDA is the aim of this case study.

In other words, the company wants to understand the driving factors (or driver variables) behind loan default, i.e. the variables which are strong indicators of default. The company can utilise this knowledge for its portfolio and risk assessment.

## Steps involved:
Reading and Understanding the Data
Data cleaning & preperation
Data Visualization (Univariate/Bivariate/Multivariate Analysis)
Conclusion: This part is about conclusion drawn from the study.

# Reading and Understanding the Data
- Import all require libraries
- Import the loan data from 2007 to 2011 and data dictionary 

# Data cleaning & preperation:

- Check the number of null values in the columns
	It is observed that many columns have all the null values, these columns may be deleted
- Dropping columns & rows with all the Null values
- Deleting all the columns which are not required and having only unique value and all unique values like id, member_id, url etc.
	Deleting columns with null value mostly null values "mths_since_last_delinq","mths_since_last_record","next_pymnt_d", desc column might have some interesting data so same is being kept even though 32.58% data is null.
- Dropping rows with null values
- Interest rate column and removing % and converting to float type for analysis
Understand the column:
- Desc column is similar to purpose of loan therefore dropping the column, also title column is also similar to purpose thus same is also deleted.
- Also columns related to behavioral attributes can be dropped as we are analysing the comparison between columns which can impact default of loan before sanction of loan as these data columns will not be availble to us before sanction. Also funding will be done after sanction thus columns related to funding is being dropped
- Our target column is loan_status for label as charged-off which indicated default against a loan

# Outlier treatment:
Let's create dataframe containing predictors and the corresponding outlier percetange and check the % of data left after all the outlier removal
% of row data lost during cleaning and removal of outliers is 15.23% which is not much considering no. of rows of the tune of 37k. Therfore, theses changes can be implemented on original updated dataframe

# Data Visualization (Univariate/Bivariate/Multivariate Analysis)

Univariate Analysis:

Identifying variables- Categorical variable:
- Ordered Categorical variables: grade, sub grade, issue_d, issue_year, Income_bin, Dti_bin etc.
- Un-ordered Categorical variables:emp_length, home_ownership, verification_status, purpose, addr_state etc.
- Quantitative variable
  loan_amnt, annual_inc, int_rate,dti etc.

- Out of total loans sanctioned excluding current loans 14.38% loans has been defaulted
- Loans with 60 month term has been started from 2010
- After starting sanctioning loan with 60 months term from 2010 it is seen that no. of defaults in 60 month term loan are on a increasing trend comapred to 36 month term loan.

Bivariate Analysis:

- Funded amount and funded amount by investor has a stromg correcaltion with each other and with loan amount, therfore theses two columns can be dropped
- As only 5 loans has been sanctioned in NE therefore high default in NE cannot be genearlized and can be ignored. The next state with maximum default rate is in NV which is having 416 no. of loan sanctioned

Derived Metrices:

- Check variable for income bin with low, Medium, High, Very high income and % loan
{'Low loan_amnt': '500.0 to   5000.0', 'Medium loan_amnt': '  5000.0 to  8875.0', 'High loan_amnt': '8875.0 to  13600.0', 'Very high loan_amnt': '13600.0 to 29000.0'}
- As installment is highly correlated with loan amount, it is assumed that simailar variation as above shall be there.


Multivariate Analysis:

- Lets check variation between dti and interest rate and loan status
- As can be seen there is a decreasing trend of loan default in 36 month term loans, however 60 month term loans deafult rate is on increasing trend ever since its inception in 2010.
- In case of very high interest rate, medium DTI is yielding alomst same deafult rate as very high DTI.
- Check combined effect of DTI ratio and interest rate on default %
{'Low int_rate': '5.42 to  8.90', 'Medium int_rate': ' 8.90 to  11.71', 'High int_rate': '11.71 to  14.22', 'Very high int_rate': '14.22 to 22.11'}
{'Low Dti': '0 to  8.35', 'Medium Dti': ' 8.35 to  13.56', 'High Dti': '13.56 to  18.70', 'Very high Dti': '18.70 to 29.99'}
- In case of very high interest rate, medium DTI is yielding alomst same deafult rate as very high DTI.

- Check combined effect of Verifiaction status  and income on default %
{'Low Income': '4000.0 to  40000.0', 'Medium income': ' 40000.0 to  55000.0', 'High Income': '55000.0 to  75000.0', 'Very high Income': '75000.0 to 137004.0'}
- Variation is as per earlier variation brought out above. No abnormality observed.

- Check combined effect of Loan amount and DTI on default %
{'Low loan_amnt': '500.0 to   5000.0', 'Medium loan_amnt': '  5000.0 to  8875.0', 'High loan_amnt': '8875.0 to  13600.0', 'Very high loan_amnt': '13600.0 to 29000.0'}
{'Low Dti': '0 to  8.35', 'Medium Dti': ' 8.35 to  13.56', 'High Dti': '13.56 to  18.70', 'Very high Dti': '18.70 to 29.99'}
- Variation is as per earlier variation brought out above. No abnormality observed.

- From above following is observed:
	In general max default for all the bins of loan amount is for loan given to small business
	For low and small loan amount default rates are higher for debt consolidation purpose of loan.
	For very high loan amount, house and education loan are having max default rate after small business
- Check combined effect of Loan amount and purpose on default %
- Again similar trend is there. Loan to small business is having max default rate among all income groups.

# Technologies Used
- Python 3.0 and above,EDA,Excel data dictionary,.csv data files,
- Pandas,numpy, metplotlib, seaborn libraries

# Conclusions
1. No. of loans being offered are in an increasing trend from 2007 to 2011 and so does the loan default rate.
2. Default rate is much higher for 60 months term comapred to 36 month term ever since its inception in 2010. Infact default rate is on decreasing trend for 36 months term may be due to increasing 60 month term loan. Therfore no. of 60 months term loan may be reduced.
3. It is observed that there is higher tendency of loan default when loan is being offered for purpose of small business, therfore no. of loans to small business may be reduced or offered after due diligence.
4. Less defaults are being observed for lower interest rate irrespective of dti, therfore, low interest rate loans may be given in more nos.. Also. Lonas are not being offered for higher dti(> ~25%) and higher interest rate (> ~15%) may be due to high default risk asociated with such loans.
5. For low and small loan amount default rates are higher for debt consolidation purpose of loan and also for very high loan amount, house and education loan are having max default rate after small business.
6. In case of very high interest rate, medium DTI is yielding alomst same deafult rate as very high DTI.

## Acknowledgements
- This project was inspired by loan applicant's and loan bank
- Reference if any
- This project was based on Loan applicant's and load criteria to approve or reject the load ( Risk Analytics for applicant's)

## Contact
Created by @data01312022 and  @eohitc - feel free to contact me!
