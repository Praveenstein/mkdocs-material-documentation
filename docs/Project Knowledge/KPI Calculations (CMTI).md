# Intro
## Raw Data

Most of the machine will expose certain raw data, which can be used along with other sets of data to find the KPIs. The raw data available/required are:

1. Operating Mode:
    This refers to the mode of operation in the cnc machine, for example, `MEM` is memory mode, in this CNC system runs programs stored in its memory. This mode is also known as the automatic mode, where the CNC machine loads the entire G Code file into its memory and executes it automatically, without any manual intervention. In this mode, the machine follows the instructions provided in the G Code file from start to finish. The entire code is executed sequentially, allowing for a fully automated operation. The machine takes care of executing each command in the G Code file without requiring any further input or interaction from the operator.

    In the execution of this project, finding out when the machine is in `MEM` mode is crucial, as this denotes the fact the production of a part has started (anything operation that isdone in other mode such as say `Edit` mode will usually be considered as non productive time, hence will contribute to prouction loss).

2. Program Status:
    This refers to the status of the program that is loaded in memory (if nothing is loaded, then a default value such as 0 might be returned). For example a number of 3 from the machine might denote that the program is started and a value of 1 might mean the program got over. In most of the cases in the machine, we might have to do some trail experiments to see what those numbers represent.

3. Machine Status:
    This refers to the staus of machine, which could (mostly) take one of the values: `PRODUCTION`, `IDLE`, `OFF`, or something similar to that. This parameter could sometime be retrieved as raw data, or it might be takes as a derived information from the operating mode and program status. This data is important to understand how much the machine was utilized. When this information is not available directly when get it as follows: 

        1. If operating mode is ``auto`` && program status is ``start`` (or anything similar) then the machine is in ``PRODUCTION``
        2. If any other combination if operation mode and program status then the machine is in ``IDLE`` status.
        3. If no data is coming the machine is in ``OFF`` status. 

4. Program Name:
    This represents the program name that is being currently executed by the machine. This is an important information to find details such as idle cycle time for a given program, which in turn will be used to find the performace and oee metrics.

## OEE Metrics2

The final KPI that we need to show are listed below:

1. Availability
    - For current shift
    - For current day
    - For cumulative (since the beginning of the project)
2. Performance
    - For current shift
    - For current day
    - For cumulative
3. Quality
    - For current shift
    - For current day
    - For cumulative
4. OEE
    - For current shift
    - For current day
    - For cumulative 

### Calculations 2

In this section we will show how to calculate all the above KPIs.

1. Availablity: 

The formula for availability is given by:

$$
\text{Availability} = \frac{\text{Actual Production Time}}{\text{Planned Production Time}}
$$


#### CASE 1 (Machine state change from production to idle)

Let's say the machine has changed its state from production to idle just now, we need to have the following data

Start time of (previous) production cycle : 31-05-2023T11:15:03 

End time of production cycle (just now) : 31-05-2023T11:19:22

1. Find the planned production time for the given duration:
    
    1. We can see that from the planned event timeline, the production start and end datetime falls under prodution (full time), hence the planned production time for the given query time duration is the query time duration itself (which is 31-05-2023T11:19:22 - 31-05-2023T11:15:03 = 289 s). (Usually the production will be done in planned production time, hence by default it will be equal to the difference between end and start time, we can hopefully skip the part where we have to check if the production was done during any of the planned production time).

    $$
    \text{Planned Production Time} = \text{289}
    $$

2. Find the Actual Production Time:

    The actual production time is same as the difference between the end and start time.

    $$
    \text{Actual Production Time} = \text{289}
    $$

3. Find Availability:
    
    1. By substituting in the previous formula we can find the value

    $$
    \text{Availability} = \frac{\text{289}}{\text{289}}
    $$

    $$
    \text{Availability} = {\text{1}}
    $$

    $$
    \text{Availability \%} = {\text{100 \%}}
    $$


#### CASE  (Machine state change from idle to production)

Let's say the machine has changed its state from idle to production just now, we need to have the following data

Start time of idle time : 31-05-2023T11:15:03 

End time of idle (just now) : 31-05-2023T11:19:22

