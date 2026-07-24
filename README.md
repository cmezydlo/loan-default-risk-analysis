# Exploratory Analysis of Loan Default Risk

## Executive Summary
Horizon Financial Group would like to reduce their default rate by half (from 24.3% to 12%). The top three factors related to default rate are credit score, debt-to-interest (DTI) ratio, and interest rate. After exploring the data for these factors, we recommend loan approvals be restricted to applications with credit scores at or above 600, DTI ratios under 41%, and interest rates under 14%. By implementing these guidelines, Horizon can reduce their default rating to 12.0%.

---

## Project Overview
Management at Horizon Financial Group (a mid-sized consumer lending company) is concerned with the rising default rate on personal loans and wants data driven insights to improve the underwriting process. This project explores borrower demographics, loan characteristics, and repayment outcomes to identify the key risk factors that predict loan defaults.

## Business Problem
Horizon's current default rate is nearly 25%, nearly twice their goal of 12%. Defaulted loans are lost funds (including repayment of loaned monies due and interest) to a lender, thus higher default rates are costly to lenders and can also affect the lender's reputation. To reduce default rate, lenders assess who they are loaning to (do any characteristics predict default?) and what types of loans are being approved (do specific loan purposes have an elevated risk?) to identify guidelines related to non-defaulting conditions for future loans.

## Objectives
1. Identify the overall default rate and how default rate breaks down by credit score range.
2. Assess the relationship between a borrower's debt to income (DTI) ratio and the likelihood of defaulting.
3. Determine which loan purposes, employment status, and years employed have the highest default rates.
4. Evaluate how the average loan amount differs between defaulted and non-defaulted. 
5. Recommend lending policies that reduce default rates.

## Dataset
Horizon's data structure consists of two csv files containing borrower profiles and loan application data, with a total row count of 1101 records. A description of each file is as follows:
- **Borrower Profiles**: Contains a list of borrowers with demographic information.
- **Loan Applications**: Contains a list of all loans associated with each borrower ID.


## Repository Structure
| FILE | DESCRIPTION |
| --- | --- |
| Analysis.ipynb | Exploratory analysis |
| Assess and Clean Data.ipynb | Data cleaning and preprocessing |
| README.md | Project documentation |
| .pkl | Intermediate save point file |
| .ipynb_checkpoints/ | Automated JupyterLab saves |
| images/ | Charts used in README |
| other/ | Other files used in analysis |
| zzz archive/ | Older versions of files |

## Data Preparation
* CSV files were imported as dataframes and assessed individually for null values, incorrect data types, and duplicates. No null or duplicate values were found. Application Date was changed to a datetime data type.
* Columns within each dataframe were assessed using pandas and seaborn bar and histogram plots to determine data value ranges, distribution of the values within the dataset, and determine which columns would benefit from binning for later analysis.
* Joined borrower and loan dataframes into one dataframe on borrower_id.

