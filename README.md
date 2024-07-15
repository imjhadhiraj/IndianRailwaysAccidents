# Indian Railways Accidents

### Project Description: Analyzing Railway Accidents in India

Railway accidents are unfortunate events that have significant impacts on public safety and transportation efficiency. Understanding the patterns and causes of these accidents can help in formulating strategies to enhance railway safety and prevent future occurrences. This project aims to analyze historical data on railway accidents in India to derive meaningful insights and identify trends.

#### Objectives
1. **Data Compilation**: Collect and compile comprehensive data on railway accidents from reliable sources such as Wikipedia.
2. **Database Creation**: Organize the data into structured tables using MySQL, ensuring it is readily accessible for analysis.
3. **Data Analysis**: Perform various operations and queries on the data to uncover trends, patterns, and critical insights.
4. **Visualization**: Use tools like Excel and Canva to create visual representations of the data, making the insights easier to understand and communicate.
5. **Dynamic Updates**: Implement an HTML form to dynamically update a Google Sheets Excel file, enhancing the user interface with CSS for better styling. This allows for automatic data entry by users who fill out the form.

#### Data Structure
The project will involve the creation of two primary tables in MySQL:
1. **Accident Information Table**: This table will include columns such as accident_id, date, state, train_name, casualties, and location.
2. **Train Information Table**: This table will include columns such as train_no, train_name, train_from, and train_to.

#### Key Operations
We will perform several key operations on the data, including but not limited to:
1. **Identifying the Train with the Most Accidents**: Analyzing which train has been involved in the highest number of accidents.
2. **Finding Routes**: Listing all trains that travel between major stations like Delhi and Patna.
3. **Average Casualties per Accident**: Calculating the average number of casualties per accident to understand the severity.
4. **Monthly Accident Trends**: Identifying which months have the highest frequency of railway accidents.
5. **Accident Locations**: Finding locations that have experienced multiple accidents to identify vulnerable areas.

#### Project Outcome
The project aims to provide a comprehensive analysis of railway accidents in India. The insights derived from this analysis can be used to inform policy decisions, enhance safety protocols, and ultimately reduce the occurrence of railway accidents. The final output will include detailed reports and visualizations that highlight key findings and recommendations.

By undertaking this project, we hope to contribute valuable knowledge to the field of railway safety and support efforts to make railway travel safer for everyone.

#### Operations

1. Displaying all the accidents.
   ```sql
   SELECT * FROM railwayaccidents.accidentinformation;
   ```

2. Displaying the details of Trains.
   ```sql
   SELECT * FROM railwayaccidents.traininfo;
   ```

3. Identify the major accidents (where casualties are greater than 100).
   ```sql
   SELECT * FROM AccidentInformation WHERE Casualties > 100;
   ```

4. Finding the Average Number of Casualties per Accident.
   ```sql
   SELECT AVG(Casualties) AS AverageCasualties FROM AccidentInformation;
   ```

5. Identifying Trains that met with accidents while going from Delhi to Bihar.
   ```sql
   SELECT TrainNo, TrainName, TrainFrom, TrainTo FROM TrainInfo WHERE TrainFrom = 'Delhi' AND TrainTo = 'Bihar';
   ```

6. List the departing station and the number of times a train departing from there met with an accident.
   ```sql
   SELECT ti.TrainFrom, COUNT(*) AS NoOfTimes FROM AccidentInformation ai INNER JOIN TrainInfo ti ON ai.TrainNo = ti.TrainNo GROUP BY TrainFrom;
   ```

7. Finding Trains with No Accidents.
   ```sql
   SELECT ti.TrainNo, ti.TrainName FROM TrainInfo ti LEFT JOIN AccidentInformation ai ON ti.TrainNo = ai.TrainNo WHERE ai.AccidentID IS NULL;
   ```

8. Finding Accidents by Train in a Specific State.
   ```sql
   SELECT ai.AccidentID, ai.Date, ai.State, ai.Casualties, ai.Location, ti.TrainName FROM AccidentInformation ai INNER JOIN TrainInfo ti ON ai.TrainNo = ti.TrainNo WHERE ti.TrainName = 'Coromandel Express' AND ai.State = 'Odisha';
   ```

9. Finding Accidents in a Specific Year.
   ```sql
   SELECT AccidentID, Date, State, Casualties, Location, TrainNo FROM AccidentInformation WHERE YEAR(Date) = 2023;
   ```

10. Identifying the Train with the Maximum Accidents.
    ```sql
    WITH cte AS (SELECT ti.TrainName, COUNT(*) AS occ FROM AccidentInformation ai INNER JOIN TrainInfo ti ON ai.TrainNo = ti.TrainNo GROUP BY ti.TrainName), ranked_cte AS (SELECT TrainName, occ, ROW_NUMBER() OVER (ORDER BY occ DESC) AS rn FROM cte) SELECT TrainName FROM ranked_cte WHERE rn = 1;
    ```