1. Find the planned production time for the given duration:
    
    1. We can see that from the planned event timeline, the production start and end datetime falls under prodution (full time), hence the planned production time for the given query time duration is the query time duration itself (which is 31-05-2023T11:19:22 - 31-05-2023T11:15:03 = 289 s). (Usually the production will be done in planned production time, hence by default it will be equal to the difference between end and start time, we can hopefully skip the part where we have to check if the production was done during any of the planned production time).

    $$
    \text{Planned Production Time} = \text{289}
    $$

2. Find the Actual Production Time:

    The actual production time is same as the difference between the end and start time.

    $$
    \text{Actual Production Time} = \text{289}
    $$

3. Find Availability:
    
    1. By substituting in the previous formula we can find the value

    $$
    \text{Availability} = \frac{\text{289}}{\text{289}}
    $$

    $$
    \text{Availability} = {\text{1}}
    $$

    $$
    \text{Availability \%} = {\text{100 \%}}
    $$


### Calculations

In this section we will show how to calculate all the above KPIs.



## OEE Metrics

Since there is not much production going in CMTI, and due to lack of systematic method for manufacturing, we're are using a different approach to calculate the KPIs, which will not reflect the actual performance of the plant and machine, but for the sake of demonstration we have to do this.

Let's explain the calculation with a sample data shown below:


Machine Production Timeline:

| S.No | Machine Name | Start Time          | End Time            | Duration*| Ideal Time    | Product Name | Program Name    | Part Status   |
|------|--------------|---------------------|---------------------|----------|---------------|--------------|-----------------|---------------|
| 1.   | MCV - 450    | 31-05-2023T11:15:03 | 31-05-2023T11:17:09 | 126      | 120           | CNC_DRILL_1  | crank_feature_1 | 1             |
| 2.   | MCV - 450    | 31-05-2023T11:17:45 | 31-05-2023T11:19:22 | 127      | 120           | CNC_DRILL_1  | crank_feature_1 | 2             |


\* Sometime the duration column in the above table will not be exactly equal to the difference between end and start time columns, reason is, the machine could have been stopped in the middle of production for minor adjustments, which could be seen in the machine status timeline table.


Part Status Desctiption Table:

| Id (PK) | Part Status       | Description                                                                                                                                                             | Category        |
|---------|-------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| 1.      | Good              | This denotes the part is of good quality and was manufactured according the given tolerances                                                                            | good            |
| 2.      | rework_start_up   | This denotes the part is was of bad quality but it could be made good by rework, it was part of the start up phase of the production, where fault will be usually high  | loss_start_up   |
| 3.      | scrap_start_up    | This denotes the part is was of bad quality and cannot be reworked, it was part of the start up phase of the production, where fault will be usually high               | loss_start_up   |
| 4.      | rework_production | This denotes the part is was of bad quality but it could be made good by rework, it was part of the production phase of the production, where fault will be usually low | loss_production |
| 5.      | scrap_production  | This denotes the part is was of bad quality and cannot be reworked, it was part of the production phase of the production, where fault will be usually low              | loss_production |


Machine Status Timeline:

| S.No | Machine Name | Start Time          | End Time            | Duration | Machine State | Label        | Label Value               | 
|------|--------------|---------------------|---------------------|----------|---------------|--------------|---------------------------|
| 1.   | MCV - 450    | 31-05-2023T11:15:03 | 31-05-2023T11:17:09 | 126      | production    | program name | crank_feature_1           |
| 2.   | MCV - 450    | 31-05-2023T11:17:09 | 31-05-2023T11:17:45 | 36       | idle          | reason       | setup_and_adjustments     | 
| 3.   | MCV - 450    | 31-05-2023T11:17:45 | 31-05-2023T11:19:22 | 127      | production    | program name | crank_feature_1           |


Planned Event Timeline:

| S.No | Date       | Shift | Start Time         | End Time           | Duration (s) |
|------|------------|-------|--------------------|--------------------|--------------|
| 1.   | 31/05/2023 | 1     | 31-05-2023T8:00:00 | 31-05-2023T4:00:00 | 28800        |


## Availability

The formula for availability is given by:

$$
\text{Availability} = \frac{\text{Actual Production Time}}{\text{Planned Production Time}}
$$


Let's say we want to find the availability between 