The Python notebook used to inspect, clean, and prepare the data for this analysis can be found in the [Assess and Clean Data notebook](https://github.com/cmezydlo/Loan_Analysis/blob/main/Assess%20and%20Clean%20Data.ipynb).

## Exploratory Data Analysis
* Created new columns for binned values: credit scores, DTI ratios, years employed, interest rates, ages
* Assessed multi loan borrowers
* Calculated overall default rate
* Assessed default rate by age, state, education level, employment status, years employed, credit score, home ownership, dependents, existing monthly debt, application date, loan purpose, loan amount, term months, interest rate, monthly payment, DTI, loan status, and days delinquent
* Assessed combinations of column data such as credit scores vs loan amounts, education level, employment status, and default rates for specific ranges of credit scores
* Calculated correlation to defaulted
* Quick logistic regression comparing defaulted with credit score, interest rate, and DTI ratio
* Assessed combinations of credit score, DTI ratio and interest rate for smallest default rate with largest loan amount
The Python notebook used to explore the data and analyze relationships can be found in the [Analysis notebook](https://github.com/cmezydlo/Loan_Analysis/blob/main/Analysis.ipynb)

## Key Findings
* **Credit Score**
    * TBD - add picture
    * **Only credit scores of 750 or greater meet the 12% default rate goal.** Nearly 40% of Horizon's current loans fall into this category of borrowers. While this group is the best option to loan to, limiting loans to only this group would reduce the number of loans by 60%.
    * **Credit scores between 520-599 have the highest default ratings.** This group has a 49.6% default rate and accounts for nearly 20% of Horizon's current loans.  
    * **Low credit scores greatly impact default rates.**
      | Credit Score Group | Default Rate|
      | :---: | :---: |
      | 520-599 | 49.6% |
      | 600-699 | 28.4% |
      | 700+ | 12.9% |
* **Debt-to-Income Ratio**
    * TBD - add picture
    * **Horizon has granted more dollars in loans to borrowers with 51% or greater DTI ratios.** This category accounts for 45% of all loans and 64% of all defaulting loans.
    * **To hit a 12% default goal, Horizon would need to restrict DTI to 25% or less.** This would reduce the number of loans by 87%.
    * **High DTI combined with low credit scores relates to higher default rates.** Comparing credit score and DTI allows us to identify ranges that align with the 12% goal (such as above 700 credit score and DTI less than 35%) and exposes similar pockets of favorable default rates in nearby combinations that could be leveraged with further refinement.
    * TBD - add picture
* **Interest Rate**
    * TBD - add picture
    * **On its own, interest rate is not enough to reduce default rate.** Most of the default rates by interest rate range are higher than the goal. Interest rates in the 8% group do have a favorable default rate, but this is because the data within this group includes the larges number of the best credit scores and lowest DTI ratios.
    * **Interest rates greater than 15% have the highest default rates.** Interest rate has a positive correlation to default; however, the correlation is likely due to the significant jump in default rate at the 14% interest rate group.
      | Interest Group | Avg default rate|
      | :---: | :---: |
      | <14% | 21% |
      | >14% | 56% |
    * **The average and median interest rate of about 10.5% is due to its frequence across all credit score groups.** The lowest credit scores have minimum interest rates in the 10% group which overlaps with interest rates granted to the highest credit scores which have maximum interest rates in the 12% group.
* **Loan Purpose**
    * TBD - add picture
    * **All loan purposes exceed the 12% goal.** There is no specific purpose that can be ruled out. 
    * **Loan purpose alone is not very helpful.** However, assessing purpose with default rate, count, and average loan amount can help Underwriters understand Horizon's exposure for specific loans. Home Improvement loans are the second highest default rate by loan purpose, and they are also the most common type of loan approved, they make up the largest amount of total amount loaned, and have the second highest average loan amount.
* **Employment**
    * TBD - add picture
    * **Very short employment length relates to higher default rate.** Borrowers with less than 2 years of employment have a 34.5% default rate, which is double the rate of borrowers with 2-5 years of employment length. This higher default rate is likely due to borrowers starting off their credit history and having less job security.
    * **2-5 years is timeframe with the lowest default rate.** This may be due to borrowers having better job security and some credit history.
    * **At 6 years, default rates increase.** This may be due to borrowers taking on more debt to purchase homes, have families, etc, and having the ability to borrow more than they could earlier in their careers.

## Recommendations
Based on the insights and findings above, we recommend Horizon Financial Group consider the following:
* Restrict loan approvals to credit scores greater than 600.
* Limit loan approvals to applicants with DTI ratios less than 41%.
* Limit approvals to loans with interest rates under 14%.
* Exercise caution with home improvement loans and borrowers with less than 2 years of employment.

## Assumptions & Caveats
* Dataset only includes approved loans.
* Only 30 states are represented.
* Best option for guidelines based on combination of credit score, and DTI ratio that produced the highest total loan amount.
* Findings may not generalize beyond this dataset.
* Correlation does not imply causation.

## Technologies Used
* Python
* Seaborn
* Pandas
* Matplotlib
* Scikit-Learn
* Jupyter Notebook
* Excel
* GitHub
* Git

## How to Reproduce
1. Clone the repository.
2. Install packages (see requirements.txt).
3. Open the Assess and Clean Data notebook and run all cells.
4. Open the Analysis notebook and run all cells.

## Future Improvements
Ideas for this project:
* Build a predictive machine learning model.
* Develop an interactive dashboard - could be used to monitor changes in default rates by loan purpose and exposure and other relationships.
* Incorporate denied loan applications, if available.
