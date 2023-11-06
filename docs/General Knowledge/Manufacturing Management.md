# Management Concepts

## Shifts in Manufacturing
A shift is a period of time during which a group of workers performs their duties. Shifts are typically 8 hours long, but they can be longer or shorter depending on the needs of the company.

Manufacturing companies often use shifts to keep their operations running 24 hours a day, 7 days a week. This is especially important for companies that produce essential goods, such as food, medicine, and energy.

There are many different ways to schedule shifts in a manufacturing company. One common approach is to use a rotating shift schedule. In this type of schedule, workers rotate between different shifts on a regular basis. This helps to ensure that everyone has a fair share of working day shifts and night shifts.

Another common approach is to use a fixed shift schedule. In this type of schedule, workers are assigned to a specific shift and work that shift every day. This type of schedule can be beneficial for workers who prefer to have a regular routine.

Here is an example of a typical shift schedule in a manufacturing company:

- Shift 1: 6:00 AM - 2:00 PM

- Shift 2: 2:00 PM - 10:00 PM

- Shift 3: 10:00 PM - 6:00 AM

Each shift would have its own group of workers who are responsible for operating the machinery and producing the products. The workers would typically rotate between shifts on a weekly basis, so that everyone has a chance to work day shifts and night shifts.

Shift work can be challenging, but it is also an important part of many manufacturing companies. By using shifts, these companies can keep their operations running 24/7 and produce the goods that we all rely on.

Key point to remeber is that, shift is a concept of factory and group of workers.

## Ramifications of Shift in KPI calculations

One thing to remember is that our KPIs should go down only if there is something wrong with the machine/resource/enviroment. Look at the following case, lets say we have two shifts, and lets say the a machine (1) was not planned to be run, then its actual production time would be zero, which will result in availabilty becoming zero (by raw formula calculation), meaning it has decreased, which means something is wrong with the machine, but we did not plan to run the machine, hence there is nothing wrong with the machine, hence the availability should be set to 100.

When the shift changes, the parameters that affect the KPI parameters will need to be reset to zero, such as actual production time, ideal cycle time, actual total number of parts. (applicable only for parameter for shift and day based, cumulative will stay unaffected).

And when calculating KPI for the individual machines (whole factory) we need to make sure that the machine was acutally planned to be run in that shift, if not, then that duration should not be added to the planned production time

This could be done by checking that the current machine was planned to run in the current shift and also if the machine was planned to run, and has finished the planned number of parts during that shift  {early finish}, then the remaining time should not be added to the planned production {since that would decrease the KPI, since the actual production will not increase}, so we should check if the machine was planned to be run in this shift, and also check if the total part count is less than the planned part count.
