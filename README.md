# Heart Failure Patient Analysis Using Power BI / DAX



## Problem Statement

Heart failure is a critical condition that requires comprehensive analysis to understand the various factors influencing patient outcomes. Healthcare providers need an efficient way to analyze patient data, including demographics, medical history, and clinical metrics, to identify patterns and make informed decisions. The challenge is to create an interactive and intuitive tool that allows for the exploration of this data to gain insights into key health indicators and their impact on mortality rates and overall patient health. This project aims to address this need by utilizing Power BI and DAX to transform raw data into a meaningful and accessible dashboard for healthcare professionals.


### Steps followed 

- Step 1 : Data was sourced from Kaggle.com.
- Step 2 : Excel was utilized to clean and preprocess the raw data.
- Step 3 : The processed data was imported into Power BI.

- Step 4 : A new column was created to categorize group ages.
            
            Age Bin = SWITCH(
                 TRUE(),
                 heart_failure[age] <= 10, "0-10",
                 heart_failure[age] <= 20, "10-20",
                 heart_failure[age] <= 30, "20-30",
                 heart_failure[age] <= 40, "30-40",
                 heart_failure[age] <= 50, "40-50",
                 heart_failure[age] <= 60, "50-60",
                 heart_failure[age] <= 70, "60-70",
                 heart_failure[age] <= 80, "70-80",
                 heart_failure[age] <= 90, "80-90",
                 "90+"
             )
        

- Step 5 : Another column was created to help with sorting the age groups in the visualization.

                Age Bin Sort Order = 
                SWITCH(
                    TRUE(),
                    heart_failure[age] <= 10, 1,
                    heart_failure[age] <= 20, 2,
                    heart_failure[age] <= 30, 3,
                    heart_failure[age] <= 40, 4,
                    heart_failure[age] <= 50, 5,
                    heart_failure[age] <= 60, 6,
                    heart_failure[age] <= 70, 7,
                    heart_failure[age] <= 80, 8,
                    heart_failure[age] <= 90, 9,
                    10
                )