Start time : 31-05-2023T11:15:03 

End time: 31-05-2023T11:19:22

1. Find the planned production time for the given duration:
    
    1. We can see that from the planned event timeline, the query start and end datetime falls under prodution (full time), hence the planned production time for the given query time duration is the query time duration itself (which is 31-05-2023T11:19:22 - 31-05-2023T11:15:03 = 289 s).

    $$
    \text{Planned Production Time} = \text{289}
    $$

2. Find the Actual Production Time:
    
    1. The actual production time is given by summation of duration column in the Machine Production Timeline table for all rows where the start and end time is within the query range.
    2. For example in the current case: 126 + 127 = 253 seconds.

    $$
    \text{Actual Production Time} = \text{253}
    $$

3. Find Availability:
    
    1. By substituting in the previous formula we can find the value

    $$
    \text{Availability} = \frac{\text{253}}{\text{289}}
    $$

    $$
    \text{Availability} = {\text{0.8754}}
    $$

    $$
    \text{Availability \%} = {\text{87.54 \%}}
    $$

## Performance

The formula for Performance is given by:

$$
\text{Performance} = \frac{\text{Ideal Production Time}}{\text{Actual Production Time}}
$$

1. Find Ideal Production Time:
    
    1. The ideal production time is determined by summing up the ideal cycle times for all the cycles that occurred between the given start and end time. For the solution deployed at cmti, this is available in the machine production timeline table, with the column name of `Ideal Time` . The collector which collects the data from the machine, will give a dummy data for this by taking a value that is between 90 % and 98 % of the actual duration time. This is something that we have to do, since there is no systematic way to get the ideal time in the current set up at cmti, and since we have to demonstrate a prototype we use some same value.

        $$
        \text{Ideal Production Time} = \sum \text{Ideal Cycle Times for All Cycles during the given Query Range}
        $$

    2. For example in the previous case, the following would be applicable
        
        120 + 120 = 240

        $$
        \text{Ideal Production Time } = {\text{240}}
        $$

2. The actual production time is already found in previous metric(Availability):

3. Find Performance

    $$
    \text{Performance} = \frac{\text{Ideal Production Time}}{\text{Actual Production Time}}
    $$

    $$
    \text{Performance} = \frac{\text{240}}{\text{253}}
    $$

    $$
    \text{Performance} = {\text{0.9486}}
    $$

    $$
    \text{Performance \%} = {\text{94.86 \%}}
    $$



## Quality

The formula for Quality is given by 

$$
\text{Quality} = \frac{\text{Good Parts Produced}}{\text{Total Parts Produced}}
$$

1. Total Parts:
    This can be calculated by querying the table of machine production timeline, the total count equal to the number of rows with column 'Machine State' equal to production and 
    
2. The number of good parts is equal to the number of rows where the rejected is not equal to 'No'.

3. For example in the above case 

    $$
    \text{Quality} = \frac{\text{2}}{\text{2}}
    $$

    $$
    \text{Quality } = {\text{1}}
    $$

    $$
    \text{Quality \%} = {\text{100 \%}}
    $$

## Overall Equipment Effectiveness (OEE)

The formula for OEE is given by 

$$
\text{OEE} = {\text{Availability}}\times{\text{Performance}}\times{\text{Quality}}
$$

$$
\text{OEE} = {\text{0.8754}}\times{\text{0.9486}}\times{\text{1}}
$$

$$
\text{OEE} = {\text{0.8304}}
$$

$$
\text{OEE \%} = {\text{83.04 \%}}
$$

## Six Big Losses
The Six Big Losses are a key concept in Total Productive Maintenance (TPM) and Overall Equipment Effectiveness (OEE). They represent the most common causes of efficiency loss in manufacturing. Here they are:

