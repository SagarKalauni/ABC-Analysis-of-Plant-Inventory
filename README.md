
Data © PSGC

Report by SagarKalauni

Premision for github by Josh Hangene [Controller]

**ABC Analysis of Plant Inventory:**

### Background of How I Got This Project

ABC Analysis of Plant Inventory was my very first solo project at PSGC. During my first week as an Analytics & Insight intern at PSGC, my supervisor assigned me two project dashboards to review and update. I enhanced the Plant Byproduct Dashboard and the Plant Outage Headcount Dashboard. PSGC's power plant deals with three types of byproducts: Gypsum, Fly-Ash, and Bottom Ash. I analyzed and updated their byproduct dashboard, making it dynamic and adding forecasting for sales, shipments, and production trends. My supervisor appreciated the insights and subsequently entrusted me with the Outage Headcount Analysis Dashboard. Building on the success of my previous project, I incorporated predictive analytics to forecast 2024 headcount based on the last three years of outage data.

A beneficial turning point occurred during a site visit facilitated by David (contractor Maintenance supervisor), an employee at PSGC, in late May during a forced outage. David provided a comprehensive tour of the plant, explaining its operations and showing me various parts and components and their working. I queried him about outage frequency and learned that typically, one unit shuts down during an planned outage. but sometime we have to shut the unit down due to maintenance issues also, while efforts are made to avoid shutdowns throughout the year, that very shutdown was a maintenance shutdown. His explanation sparked the idea for a dynamic dashboard tracking unit shutdown dates for both units in the plant. In my mind I want to create a dashboard that in one click will give all the dates on which Unit1 was shutdown in one side and all dates on which unit 2 was shut down in other side. And I eventually did that on very next day, making a dynamic dashboard of tracking all the shutdown dates, this initiative impressed my supervisor, who subsequently assigned me the ABC Analysis of Plant Inventory project.

### About the Project

PSGC has been operational since 2009 and manages a substantial inventory valued at $***M (confidential). Not all items in the inventory are equally critical. But they need to have all the items avaliable for emergencies. PSGC categorizes items annually into three categories: A, B, and C. The goal of this project was to automate the categorization process using Power BI, replacing the manual Excel-based system overseen by Justin, the warehouse supervisor. This transition aims to streamline the labor-intensive process of categorization based on Annual Dollar Value of Usage (ADVU). ADVU is determined by net quantity issued, excluding adjustments, scrap, and other transactions affecting inventory balances. This analysis, conducted every December, utilizes four years of usage data to assign ABC classifications. For newly introduced items, priority is given based on unit cost.

Excluded from ABC designation are capital items, commodities, VMI (vending machine inventory), boiler spares, and obsolete items, reflecting PSGC's strategic inventory management approach.

Rating of the plant inventory should be done this way:
A Items - 70%
B Items - 20%
C Items - 10%

### Data Cleaning

Data cleaning is a critical aspect of data analysis, ensuring accuracy and reliability in insights derived. For my inaugural solo project, I aimed to maximize dynamism while showcasing proficiency in Power Query's M-Language. Here's a breakdown of the steps I applied to clean the data specifically for desired outputs:

1. **Filtering Power Plant Data:**
   - Initially, I filtered the dataset to include only rows relevant to the power plant.

2. **Average Cost Calculation:**
   - To determine the average cost for each inventory item, I merged the dataset with the InvCost table and extracted the 'avgcost' column.

3. **Exclusion of Absolute Status Items:**
   - Items marked with an 'absolute' status were deemed irrelevant, so I removed all corresponding rows.

4. **Exclusion Based on Maximo Category and Null Average Cost:**
   - Certain items, such as capitalized items, were excluded based on their current Maximo category (N) and a null average cost. This step involved consolidating relevant columns to facilitate efficient filtering.

5. **Inclusion Based on Current Balance:**
   - Items categorized as 'N' but with existing current balances required separate handling to ensure accurate categorization. I achieved this by merging the dataset with the InvBalance table and incorporating the 'curbalance' column.

6. **Removal of Non-Stock Items with Zero Current Balance:**
   - Items classified under non-stock categories with a current balance of zero were excluded from further analysis. This step addressed inventory items located externally with vendors, emphasizing items currently in PSGC's possession.

There are few more filter which I am going to use DAX code to perform.

Below is the M-Code with comments detailing each step for clarity and reproducibility:

![1](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/acca8a6a-51dc-41ec-be3c-ddac83c24cf7)

![2](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/9bc73ef3-4d40-4d37-be2a-c42cba2ecfc7)


One all the basic data cleaning is done then I started modeling the data Tables

### Modeling

Now I was all set about to do the ABC analysis of Inventory. First of all I Extracted all the necessary data table from the maximo to the power BI through dataflow. I pulled 9 Tables from the Maximo Namely
InvBalance
InvCost
Inventory
Inventory(Z-Commodities)
InvReserve
InvStatus
InvTrans
items
Stagemat

