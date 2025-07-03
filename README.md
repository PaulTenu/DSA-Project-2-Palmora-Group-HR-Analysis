# DSA-Project-2-Palmoria-Group-HR-Analysis
## Project Objective
This Project aims to analyse product and customer review data to uncover actionable insights. The primary goal is to support data-driven decision-making across product development, marketing, and customer engagement strategies. By identifying patterns in customer feedback and product performance, the project aims to Highlight areas for product improvement, Inform targeted marketing campaigns and Enhance customer satisfaction and loyalty through better engagement.

## Data Set used
- <a href = "https://github.com/PaulTenu/DSA-Project-2-Palmora-Group-HR-Analysis/blob/main/Palmoria%20Group%20emp-data.csv">Original Data Set</a>
- <a href = "https://github.com/PaulTenu/DSA-Project-2-Palmora-Group-HR-Analysis/blob/main/Palmoria%20Group%20emp-data_%5Btransformed%5D.csv">Used Data Set</a>

## Analysis Tasks
1. What is the gender distribution in the organization? Distil to regions and
departments
2. Show insights on ratings based on gender
3. Analyse the company’s salary structure. Identify if there is a gender pay gap. If
there is, identify the department and regions that should be the focus of
management
4. A recent regulation was adopted which requires manufacturing companies to pay
employees a minimum of $90,000
  - Does Palmoria meet this requirement?
  - Show the pay distribution of employees grouped by a band of $10,000. For example:
  - How many employees fall into a band of $10,000 – $20,000, $20,000 – $30,000,
etc.?
  - Also visualize this by regions
6. With the rule for making bonus payment dataset;
  - Calculate the amount to be paid as a bonus to individual employees
  - Calculate the total amount to be paid to individual employees (salary inclusive of
bonus)
  - Total amount to be paid out per region and company-wide
7. Dashboard
  - <a href = "https://github.com/PaulTenu/DSA-Project-2-Palmora-Group-HR-Analysis/blob/main/DSA%20CAPSTONE%20PROJECT%20QNS.%203_POWER_BI.pdf">Dashboard File</a>

## Exploratory Data Analysis
1. Imported the employee data into Power BI. Did a proper cleaning which include;
  - Removing employees without salaries and departments indicated as "NULL".
  - Assign a generic gender status to employees who refused to disclose their gender. Created a column for it and named **Gender_Status**

2. Performed a Gender Distribution Analysis and created a barchart with the following attributes
  - Axis: *Department*
  - Value: Count of *Employees by Gender*
3. Created a slicer to filter by *Location*.
4. Visualize the overall *gender distribution* using a pie chart(*Donut Chart*).

**Measures applied for the first four steps;**
  - *Gender Count = COUNT('Employee'[Gender])*
  - *Gender Percentage = DIVIDE(CALCULATE(COUNT('Palmoria Group emp-data'[Gender_Status])), CALCULATE(COUNT('Palmoria Group emp-data'[Gender_Status]), ALL('Palmoria Group emp-data'[Gender_Status])))*
  - *Gender_Status = 
VAR g = TRIM(LOWER('Palmoria Group emp-data'[Gender]))
RETURN 
SWITCH(
    TRUE(),
    g = "Male", "Male",
    g = "Female", "Female",
    ISBLANK('Palmoria Group emp-data'[Gender]), "Not Specified",
    "Undisclosed"
)*

5. Minimum Salary Requirement Analysis
  - Created a histogram as follow:
    - Axis: Salary Band ($10,000 increments)
    - Value: Count of Employees
  - Calculated the number of employees below the minimum salary threshold by region. And visualised with a Bar chart:

**Measures applied;**
  - *Employees Below Minimum Salary = COUNTX(FILTER('Palmoria Group emp-data','Palmoria Group emp-data'[Salary] < 90000), 'Palmoria Group emp-data'[Salary])*
  - *% Below Minimum Salary (Female) = 
DIVIDE(
    COUNTX(
        FILTER(
            'Palmoria Group emp-data',
            'Palmoria Group emp-data'[Salary] < 90000 &&
            'Palmoria Group emp-data'[Gender] = "Female"
        ),
        'Palmoria Group emp-data'[Salary]
    ),
    CALCULATE(
        COUNTROWS('Palmoria Group emp-data'),
        'Palmoria Group emp-data'[Gender] = "Female"
    ),
    0
)*
  - **SAME WAS USED FOR MALE(%)**

## Dashboard

![Screenshot_Power_BI_dashboard](https://github.com/user-attachments/assets/b842b351-2524-4789-920d-5f8074f537ed)

## Project Insight
1. **Gender Distribution**: There is a relatively balanced gender representation, though a small number of employees have undisclosed gender information.

2. **Salary Analysis**:
  - A majority of both male and female employees earn below the $90,000 minimum threshold, with female employees slightly more affected.
  - Despite near parity in gender count, there is a $3M difference in total salary, indicating a possible gender pay gap.

3. **Departmental Gender Count**
  -Fields like Legal, Support, and Marketing show male dominance.
  -Departments such as Human Resources and Training lean more female.
  -Several departments (e.g., Engineering, Research) have uneven gender spread or significant undisclosed gender entries.

## Conclusion
While the analysis reflects a fairly balanced gender representation at Palmoria Group, it also highlights concerning patterns—particularly the high number of employees earning below the minimum salary and a notable gender-based pay gap. These findings point to signs of gender imbalance, especially in how roles and compensation are structured across departments. However, it would be premature to definitively label the organization a "manufacturing patriarchy." The data suggests the presence of patriarchal traits often observed in traditional manufacturing environments—such as male-dominated leadership roles or pay disparities—but the overall workforce is not heavily skewed toward men.

A more accurate assessment would require deeper exploration into the company’s internal policies, role-specific salary scales, and historical trends in hiring and promotion. Only with this broader context can we draw a well-informed conclusion about the company's equity and inclusion practices.

Addressing these issues will require Palmoria to implement fair and transparent pay structures, alongside intentional gender equity programs. These actions won’t just close existing gaps—they’ll also foster a more inclusive workplace, enhance employee morale, and reinforce Palmoria’s commitment to fairness, equity, and sustainable HR practices.