- Step 6 : A last column was added to group up the follow_up of the patients.

            Age Follow-Up Bin = 
                SWITCH(
                    TRUE(),
                    heart_failure[Follow_up] <= 30, "0-30",
                    heart_failure[Follow_up] <= 60, "31-60",
                    heart_failure[Follow_up] <= 90, "61-90",
                    heart_failure[Follow_up] <= 120, "91-120",
                    "120+"
                )

    ![image](https://github.com/Ndaaboul/Portfolio/assets/123441867/ba31a7f9-31cc-40fc-8536-e6e4803092e2)


- Step 7 :To effectively analyze the heart failure patient data and visualize key insights, I utilized Power BI and DAX to transform the raw data into meaningful metrics. One of the critical steps in this process involved creating several calculated measures. These Measures were:

    1-

            Percentage_Females_Die_From_HeartFailure = 
                DIVIDE(
                 CALCULATE(COUNTROWS(Heart_Failure), Heart_Failure[sex] = "Female", Heart_Failure[DEATH_EVENT] = "Yes"),
                 CALCULATE(COUNTROWS(Heart_Failure), Heart_Failure[sex] = "Female"),
                  0
            )

    2-

            Percentage_Males_Die_From_HeartFailure = 
                DIVIDE(
                 CALCULATE(COUNTROWS(Heart_Failure), Heart_Failure[sex] = "male", Heart_Failure[DEATH_EVENT] = "Yes"),
                 CALCULATE(COUNTROWS(Heart_Failure), Heart_Failure[sex] = "male"),
                0
                )  

    3-

            Percentage_Females_With_HeartFailure = 
                DIVIDE(
                    CALCULATE(COUNTROWS(Heart_Failure), Heart_Failure[sex] = "Female"),
                    COUNTROWS(Heart_Failure),
                    0
                 ) 

    4-

            Percentage_Men_With_HeartFailure = 
                DIVIDE(
                 CALCULATE(COUNTROWS(Heart_Failure), Heart_Failure[sex] = "Male"),
                 COUNTROWS(Heart_Failure),
                 0
             ) 

    5-

            CountFemale = 
                 CALCULATE(COUNTROWS(Heart_Failure), Heart_Failure[sex] = "Female")

    6-

            CountMale = 
                 CALCULATE(COUNTROWS(Heart_Failure), Heart_Failure[sex] = "male")

    7-

            Survivals Count = 
                CALCULATE(
                 COUNT(heart_failure[DEATH_EVENT]),
                 heart_failure[DEATH_EVENT] = "no"
                )

    8-

            Deaths Count = 
                CALCULATE(
                    COUNT(heart_failure[DEATH_EVENT]),
                    heart_failure[DEATH_EVENT] = "yes"
                )

    9-

            Anaemia Percentage = 
                DIVIDE(
                 COUNTAX(FILTER(heart_failure, heart_failure[anaemia] = "yes"), heart_failure[anaemia]),
                 COUNT(heart_failure[anaemia])
                ) * 100

    10- 

            Diabetes Percentage = 
                DIVIDE(
                    COUNTAX(FILTER(heart_failure, heart_failure[diabetes] = "yes"), heart_failure[diabetes]),
                    COUNT(heart_failure[diabetes])
                ) * 100
    11-

            High Blood Pressure Percentage = 
                DIVIDE(
                    COUNTAX(FILTER(heart_failure, heart_failure[high_blood_pressure] = "yes"), heart_failure[high_blood_pressure]),
                    COUNT(heart_failure[high_blood_pressure])
                ) * 100

    12- 

            Smoking Percentage = 
                DIVIDE(
                 COUNTAX(FILTER(heart_failure, heart_failure[smoking] = "yes"), heart_failure[smoking]),
                 COUNT(heart_failure[smoking])
                ) * 100

    



- Step 8 : two crucial cards were developed to provide essential insights:

    A. Gender Distribution Card: One card was dedicated to showcasing the distribution of genders among the 5000 patients included in the study. By leveraging calculated measures, the card displays the percentage of females to males in the dataset. This measure allowed for a clear visualization of gender proportions, providing valuable context for further analysis.

    B. Death Percentage by Gender Card: Another important card focused on depicting the death percentage among genders. Through calculated measures, the card presents the percentage of patients who experienced death categorized by gender. This visualization enables a comparative analysis of mortality rates between male and female patients, offering insights into potential gender-based disparities in health outcomes.
       
![Cards](https://github.com/Ndaaboul/Portfolio/assets/123441867/9bc16de6-3512-43e5-828a-8d6763c99cbd)



- Step 9 : clustered column chart that effectively displays the percentages of the following health indicators:

    A. Anaemia: The percentage of heart failure patients diagnosed with anaemia.

    B. Diabetes: The percentage of heart failure patients diagnosed with diabetes.

    C. High Blood Pressure: The percentage of heart failure patients diagnosed with high blood pressure.

    D. Smokers: The percentage of heart failure patients who are smokers.

Each health indicator was represented as a distinct column in the chart, with the height of the column indicating the respective percentage. The clustered layout facilitated easy comparison between the different health indicators, allowing for quick identification of prevalent conditions among heart failure patients.

This visualization provides valuable insights into the distribution of key health factors within the heart failure patient population, aiding healthcare professionals in understanding the overall health profile of these patients and informing potential interventions and treatment strategies.

![Clustered](https://github.com/Ndaaboul/Portfolio/assets/123441867/3186e8a0-797a-4cd1-b4f9-9c1e4f15a052)



- Step 10 : I proceeded to create stacked column charts to illustrate the distribution of death and survival rates across different age groups. This visualization aimed to provide insights into the relationship between age and patient outcomes, facilitating a deeper understanding of mortality patterns within the heart failure patient population.

![DeathSurvival](https://github.com/Ndaaboul/Portfolio/assets/123441867/23579581-1a55-4408-a955-c5ee3e6aef00)


- Step 11 : Using Power BI's analytical capabilities, I computed the average follow-up days for each age group and visualized the results in a bar chart. Each bar in the chart represents an age group, and the height of the bar corresponds to the average follow-up duration for that group. This visualization enables easy comparison of follow-up days across different age categories, allowing for the identification of any age-related variations in patient care and monitoring.

    By analyzing the average follow-up days by age group, healthcare professionals can gain insights into the effectiveness of follow-up protocols and the level of engagement among patients of different age demographics. This information can inform strategies for optimizing patient care and improving outcomes, ultimately enhancing the quality of care for heart failure patients across all age groups.

![FollowUp](https://github.com/Ndaaboul/Portfolio/assets/123441867/3cb1aa0b-6612-4221-8a27-006f9103a900)



- Step 12 : In this analysis, I utilized a stacked bar chart in Power BI to depict the distribution of key health conditions among heart failure patients across different age groups. The chart showcases the percentages of patients with anaemia, diabetes, high blood pressure, and smokers within each age demographic. This visualization enables quick comparison and identification of prevalent health conditions across age groups, facilitating targeted treatment strategies and improving patient care.

![Health Conditions](https://github.com/Ndaaboul/Portfolio/assets/123441867/566da9d7-0320-4e0d-a43c-4fe222fce990)

- Step 13 :Lastly, a table was created that provides a concise summary of heart failure patient demographics and healthcare engagement metrics. It includes age groups, average follow-up days, number of visits, and the distribution of patients by gender. This comprehensive overview allows for easy comparison of patient characteristics and healthcare utilization patterns, aiding healthcare professionals in understanding and managing heart failure patient care effectively.

![Table](https://github.com/Ndaaboul/Portfolio/assets/123441867/a543e69d-9aa1-4a77-a9be-f599343960ab)

VIEW OF THE FULL DASHBOARD:

![DashBoard](https://github.com/Ndaaboul/Portfolio/assets/123441867/bc491a46-70db-4183-8ff0-f659b0324de7)


