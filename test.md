# Job Comparison App – Requirements and Design

---

## 1. Main Menu

When the app is started, the user is presented with the **main menu**, which allows the user to:

1. Enter or edit current job details  
2. Enter job offers  
3. Adjust the comparison settings  
4. Compare job offers  
   - Disabled if no job offers were entered yet¹  

> This is not represented in my design, as it will be handled entirely within the GUI implementation.

---

## 2. Entering Current Job Details

When choosing to enter current job details, a user will:

### a. Be shown a user interface to enter (or edit) the following details:

1. **Title**  
2. **Company**  
3. **Location** (city and state)  
4. **Cost of living index**  
5. **Yearly salary**  
6. **Yearly bonus**  
7. **Stock Option Shares (SOS)**  
   - Whole number  
   - Assumes 3-year vesting period  
   - $1 stock value  
8. **Wellness Stipend (WS)**  
   - $0–$1200 inclusive annually  
9. **Life Insurance (LI)**  
   - Percentage of yearly salary  
   - Integer: 0–10 inclusive  
10. **Personal Development Fund (PDF)**  
    - $0–$6000 inclusive annually  

### b. User actions

- Save the job details  
- Cancel and exit without saving  

Both return to the **main menu**.

### Design Realization

- A class named **`Job`** is defined with all the above attributes.
- Includes an operation for entering a new job.
- **`JobOffer`** and **`CurrentJob`** inherit from `Job`.
- `CurrentJob` includes an additional method:
  - `editCurrentJobDetails()`

---

## 3. Entering Job Offers

When choosing to enter job offers, a user will:

### a. Enter the same details listed for the current job  
### b. Save or cancel  
### c. Choose to:
1. Enter another offer  
2. Return to main menu  
3. Compare the saved offer with the current job (if present)

### Design Realization

- The **`JobOffer`** class:
  - Inherits from `Job`
  - Handles validation and saving
- Application flow manages transitions:
  - Back to main menu  
  - Back to entering another offer  
  - To comparison  

### UML Relationships

- `JobOffer`: 0..*  
- `CurrentJob`: 0..1  
- Both inherit from `Job`  
- Associated with `JobComparison`

---

## 4. Adjusting Comparison Settings

Users can assign integer weights (0–9) to:

- Yearly salary  
- Yearly bonus  
- Stock Option Shares  
- Wellness Stipend  
- Life Insurance  
- Personal Development Fund  

### Rules

- 0 = No interest  
- 9 = Highest interest  
- Default weight = 1  
- If no weights assigned → all factors are equal  
- User can:
  - Save
  - Cancel  
- Both return to main menu

### Design Realization

- Class: **`ComparisonSettingsWeightsAdjustment`**
  - Attributes: integer weights (default = 1, range 0–9)
  - Methods:
    - `setWeight()`
    - `save()`
    - `cancel()`
    - `returnToMainMenu()`

---

## 5. Comparing Job Offers

When choosing to compare job offers:

### a. Display ranked list (best to worst)

- Title
- Company
- Includes current job (if present)
- Clearly indicated

### b. User selects two jobs  
### c. Display comparison table:

For each job:

1. Title  
2. Company  
3. Location  
4. Adjusted Yearly Salary (AYS)  
5. Adjusted Yearly Bonus (AYB)  
6. Stock Option Shares (SOS)  
7. Wellness Stipend (WS)  
8. Life Insurance (LI)  
9. Personal Development Fund (PDF)  
10. Job Score (JS)

### d. User can:
- Perform another comparison  
- Return to main menu  

### Design Realization – `JobComparison` Class

Methods:

- `hasCompareEnabled()` → boolean  
- `showListOfJobOffer()` (GUI handled)  
- `rankFromBestToWorst()`  
- `includeCurrentJob()`  
- `triggerComparison()`  
- `displayTwoJobs()`  
- `performAnotherComparison()`  
- `returnToMainMenu()`  

Attributes:

- `currentJobIndicator` (string)

> Selecting two jobs is handled entirely within the GUI.

---

## 6. Job Scoring Formula

A job’s score is computed as the **weighted average** of:
