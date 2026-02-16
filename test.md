1.     When the app is started, the user is presented with the main menu, which allows the user to (1) enter or edit current job details, (2) enter job offers, (3) adjust the comparison settings, or (4) compare job offers (disabled if no job offers were entered yet1).
 
This is not represented in my design, as it will be handled entirely within the GUI implementation.
 

2. When choosing to enter current job details, a user will:
a. Be shown a user interface to enter (if it is the first time) or edit all the details of
their current job, which consists of:
i. Title
ii. Company
iii. Location (entered as city and state)
iv. Cost of living in the location (expressed as an index)
v. Yearly salary
vi. Yearly bonus
vii. Stock Option Shares (Whole number, assumes 3-year vesting period
and $1 stock value)
viii. Wellness Stipend ($0-$1200 Inclusive annually)
ix. Life Insurance (Percentage of Yearly Salary as an integer: 0 – 10
inclusive)
1 To be precise, this functionality will be enabled if there are either (1) at least two job offers, in case there
is no current job, or (2) at least one job offer, in case there is a current job.
x. Personal Development Fund ($0 to $6000 inclusive annually)
b. Be able to either save the job details or cancel and exit without saving, returning
in both cases to the main menu.

To realize this requirement, a class named ‘Job’ is defined as having all the job details above as its attributes and an operation for entering a new job which will be used to get the details of a new job. ‘Job Offer’ and ‘Current Job’classes are children of parent ‘Job’ class and inherit all the attributes and operations except ‘Current Job’ class has an additional ‘editCUrrentJobDetails()’ for editing all the details of the current job.

3. When choosing to enter job offers, a user will:
a. Be shown a user interface to enter all the details of the offer, which are the same
ones listed above for the current job.
b. Be able to either save the job offer details or cancel.
c. Be able to (1) enter another offer, (2) return to the main menu, or (3) compare the
offer (if they saved it) with the current job details (if present).

To realize this requirement, a class named Job Offer will handle the user interface for entering job offer details, utilizing the attributes inherited from the parent Job class. It will include operations for validation and saving. The application flow will manage transitions back to the main menu, back to the Job Offer for entering another offer, or to the comparison function based on the user's choice. As it has been shown in the UML diagram a Job Offer class can be zero to as many, while the Current Job class would be 0 or 1 and they have a child-parent relation with Job class and an association with Job Comparison.

4. When adjusting the comparison settings, the user can assign integer weights to:
a. Yearly salary
b. Yearly bonus
c. Stock Option Shares
d. Wellness Stipend
e. Life Insurance
f. Personal Development Fund
NOTE: These factors should be integer-based from 0 (no interest/don’t care) to 9
(highest interest). Default value for all weights: 1
- If no weights are assigned, all factors are considered equal.
- The user must be able to either save the comparison settings or cancel; both will
return the user to the main menu.

To realize this requirement, a class named Comparison Settings Weights Adjustment will handle the comparison settings, utilizing the described attributes in requirement (4) with the datatype of int, default value of 1 and value between 0 to 9. It includes an operation called “setWeight” substituting the entered  weight with the default values and operations “save”, “cancel”, “returnToMainMenu” each for the corresponding task described in the requirement.


5. When choosing to compare job offers, a user will:
a. Be shown a list of job offers, displayed as Title and Company, ranked from best
to worst (see below for details), and including the current job (if present), clearly
indicated.
b. Select two jobs to compare and trigger the comparison.
c. Be shown a table comparing the two jobs, displaying, for each job:
i. Title
ii. Company
iii. Location
iv. Yearly salary adjusted for cost of living
v. Yearly bonus adjusted for cost of living
vi. Stock Option Shares (SOS)
vii. Wellness Stipend (WS)
viii. Life Insurance (LI)
ix. Personal Development Fund (PDF)
x. Job Score - (JS) Calculation shown in Requirement #6
d. Be offered to perform another comparison or go back to the main menu.

To realize this requirement, in the Job Comparison class, I include an operation “hasCompareEnabed()” with boolean to determine if compare job offer has been chosen. The operation  “showListOfJobOffer()”, displayed job offers as Title and Company in a table which has not represented in my design and will be handled within the GUI implementation.  I include an operation “rankFromBestToWorst()” in the Job Comparison class to rank the jobs based on their score from highest to lowest score. The operation “includeCurrentJob()” has been added, which indicates if the current job is presented to either include it or not. “currentJobIndicator” attribute is a string that has a value which indicates clearly the current job when comparing job offers. Selecting two jobs  is not represented in my design, as it will be handled entirely within the GUI implementation. The “triggerComparison()” operation will do the comparison and the operation “displayTwoJobs” will show a table comparing two jobs and for each will display the associated job parameters. An operation called “performAnotherComparison()” suggests if another comparison is needed or not or the class “returnToMainMenue()” will be called.

6. When ranking jobs, a job’s score is computed as the weighted average of:
AYS + AYB + (SOS/3) + WS + (LI/100 * YS) + PDF
where:
AYS = Yearly Salary Adjusted for cost of living
AYB = Yearly Bonus Adjusted for cost of living
SOS = Stock Option Shares (Whole number, assumes 3-year vesting period and $1
stock value)
WS = Wellness Stipend ($0-$1200 Inclusive annually)
LI = Life Insurance (Percentage of Yearly Salary expressed as an integer: 0 – 10
inclusive)
PDF = Personal Development Fund ($0 to $6000 inclusive annually)
For example, if the weights are 2 for the adjusted yearly salary, 2 for the adjusted yearly
bonus, 2 for SOS, and 1 for all other factors, the score would be computed as:
JS = 2/9 * AYS + 2/9 * AYB + 2/9 * (SOS/3) + 1/9 * WS + 1/9 * (LI/100 * YS) + 1/9 * PDF
For example, if the weights are 3 for the adjusted yearly salary, 3 for the adjusted yearly
bonus, 4 for SOS, and 1 for all other factors, the score would be computed as:
JS = 3/13 * AYS + 3/13 * AYB + 4/13 * (SOS/3) + 1/13 * WS + 1/13 * (LI/100 * YS) + 1/13 * PDF

To realize this requirement, I added a float  “yearlySalaryAdjustedForCostOfLiving”  and a float “yearlyBonusAdjustedForCostOfLiving” to the ‘Scoring Job’ class to represent the Yearly Salary Adjusted for cost of living (AYS) and Yearly Bonus Adjusted for cost of living (AYB). The operation “setAYS” and “setAYB” will calculate and set the values AYS and AYB, using the “costOfLivingInTheLocation” index. The “jobScoreCalculation” operation does the calculation based on the two values of the AYS and AYB, the other values from either current job and/or job offer attribute and the weights derived from “Comparison Settings Weights Adjustment”.


7. The user interface must be intuitive and responsive.

This is not represented in my design, as it will be handled entirely within the GUI implementation.



8. For simplicity, you may assume there is a single system running the app (no communication or saving between devices is necessary).

This assumption has been made and communication or saving between devices are not represented in my device. Also we don’t need a user class to identify the current user since the assumption of this app design assignment is that the app is a single-user job comparison app.