Now I started creating a data model after looking a data and observing all the data table for a while. My data model looks like below:

![Screenshot 2024-06-22 150254](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/3bfc08ea-c0ed-447b-abd6-45860826118e)

## Steps Applied for Calculation

Having cleaned and organized the data, I focused on achieving my project's primary objective—implementing an effective ABC analysis of the plant inventory. Here's a structured outline of the steps I undertook to accomplish this:

1. **Calculation of Total Issues in the Last 4 Years:**
   - Determined how frequently each item was withdrawn from the warehouse over the past four years. Items with higher total issues are considered more frequently used.

   ![1](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/bea840a5-20b5-432e-a169-cb9af53fb435)

2. **Calculation of Annual Dollar Value of Usage (ADVU):**
   - Computed the ADVU for each item using the formula: `(total item issues in last 4 years * average cost) / 4`. If an item had zero total issues, ADVU was set equal to its average cost. This metric helps in assessing the financial significance of each inventory item annually.

   ![Screenshot 2024-06-22 161933](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/53cb9f1f-4d0e-4d7b-8078-30764256bb2f)

3. **Percentage Contribution to Total Inventory:**
   - Assessed the percentage contribution of each item to the total inventory value. This step highlighted items with significant financial impact versus those with minimal contribution.

   ![Screenshot 2024-06-22 161948](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/54e02d43-e114-43e7-b3e1-cf4ec2e534aa)

4. **Ranking Based on ADVU and Calculation of Cumulative Percentage:**
   - Ranked all items based on their ADVU values. To ensure distinct rankings despite similar ADVU values, I utilized a W-value technique. Next, calculated the cumulative percentage of the total inventory value, prioritizing higher ADVU items to classify the top 70% as A, the next 20% as B, and the bottom 10% as C.

   ![Screenshot 2024-06-22 162059](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/fea809d7-9870-41a2-9da8-2129ec6cf729)

![Screenshot 2024-06-22 162112](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/a3bde11e-ce80-4f60-a835-6971fbf53c8d)


![Screenshot 2024-06-22 162128](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/ced5ff74-25fa-4b28-aae1-f96e0a23c88a)



5. **Retention of Original Maximo Category for Certain Items and categories others:**
   - Items categorized as 'N' in the old Maximo system with a current balance of zero were retained in their original category. This decision was implemented using DAX (Data Analysis Expressions) to maintain flexibility for future inventory updates.

   ![Screenshot 2024-06-22 163517](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/c3aca969-67bd-496f-8ca2-0d0b7bb175be)

6. **Comparison and Remark of Category Changes:**
   - Compared the new ABC categories assigned to items with their original Maximo categories, noting any changes with a remark.

   ![Screenshot 2024-06-22 162205](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/193ba77c-ccce-4f9e-9775-f8ecfb630658)

7. **Creation of Measures for Category Changes:**
   - Developed measures to count and track the movement of items across different ABC categories from their original Maximo categories, providing insights into overall inventory restructuring.

8. **Dynamic Assessment for Newly Added Items:**
   - Introduced DAX calculations to dynamically assign newly added items into ABC categories based on their ADVU values relative to predefined thresholds (70% and 90% thresholds). This approach ensures ongoing accuracy in category assignments as the inventory evolves.

  ![Screenshot 2024-06-22 162310](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/ff22962e-4fb3-4e63-80cb-447584fba1d2)

![Screenshot 2024-06-22 162300](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/e6c83f33-c487-4702-af82-4442876d8649)


   ![Screenshot 2024-06-22 162245](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/fec3e0d5-5a0d-4d01-89d1-21f7bf4820e2)


This meticulous approach not only streamlined inventory management at PSGC but also facilitated dynamic reporting, ensuring that changes in item usage patterns are promptly reflected in the ABC analysis results.


### Project Conclusion and Future Directions

After completing the ABC Analysis of Plant Inventory project, I had the opportunity to present my findings to the stakeholders.This transition from manual to automated analysis was met with great relief by the warehouse management team at PSGC, who expressed great satisfaction with the streamlined process and actionable insights provided.

My Final dashboard looks like this:
![Screenshot 2024-06-22 165131](https://github.com/SagarKalauni/ABC-Analysis-of-Plant-Inventory/assets/141047160/8c00538a-8c4a-4f64-a50f-0ec7143b0b6b)

There are few more analysis on this dashboard which can be accessed thtough drill through but are not discussed here to mantain confidentiality.

The success of this project has opened doors to new opportunities. I have recently completed another project focused on Item Count Analysis of Plant Inventory, which proved even more intriguing. Details on this project will be discussed in the upcoming chapter.

Contributing to making someone's work easier and more efficient has been incredibly rewarding. It reaffirms the value of leveraging data analytics to drive meaningful improvements in operational efficiency and decision-making. I am grateful for the support and trust of PSGC's management throughout this journey.

Thank you for the opportunity to contribute to these impactful projects.