1. **Downtime Loss (Mapped to Availability in OEE)** 
    - **Breakdowns:** These are instances of equipment failure that result in unscheduled downtime. They can be caused by tooling failures, unplanned maintenance, equipment breakdown, etc.

    - **Setup and Adjustments:** This refers to the time taken to change over from one product variant to another. It includes setup and adjustment time during which the equipment is not operational.

    - **Idling and Small Stops:** These refer to minor stops or pauses in the production process that last for less than 5 minutes and do not require maintenance personnel. They can occur due to issues like a blocked sensor, a minor jam, or idle time during part changeover.

    - It is the collector's responsibility to accurately identify the reason for the machine's idle state. One simple method is to categorize durations less than 5 minutes as "Idling and Small Stops," durations between 5 minutes and 2 hours as "Setup and Adjustments," and durations exceeding 2 hours as "Breakdowns."

    - **Calculation:** To calculate the losses associated with these conditions within a specific time range, we need to query the `Machine Status Timeline` table for that range, focusing on entries where the `Machine State` column indicates an idle or off condition. For cumulative downtime, we sum the duration values across all corresponding rows related to the above conditions. To obtain individual values, we further filter the rows based on the label column, using the following criteria:

        - **Breakdowns:** Select entries where the machine state is idle or off, and the label value is `breakdown`.

        - **Setup and Adjustments:** Select entries where the machine state is idle or off, and the label value is `setup and adjustments`.

        - **Idling and Small Stops:** Select entries where the machine state is idle or off, and the label value is `idling and small stops`.

2. **Speed Loss (Mapped to Performance in OEE)**
    - **Reduced Speed:** This refers to instances where the machinery is operating, but not at its optimal speed. This could be due to wear and tear, equipment issues, or sub-optimal operating conditions.
    
    - **Calculation:** The formula for reeduced speed loss is given by the following formula, and it is almost similar to calculation of performance

        $$
        \text{Reduced Speed Loss} = \frac{\text{Actual Production Time - Ideal Production Time}}{\text{Actual Production Time}}
        $$

3. **Defect Loss (Mapped to Quality in OEE)**
    - **Startup Rejects:** These are defects that occur during the startup phase of production. When equipment is first started, it may take a while for it to operate correctly, resulting in defective output.
    
    - **Calculation:** To determine the start-up reject loss within a given time range, you can refer to the `Machine Production Timeline` table. By filtering out the rows with a `Part Status` column value of either 2 or 3, corresponding to `rework_start_up` or `scrap_start_up` in the Part Status Description Table, you can identify the start-up reject instances. Let's assume there are 3 such rows. To calculate the start-up reject loss, you need to consider the total number of parts produced during that time range, which includes both good and bad parts. This can be determined by counting the total number of rows in the table within the specified time range, let's say it's 10. The start-up reject loss can then be calculated as follows:

        $$
        \text{Startup Rejects Loss} = \frac{\text{Bad Parts Produced During Start Up}}{\text{Total Parts Produced}}
        $$

        $$
        \text{Startup Rejects Loss} = \frac{\text{3}}{\text{10}}
        $$

        $$
        \text{Startup Rejects Loss \%} = \text{30 \%}
        $$

    - **Production Rejects:** These are defects that occur during steady-state production. Despite the equipment running as expected, there can still be quality losses due to factors like tool wear or process variation.
    
    - **Calculation:** To determine the start-up reject loss within a given time range, you can refer to the `Machine Production Timeline` table. By filtering out the rows with a `Part Status` column value of either 4 or 5, corresponding to `rework_production` or `scrap_production` in the Part Status Description Table, you can identify the production reject instances. Let's assume there are 2 such rows. To calculate the production reject loss, you need to consider the total number of parts produced during that time range, which includes both good and bad parts. This can be determined by counting the total number of rows in the table within the specified time range, let's say it's 10. The production reject loss can then be calculated as follows:

        $$
        \text{Production Rejects Loss} = \frac{\text{Bad Parts Produced During Production}}{\text{Total Parts Produced}}
        $$

        $$
        \text{Production Rejects Loss} = \frac{\text{2}}{\text{10}}
        $$

        $$
        \text{Production Rejects Loss \%} = \text{20 \%}
        $$

    - To classify the losses into rework and scrap categories, we can apply additional filtering based on the Part Status column value. Specifically, we can include values 2, 3, 4, or 5, which correspond to different types of losses: rework loss during start-up, scrap loss during start-up, rework loss during production, and scrap loss during production, respectively. By filtering the Part Status column to only include these values, we can further categorize the losses accordingly.

By identifying and targeting these Six Big Losses, manufacturers can significantly improve their OEE and overall productivity.
